# Inkwell — PLAN

Living plan. Research: `replica/research.md`. Manual steps: `NOTES.md`.

## Context
Luca wants a personal notes app (not for the App Store) for handwritten notes on an **iPad Pro (M4/M5) with Apple Pencil Pro**, also usable on his **Mac (M5, macOS 26.6.2)** for reading, organising, typed text and trackpad drawing. GoodNotes shows the kind of app this is meant to be, but this is not a copy of it. Notes must stay current on both devices and be kept safe. Hard rules from the spec:
- Never destroy or alter original ink.
- Sync must never lose data.
- Everything is processed on-device.

He writes **English plus maths notation**, in **cursive**, with many **diagrams and graphs**.

**Constraint: no $99 Apple Developer Program.** Consequences:
- Apps are signed with a free "Personal Team". On the iPad they expire after **7 days** and must be reinstalled from Xcode. Notes are kept, provided the app is never deleted. Source: [Apple: provisioning profile expiring in 7 days](https://developer.apple.com/forums/thread/69248).
- **CloudKit / the iCloud capability is not available**, as far as I can tell. Apple lists it as a paid-programme capability, but I couldn't read the exact table row, so I'll confirm in Xcode during Step 0.5.
- **Sync therefore goes through an ordinary folder in Luca's iCloud Drive**, picked once on each device. The app does not need the iCloud entitlement for this.

Decisions already made: erasing is a real edit, backed by undo and history; PencilKit for inking, with our own stroke format as the source of truth; the iPhone is dropped.

## Product decisions (agreed in discussion)
**Features and UI**
- **Library:** nested folders, like Finder (e.g. Uni → Economics → Macro).
- **Pages** scroll vertically. Pages are **shaped like the iPad screen**; imported PDF pages keep their own size.
- **New page:** lined/grid/blank chips at the foot of each fresh page, defaulting to the last paper used. Paper can be changed later on any page. Pages are separate (ink never flows across a page break).
- **Tools:** a slim top bar with tools and colours.
  - **Pencil Pro squeeze:** a quick squeeze toggles pen ↔ eraser; squeeze-and-hold is a temporary eraser, and letting go returns to the pen. This overrides the system squeeze preference for this app; I'll check that Apple allows this.
  - **Double-tap = open the tool palette.**
- **Finger drawing:** a toggle, **off by default**. When it's off, fingers only scroll and zoom.
- **Dark mode** changes the app UI only. Paper stays white.
- **Name:** Inkwell.
- **Pen presets:** 3 **ballpoint** pens and 2 highlighters, each with its own colour and thickness. Long-press a preset to edit it. Undo button at the top-left.
- **Gestures:** two-finger tap undoes, three-finger tap redoes. Scratch-out to erase is **opt-in**. Insert-space gesture (two-finger long-press + drag).
- **Shape snapping** (hold the pen still about 0.5 s, raw stroke kept, angle/endpoint snapping) comes **right after the MVP**, ahead of text neatening.
- **Highlighter:** draws **behind** the ink and **snaps straight**.
- **Mac layout:** folder sidebar plus the page, with standard shortcuts (⌘N, ⌘Z, ⌘F).
- **After the MVP:** tabs and split view (slides beside notes), and more templates (Cornell, dotted, maths graph paper, custom spacing).

**Sync and security**
- **Conflicts:** keep both versions, outline the clashing ink, and show an "N conflicts" badge. Luca resolves them whenever he likes.
- **History:** 30 days of daily snapshots, and Trash keeps deleted notebooks for 30 days. The raw operation log itself is never deleted, so the rule that ink is never destroyed still holds.
- **No app lock.** Nothing is employer-confidential.
- **Automatic PDF mirror:** every notebook gets a read-only PDF copy in the sync folder, updated a few seconds after writing stops. Notes stay readable even if the app breaks or expires.

**Neatening**
- **Goals:** slight changes so messy handwriting looks neater. Straight lines of text, evenly sized words, clean diagrams and smoother strokes.
- **Runs live, line by line.** When Luca moves on to the next line, the line he just finished is neatened after a short pause. Ink that's still being written is never moved.
- **One global on/off switch.** A strength slider, gentle by default. One-tap revert on any line.
- **Maths is always skipped** apart from light smoothing. On blank pages, the lines are estimated from the writing, with lower confidence, so less is changed there.
- **Tuning data:** after the MVP, Luca writes test pages in the app, giving real stroke data. Those samples are never committed.

## Architecture
- **Xcode project `Inkwell`** (working name, rename freely). One app target for **iPadOS + Mac Catalyst**, so the same UIKit/PencilKit code runs on both, and the Mac build is a real Mac app.
- **Swift package `NoteCore`** (pure Swift, no UI). Contains the data model, file format, operation log, merge logic, neatening geometry and search index. Its tests run on the Mac with `swift test` / `xcodebuild test`, without a device.
- **App layer:**
  - SwiftUI for the library, navigation and settings.
  - `PKCanvasView`, wrapped in UIKit, for the page canvas.
  - PDFKit for PDF backgrounds and export.
  - Text boxes as overlay views.
  - On the Mac, `drawingPolicy = .anyInput` so the trackpad and mouse can ink.
- PencilKit is used only to capture and render strokes. Every finished stroke is converted into a `NoteCore.Stroke` and saved as an operation. On load, the page's `PKDrawing` is rebuilt from our strokes.

## Data model (NoteCore)
- `Notebook {id, title, createdAt, pageOrder}`, where page order uses fractional-index keys so that concurrent reorders merge.
- `Page {id, template: blank|lined|grid(spacing), pdfBackground?: (assetHash, pageIndex), size}`
- `Stroke {id: UUID, tool: pen|highlighter, colour, width, points: [x, y, t, force, azimuth, altitude, roll?], createdOn: deviceID}`. Strokes are immutable values.
- `TextBox {id, frame, text, style}`
- `NeatenedVariant {id, sourceStrokeIDs, algorithmVersion, params, resultStrokes}`. Stored **alongside** the raw strokes. A page or group shows either raw or neatened ink, and switching is just a display flag. Raw strokes are never changed.
- Partial erase = `replaceStroke(old → [fragments])`. The old stroke stays in the log, so page history can bring it back.

## File format and sync (works without CloudKit)
Each notebook is a folder inside the chosen iCloud Drive folder:
```
Lecture Notes.inkbook/
  devices/<deviceID>/ops-000001.jsonl …   append-only, written ONLY by that device
  assets/<sha256>.pdf                      immutable, content-addressed PDFs
  cache/…                                  rebuildable snapshots (never authoritative)
```
- **No two devices ever write the same file**, so iCloud Drive can never create conflicting file versions or silently overwrite one. Each device reads every device's log and merges them, and the result is deterministic.
- Every operation carries `(deviceID, seq, versionVector)`. Merge rules:
  - Adds always merge.
  - When two devices change the same object concurrently (move/erase/neaten the same stroke, edit the same text box, rename the notebook), **both versions are kept** and a conflict is flagged in the UI for Luca to resolve.
  - When a delete and an edit are concurrent, the edit wins, so nothing is lost silently.
- Files are written with `NSFileCoordinator`, atomically. Log segments are sealed by size. A log that's incomplete or missing (partial sync) only delays merging; it never corrupts anything.
- Folder access is a **security-scoped bookmark** created by the document picker, on both iPad and Mac.
- Changes are detected with `NSFilePresenter`, a rescan when the app comes to the foreground, and polling every few seconds while a notebook is open. Expect the other device's changes to arrive **within seconds to a couple of minutes**; iCloud Drive controls the timing.
- Evicted files are downloaded on demand through coordinated reads.
- **Sync status:**
  - Per notebook: "saved locally / uploading / up to date / waiting for other device's data", based on ubiquitous resource keys (needs verifying in the spike).
  - A "N conflicts" badge.
- **Deleting a notebook** moves it to a `.Trash` folder inside the sync folder for 30 days.
- **Backups:**
  - A daily local snapshot (zip) in the app's own container, which is not synced, keeping 30 days.
  - An "Export all" (zip + PDFs) button.
- **Security:**
  - Files are protected at rest by the device passcode.
  - Recommend turning on **Advanced Data Protection** (end-to-end encrypted iCloud). This is a manual step.
  - No app-level encryption. A lost key would mean lost notes, which is a worse risk for Luca.

## Phases (revised)
- **0.5 — Sync spike (do this first, about 1 day).** A throwaway app on the iPad and the Mac. Confirm:
  - The free Personal Team can't add iCloud.
  - The picked iCloud Drive folder bookmark survives app restarts **and the 7-day reinstall**.
  - Changes made on one device show up on the other.
  - Evicted files download.
  - Upload-status keys work.
  - PencilKit works with a mouse under Mac Catalyst.
  - Whether the Mac Catalyst build also expires under a Personal Team.

  If anything fails, stop and re-plan before any real code is written.
- **1 — MVP (local).** Everything is built on the operation-log format from day one:
  - Library (create, rename, delete-to-trash) and pages with blank, lined and grid templates.
  - Pen, highlighter, stroke and pixel eraser, lasso move/resize, undo/redo, zoom and scroll, autosave.
  - **Text boxes.**
  - Nested folders, the new-page picker, and the finger-drawing toggle.
  - PDF import, annotation and export.
  - iPad and Mac builds.
- **2 — Sync.** Folder picker, multi-device merge, conflict UI, sync status, trash, daily snapshots, Export all, automatic PDF mirror.
- **3 — Pencil Pro.** Squeeze toggles the eraser, double-tap opens the palette, barrel roll, hover preview, haptics, plus fallbacks. Verify the current APIs in Apple's docs first (`UIPencilInteraction` squeeze, `UITouch.rollAngle`, hover gestures, `UICanvasFeedbackGenerator`).
- **4 — Neatening v1 (deterministic, live line by line, one-tap revert, strength slider).**
  - Start with an on-demand debug mode used for tuning. Then switch on live mode: it triggers when the Pencil moves to a new line, or after about 1.5 s of idle time away from the line.
  - Order: smoothing, then shape snapping (axes snapped exactly horizontal/vertical, arrows, lines, circles, boxes), then straightening each **word** onto the baseline, evening out size per word (cursive can't be split into letters reliably), then evening out slant and the spacing between words.
  - Maths is detected (vertical spread off the baseline, symbol patterns, low recognition confidence) and **skipped**.
  - The result is saved as a `NeatenedVariant` operation, so the other device shows exactly the same result without recomputing it.
- **5 — Search.** Vision recognises text on-device from page renders. The index is a local cache that isn't synced and can be rebuilt. Recognition is used for search only.
- Smart Script being unavailable to third-party apps and AI re-rendering stay out of scope until Luca asks.

## What approving this plan starts
No app code yet. Approval starts only workflow steps 1–3: repo setup, the competitor research, and writing `replica/research.md`. Work then **stops**, and Luca reviews the research and the updated plan and issue outline. Nothing goes on GitHub as an issue, and no code is written, until he approves that.

## Tech stack (the workflow's checklist)
| Layer | Choice |
|---|---|
| Language | Swift 6. SwiftUI for app structure; UIKit + PencilKit for the canvas; PDFKit; Vision |
| Platforms | iPadOS + Mac Catalyst, one app target |
| Database | None. Notebook packages are files (append-only JSONL operation logs). The search index is a local cache |
| Auth / login | None. Personal app, only Luca's own devices |
| Email | None |
| Cloud / VMs | None. No server |
| Object storage | A folder in Luca's iCloud Drive (works without the paid programme). PDFs stored once, named by content hash |
| AI models | On-device only: Vision handwriting recognition, used for search and maths detection. No LLMs in v1 |
| Tests / lint | Swift Testing (NoteCore) + XCTest/XCUITest (app); SwiftLint |
| CI | GitHub Actions on macOS runners (job name `ci`). Public repo, so it's free and merges can be blocked |
| UI testing by Claude | XcodeBuildMCP (replaces Puppeteer from the workflow) |

## Workflow (Robbie's, adapted for a native app)
Order of execution once this plan is approved:
1. `git init`. Create a **public** GitHub repo `lucaclo/<app-name>` with `.gitignore` covering `*.inkbook`, `samples/`, `replica/screens/`, signing files and `xcuserdata`.
2. **Competitor research (deep research + Replica skills, before any code).** Covers GoodNotes plus 5 alternatives: **Notability, Nebo (MyScript), Noteshelf 3, Apple Notes + Math Notes (Smart Script), Concepts**. Focus areas per app:
   - Notability: speed and simplicity.
   - Nebo: handwriting and maths recognition.
   - Noteshelf: pen feel and notebooks.
   - Apple Notes: neatening (Smart Script) and live maths.
   - Concepts: shape and diagram tools.

   Run with the deep-research approach: parallel research subagents, one per app, then a synthesis.
   - `/replica-recon` on each app, core handwriting slice only. Output goes to `replica/<app>/recon.md` + `features.csv`.
   - `/replica-entrepreneur` on each app: real user reviews (App Store, Reddit, forums), quoted and linked. Covers what users love, what they hate, and what's missing.
   - Merge everything into `replica/research.md`: a comparison matrix, the best idea from each app, the UX patterns worth adopting, and the pitfalls to avoid.
   - Each idea is marked must/should/could/skip **for Luca's use** (cursive + maths + diagrams, iPad + Mac, offline, free sync).
   - New features go back into this plan and into the issue outline. Then **stop for Luca's approval.**
   - Later, `/replica-design` builds an original design system informed by the research, and `/replica-diff` scores parity against the merged feature matrix.
   - Not used: `/replica-architect`, `/replica-backend` and `/replica-deploy` (they assume a server/web stack), `/replica-launch` (no App Store launch), `/replica-brand` (already named; any leftover-asset checks are covered by the design sweep).
3. **GoodNotes specifics (part of step 2's research).** This is a feature and flow map only. No name, icons, templates, copy text or code are taken.
   - **Slice:** the core handwriting loop. Library/folders, notebook and page editing, pens/eraser/lasso, templates, PDF import/annotate/export, search, sync, Pencil features. It skips AI, the marketplace, sharing/collaboration, flashcards, audio and typed documents.
   - **Sources:**
     - Public: help centre, App Store listing, changelog, walkthrough videos. Read at human pace, no scraping.
     - **Luca's screenshots** from his own iPad, dropped into `replica/screens/`. These are **gitignored**, because the repo is public and the screenshots are GoodNotes' material.
   - **Outputs:**
     - `replica/recon.md`: screens S01…, flows F01… with click counts, components, inferred data model.
     - `replica/features.csv`: must/should/could/skip, with our decisions applied, e.g. maths-safe neatening and the free iCloud Drive sync.
   - These feed `brainstorm.md` and the issue outline. Recon's click counts become targets in the acceptance criteria (e.g. "new page in ≤ N taps").
   - Only recon from the Replica pack is used, plus `/replica-diff` later for a parity score. `/replica-architect`, `/replica-backend` and `/replica-deploy` assume a server/SQL web stack, which this app deliberately doesn't have.
3. Write the setup docs:
   - `brainstorm.md`: the full project spec prompt, i.e. the original spec plus every decision in this plan.
   - `PLAN.md` and `NOTES.md`.
   - A **lean** `CLAUDE.md` with build/test commands, hard rules and conventions, under about 60 lines. Written by hand, because `/init` has nothing to scan in an empty repo; it can be refreshed with `/init` once code exists.
4. Create `.claude/commands/process-issue.md` (`/process-issue <n>`), Robbie's PLAN → CREATE → TEST → DEPLOY loop adapted as follows:
   - Scratchpads go in `scratchpads/<issue#>-<slug>.md`.
   - One branch per issue. One logical change per commit, referencing `#n`, with a push after every commit.
   - Tests use Swift Testing/XCTest instead of rspec. UI checks use XcodeBuildMCP instead of Puppeteer.
   - Run the full test suite and SwiftLint before opening the PR. The PR body ends with the honest report: built, tested, untested, risks, and **manual iPad checks for Luca**.
5. **Propose the issue outline (below, refined with recon) and stop for Luca's approval.** Only after approval: `gh issue create` one issue at a time, using the five required sections (Goal, Acceptance Criteria 3–7, Implementation Notes, Dependencies, Out of Scope), then `gh issue list`.
6. Branch protection on `main` requires the `ci` check. Luca does this by hand (steps in `NOTES.md`) once CI has run at least once, because the check can't be selected before then. Note: GitHub doesn't let you approve your own PR, so "approve" means: check that CI is green, then merge.
7. The loop: `/process-issue n` → PR → CI green → Luca merges → `/clear` → next issue.

### Issue outline (v3, quality-checked; deps in brackets)
Each line = one atomic issue. Full five-section bodies are written at creation time.

**Setup**
1. Set up the test suite (Xcode project, NoteCore package, Swift Testing + XCTest) [—]
2. Set up CI via GitHub Actions (job `ci`: tests + SwiftLint, blocks merge) [1]
3. Set up XcodeBuildMCP for simulator UI testing [1]
4. Spike: verify iCloud Drive folder sync + Auto-refine risk on iPad and Mac [1]

**Core model (NoteCore)**
5. Add Stroke and StrokePoint model with JSON codec [1]
6. Add Page model (paper type, PDF background, size) [5]
7. Add Notebook model with fractional page order [6]
8. Add Folder tree model [7]
9. Add operation types and per-device append-only log [5,6,7]
10. Add version-vector merge of device logs [9]
11. Add concurrent-edit conflict detection (keep both) [10]
12. Add notebook package FileStore (per-page files, atomic coordinated writes) [9]
13. Add read-only fallback for damaged or newer-format notebooks [12]

**MVP UI**
14. Add library folder tree screen [8,12]
15. Add create/rename/move for notebooks and folders [14]
16. Add delete-to-Trash for notebooks [15]
17. Add PencilKit canvas with PKStroke↔Stroke conversion [5]
18. Add ballpoint rendering: render-time smoothing, pressure clamp, display-only prediction [17]
19. Add autosave on pen-up and reload on open [12,17]
20. Add vertical page scroll and zoom with virtualised pages [19]
21. Add paper chips at page foot with last-used default [20]
22. Add change-paper for an existing page [21]
23. Restore last page, offset and zoom on reopen [20]
24. Add top toolbar with 3 pen and 2 highlighter presets [17]
25. Add long-press preset editing (colour, width) [24]
26. Render highlighter strokes behind ink [24]
27. Snap highlighter strokes straight [26]
28. Add stroke eraser [19]
29. Add pixel eraser via replaceStroke [28]
30. Add lasso select, move and resize (width preserved) [19]
31. Add tap-to-select a single stroke [30]
32. Add grouping of selected strokes [30]
33. Add operation-based undo/redo with top-left undo button [19,24]
34. Add two-finger-tap undo and three-finger-tap redo [33]
35. Add finger-drawing toggle (off by default) [17]
36. Add text boxes that snap to ruled lines [19,21]
37. Add page sidebar with thumbnails and drag-reorder [20]
38. Add multi-select page actions in sidebar [37]
39. Add page bookmarks with bookmark filter [37]
40. Add outline view incl. PDF table of contents [39]
41. Add PDF import as a new notebook [20]
42. Add PDF insert at position into an existing notebook [41]
43. Add insert blank page between pages [41]
44. Add vector PDF export matching screen [41]
45. Enable Mac Catalyst build with trackpad/mouse inking [19]
46. Add Mac sidebar + page window layout [45,14]
47. Add Mac keyboard shortcuts [46]

**Sync**
48. Add sync folder picker with security-scoped bookmark [4,12]
49. Keep sync folder downloaded and open from local data [48]
50. Detect remote changes and merge them live [49,11]
51. Add honest per-notebook sync status indicator [50]
52. Add conflict badge and resolve UI [50]
53. Add page-level Trash with 30-day purge [50,16]
54. Add daily local snapshots (30 days) [50]
55. Add Export all (zip + PDFs) [44]
56. Add automatic PDF mirror in sync folder [44,50]

**Pencil Pro**
57. Add squeeze: tap toggles eraser, hold = temporary eraser (in-app setting) [28]
58. Add double-tap palette at pen tip [24]
59. Add hover tool preview [24]
60. Add Pencil Pro haptics [57]
61. Add barrel roll for highlighter chisel [26]

**Shapes (Phase 4a, right after MVP)**
62. Add ShapeInterpretation model stored beside raw strokes [9]
63. Add hold-to-snap recognition (line, axes, arrow, circle, ellipse, rectangle, curve) [62,19]
64. Add show-original chip and snap-only undo [63]
65. Add per-shape-type and master snapping toggles [63]
66. Add angle snapping (±5°) [63]
67. Add endpoint joining with target dot [63]

**Neatening (Phase 4b)**
68. Add NeatenedVariant model and per-line revert [9]
69. Add smoothing transform for neatened layer [68]
70. Add line and word segmentation [68]
71. Add maths detection with fraction-bar protection [70]
72. Add leave-alone region marker [68]
73. Add baseline straightening [70,71]
74. Add per-word size evening [73]
75. Add slant and word-spacing evening [73]
76. Add live line-by-line neatening trigger [74,75]
77. Add global neatening switch and strength slider [76]

**Gestures**
78. Add scratch-out-and-hold to erase (opt-in) [28,71]
79. Add insert-space gesture [30]

**Search**
80. Add background handwriting index with PKStrokeRecognizer [12,19]
81. Add PDF text extraction for search [41,80]
82. Add search UI that opens the exact page [80,81]
83. Embed recognised text in exported PDFs [44,80]

**After MVP (not yet issues):** tabs / split view, more templates.

## Critical files (to be created)
- `PLAN.md`: this plan, plus decisions and open questions.
- `NOTES.md`: manual steps for Luca (see below).
- `NoteCore/Sources/NoteCore/{Model,Ops,Merge,FileStore,Neatening,Search}/…` and `NoteCore/Tests/…`
- `Inkwell/{App,Library,Canvas,PDF,Sync,Pencil}/…`
- `.gitignore`, which excludes any `*.inkbook`, sample notes and signing files.

## Verification
- **Automated tests (NoteCore):**
  - Encode/decode round-trips and golden-file tests for the format.
  - **Merge property tests:** random interleavings of operations from 2–3 simulated devices, including dropped or delayed log segments, must converge on every device with no lost strokes and with conflicts flagged.
  - Every neatening transform is checked for these properties:
    - its input is unchanged
    - it's deterministic
    - reverting gives back the exact raw stroke
    - maths gets skipped
- **Simulator and Mac:** `xcodebuild test` plus a few XCUITests (create notebook → draw → relaunch → strokes still there).
- **Manual on the iPad** (exact steps in `NOTES.md`):
  - Latency and pressure feel.
  - Pencil Pro gestures.
  - The **two-device offline test**: put both devices in airplane mode, edit the same page on each, reconnect, check that every stroke is present and conflicts are flagged.
  - The 7-day reinstall, checking notes survive.
  - Opening a large PDF.

## NOTES.md: Luca's manual steps
1. Install Xcode from the App Store, open it, add the iOS platform, then run `sudo xcode-select -s /Applications/Xcode.app`.
2. In Xcode → Settings → Accounts, add your Apple ID. This gives you the free Personal Team.
3. On the iPad: connect it by USB-C, turn on Developer Mode (Settings → Privacy & Security), and trust the developer certificate (Settings → General → VPN & Device Management).
4. **Every week:** plug in, press Run in Xcode, and the app is re-signed. **Never delete the app** from the iPad.
5. Create the folder `iCloud Drive/Notes` and make sure it's kept downloaded on the Mac. Turn on Advanced Data Protection.

## Open questions (non-blocking; defaults in brackets)
- **Deployment target: iPadOS 27 + macOS 27 (decided).** Luca updates both devices.
- Largest PDF to support [design for 300 pages].
- Install **XcodeBuildMCP** so I can drive the simulator myself [yes].
- Repo: public `lucaclo/inkwell` (decided).
