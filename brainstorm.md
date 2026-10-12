# Inkwell: project spec (brainstorm output)

This is the complete spec for planning and issue creation. Decisions and their reasons are in `PLAN.md`. The evidence behind the product choices is in `replica/research.md`.

## What it is
A personal (not App Store) handwritten note-taking app for Luca's **iPad Pro (M4/M5) with Apple Pencil Pro**, also running on his **Mac (M5, macOS 26)** as a Mac Catalyst app. It's in the same category as GoodNotes and Notability, but nothing is copied from them. He uses it every day for university (economics) and work. **Reliability, and never losing or altering his writing, matter more than features.** He writes in English, in cursive, with a lot of maths notation and economics diagrams.

## Non-negotiable rules
1. **Original ink is never destroyed.** Raw strokes are always stored. Neatening and shape snapping are separate, reversible layers that can be toggled per line, group or page. Erasing is a real edit, recoverable from undo and from page history.
2. **Neatening never changes what was written.** Allowed: smoothing, straightening onto the baseline, evening out size, slant and spacing per word, and snapping shapes. Letters are never regenerated. Maths, diagrams and anything uncertain are skipped.
3. **Sync never loses data.** Concurrent offline edits never silently overwrite each other. When in doubt, keep both versions and let Luca choose.
4. **Everything is on-device.** No server, account, analytics or network calls. Notes leave his devices only through his own iCloud Drive.
5. **Nothing is taken from other apps:** no names, icons, templates, UI assets or copy.
6. **Apple APIs are checked against the current official docs** before being relied on, and anything uncertain is said out loud.
7. **Every smart behaviour can be switched off. Nothing pops up over the canvas. Tools and gestures stay put between versions.**

## Constraints
- **Free Apple Personal Team** (no $99 programme). The iPad build must be reinstalled from Xcode every 7 days, and the iCloud/CloudKit entitlement isn't available.
- **Sync** goes through a user-picked folder in iCloud Drive (a security-scoped bookmark), on both iPad and Mac.
- Luca isn't an experienced iOS developer. Every manual step goes in `NOTES.md`.

## Tech stack
- **Language and frameworks:** Swift 6. SwiftUI shell; UIKit + PencilKit canvas; PDFKit; Vision for on-device recognition.
- **OS:** iPadOS 27 and macOS 27 minimum, which gives `PKStrokeRecognizer` for search.
- **Targets:** one app target for iPadOS + Mac Catalyst, plus a UI-free Swift package `NoteCore` (model, op log, merge, file store, neatening, search).
- **Storage:** no database or backend. Each notebook is a package of per-device, append-only JSONL operation logs plus PDF assets named by content hash.
- **Testing and CI:** Swift Testing / XCTest / XCUITest, SwiftLint, GitHub Actions (job `ci`) on macOS runners. The repo is public.
- **UI testing by Claude:** XcodeBuildMCP.

## Data model and sync
- **Entities:**
  - `Notebook`: id, title, createdAt, page order using fractional keys.
  - `Folder`: a nested tree.
  - `Page`: paper (lined, grid or blank), optional PDF background, size shaped like the iPad screen.
  - `Stroke`: id, tool, colour, width, points (x, y, t, force, azimuth, altitude, roll); immutable.
  - `TextBox`.
  - `NeatenedVariant` and `ShapeInterpretation`: stored alongside the raw strokes.
- **Operations:** add, replace (partial erase), transform, delete (tombstone), page add/reorder, rename, neaten/revert, snap/revert. Each carries (deviceID, seq, version vector).
- **One rule makes sync safe:** each device writes only `devices/<deviceID>/`. No file is ever written by two devices, so iCloud can't create conflict copies.
- **Merging:** adds always merge. Concurrent edits to the same object keep both versions and set a conflict badge. When a delete and an edit happen concurrently, the edit wins.
- **Reliability:**
  - Each stroke is saved the moment the pen lifts. Writes are atomic and coordinated.
  - A damaged or newer-format notebook opens read-only and is never refused.
  - The sync folder is kept downloaded, and the app always opens from local data.
  - Sync status is shown honestly.
- **Recovery:**
  - 30-day Trash for notebooks and pages.
  - Daily local snapshots, kept 30 days.
  - "Export all" button.
  - An automatic read-only PDF mirror of every notebook in the sync folder.

## Product decisions
- **Library:** nested folders. On the Mac, a sidebar plus the page, with standard shortcuts.
- **Pages:** vertical scroll; pages separate and shaped like the iPad screen.
  - New pages show lined/grid/blank chips at the foot, defaulting to the last paper used.
  - The page sidebar has thumbnails, reordering, multi-select, bookmarks and an outline (including the PDF's own table of contents).
  - Reopening a notebook returns to the last page, position and zoom.
- **Tools:**
  - A slim top bar with 3 ballpoint pens and 2 highlighters, each a preset. Long-press a preset to edit it. Undo sits at the top-left.
  - Highlighter ink sits behind the writing and snaps straight.
  - Erasing: stroke and pixel eraser.
  - Lasso: scaling keeps line width. Tap selects a single stroke. Selections can be grouped.
  - Text boxes that sit on the ruled lines.
  - The finger-drawing toggle is off by default.
- **Ink quality:** smoothing is applied only when drawing, set per pen. Pressure is limited to about 0.6–1.4× width. Predicted touches are never saved.
- **Gestures:** two-finger tap undoes, three-finger tap redoes. Scratch-out to erase is opt-in. Insert space with a two-finger long-press and drag.
- **Pencil Pro:**
  - A quick squeeze toggles the eraser; squeeze-and-hold is a temporary eraser.
  - Double-tap opens a palette at the pen tip.
  - Hover preview, haptics.
  - Barrel roll rotates the highlighter's flat tip.
- **PDF:**
  - Import a PDF as a new notebook, or insert it into an existing notebook at a chosen position.
  - Blank pages between slides.
  - Export as a vector PDF that matches the screen, with the recognised text embedded.
- **Shapes (right after the MVP):**
  - Hold the pen still for about 0.5 s to snap a line, axes, arrow, circle, ellipse, rectangle or curve.
  - Angle snapping (±5°) and endpoint joining (about 12 pt).
  - A "show original" chip appears after a snap, and the first undo reverts only the snap.
  - Each shape type has its own toggle, plus a master switch.
- **Neatening:**
  - Live and line by line, run only after the pen has moved on.
  - One global switch, and a strength slider set to gentle by default.
  - Order: smoothing, then baseline straightening, then evening out size, slant and spacing per word.
  - Maths is detected and skipped, with fraction bars protected. A "leave alone" region marker. One-tap revert for each line.
- **Search:** Vision recognises text silently in the background. One search box covers handwriting, typed text, PDF text and titles, and opens the exact page.
- **After the MVP:** tabs / split view, more templates.

## Delivery
- Build a thin working slice first, then iterate.
- The issue outline is in `PLAN.md`. Order: #1 test suite, #2 CI, #3 XcodeBuildMCP, #4 sync spike, then the remaining issues in dependency order.
- **MVP is done when** Luca can:
  - install the app on his iPad
  - write smoothly with the Pencil
  - organise notebooks in folders
  - annotate a PDF
  - close and reopen the app with everything intact
  - see the same notebook on the Mac after sync, with no lost strokes in a two-device offline edit test
