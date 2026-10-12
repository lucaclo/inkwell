# Inkwell competitor research: synthesis

Date: 2026-10-12. Apps: GoodNotes 6/7, Notability, Nebo (now "MyScript Notes"), Noteshelf 3, Concepts, Apple Notes (Smart Script / Math Notes).
Per-app detail: `replica/<app>/recon.md`, `features.csv`, `reviews.csv`, `feedback.md` and `fixes.md`.

**Sample:** 3,034 real reviews and comments.

| App | Items | Sources |
| --- | --- | --- |
| GoodNotes | 553 | App Store US+GB, HN, Trustpilot, feature board |
| Notability | 540 | App Store US+GB, HN, Trustpilot |
| Nebo | 629 | App Store US+GB, HN, forums |
| Noteshelf 3 | 396 | App Store US+GB, Google Play, HN |
| Concepts | 916 | App Store US+GB, HN, Google Play |

Every quote is verbatim and linked in the per-app `fixes.md`.

**Gaps:**
- **Reddit:** blocked for all researchers, so it isn't represented.
- **Tap counts:** inferred from help centres, not timed on a device.
- **Theme counts:** keyword matches, so treat them as estimates.

App Store feeds are "most recent first", so samples lean toward recent controversies (Notability's cloud move, the GoodNotes 2025 redesign, Nebo's subscription).

---

## 1. The big picture

1. **Losing notes is the #1 complaint in every app.**
   - Notability: about 50 "notes vanished" reviews after its forced move to its own cloud.
   - GoodNotes: about 30 on vanishing or resurrected ink and sync.
   - Noteshelf: 18 crash-lost-work and 14 "won't open" reviews.
   - Concepts: 77 on sync and data.
   - Nebo: 10 on lost work, plus "conflicted copies".

   Inkwell's architecture (append-only per-device logs, keep-both conflicts, snapshots, PDF mirror, no account) targets exactly this. Reliability *is* the differentiator.
2. **"Smart" features users can't control are the #2 source of anger.** Nebo has at least 24 reviews about maths and graphs being "corrected" (fraction bars snapped, graph boxes adjusted). Concepts and GoodNotes get complaints about shape snapping firing on natural pauses. Every intelligent behaviour in Inkwell must be:
   - deliberate or gated
   - toggleable
   - kept away from maths
   - reversible
3. **Changing the UI in updates is punished hard.**
   - GoodNotes: a 640-vote "revert the toolbar" request, and a 543-vote request about it auto-switching to the lasso.
   - Notability: users were angry when the squeeze eraser and one-finger scroll were removed.

   Inkwell's gestures and toolbar get frozen once they're settled.
4. **Nobody does reversible neatening.**
   - GoodNotes has only a manual "straighten and reflow" (a 452-vote board request asks for better).
   - Nebo's beautification is destructive.
   - Concepts can't turn a snapped shape back into the freehand stroke.

   Inkwell's raw-ink-plus-reversible-layer model is genuinely new.
5. **Account, AI and subscription bloat drives users away** (Notability, Nebo, GoodNotes). Inkwell has none of these by design. Keep it that way: no pop-ups, upsells or prompts over the canvas.

---

## 2. Consensus patterns: in 3 or more apps and praised by users

| # | Pattern | Seen in | Priority | Inkwell version |
| --- | --- | --- | --- | --- |
| P1 | **Hold-to-snap shapes** | All 5 | must | Hold the pen still for about 0.5 s (stillness about 2 pt) at the end of a stroke and it snaps. Before you lift, moving the pen scales and rotates the shape. A haptic tick on Pencil Pro. Types: line, axes (L), arrow, circle, ellipse, rectangle, smooth curve. A toggle per type plus a master switch. **The raw stroke is kept**, with a "show original" chip for about 3 s, and the first undo reverts only the snap. |
| P2 | **Angle and endpoint snapping** | Concepts, GN, Notability | must | Lines within ±5° lock to horizontal or vertical (and 45° on grid pages). An endpoint within about 12 pt joins the nearest endpoint or axis, with a target dot shown before you lift. Gives clean supply and demand diagrams. |
| P3 | **Two-finger tap undo, three-finger tap redo** | All 5 | must | 0 taps. After the first two-finger tap, single taps repeat the undo (a GoodNotes board idea). Has an off switch. Also an undo button at the **top-left**, for the non-writing hand (Noteshelf). |
| P4 | **Palette at the pen tip** | GN, Nebo, Noteshelf | must | Double-tap opens it at the hover or last-touch point, and it closes on your next stroke. |
| P5 | **Precise, unsmoothed ink with distinct nibs** | Noteshelf (top praise), Nebo, GN pitfall | must | Smoothing is a setting on each pen, applied **when drawing to screen, never baked into the saved points**. Predicted touches only ever appear on screen. Pressure-to-width is limited to about 0.6–1.4×. Nib types: ball, felt, fountain (suits cursive). |
| P6 | **Paper chosen as you add the page, defaulting to the last one used** | GN, Notability, Noteshelf | must | Instead of a picker sheet: small lined, grid and blank chips at the foot of a fresh page, defaulting to the last paper used, disappearing when you first write. 0 taps in the common case. "Change paper" can be done later on any page. |
| P7 | **Sidebar page manager** | GN, Noteshelf | must | Thumbnails, drag to reorder, multi-select, a filter for bookmarked pages, and an outline that imports the PDF's own table of contents. |
| P8 | **One search box for everything** | GN, Notability, Nebo | must | Handwriting, typed text, the PDF's text, titles and bookmarks. Opens the exact page. Recognition runs **silently** with no pop-ups. Exported PDFs include the recognised text, so they stay searchable outside Inkwell. |
| P9 | **PDF workflow for lectures** | Notability, GN, Noteshelf | must | Import into the current notebook at a chosen position. Option to add blank margin space beside each slide. Insert blank pages between slides. Drag and drop on Mac. Render PDF pages sharply at screen resolution, and export from the same stroke data so exports match the screen. |
| P10 | **Recovery net** | Notability, Noteshelf, Nebo pitfall | must | 30-day Trash for notebooks **and pages**. History follows the notebook ID, never its name (Notability wipes history on rename). Backups never copy deletions. |
| P11 | **Lasso: circle, move, resize** | All | must | Selects whole strokes by default. Scaling keeps stroke width. Groups a diagram so it moves as one. **Tap a single stroke to select it.** Never picks up erased fragments. |
| P12 | **Reopen where you left off** | Noteshelf pitfall | must | Each notebook remembers its last page, position and zoom. |

## 3. Distinctive ideas worth taking (one app each)

| Idea | From | Priority | Notes |
| --- | --- | --- | --- |
| Scratch-out to erase (scribble over ink) | Nebo (its most-loved gesture), asked for in Notability | should, **opt-in** | It risks conflicting with cursive. Require at least 3 direction reversals that are dense and over existing ink. Never in maths regions. The erased ink fades out and can be undone. **Question for Luca.** |
| Insert space: two-finger long-press, then drag | Nebo | should | Moves everything below a line down or up. A reversible move of the ink, not a reflow. Great when you need room mid-lecture. |
| Save selection as a reusable stamp | Noteshelf | should | E.g. a blank supply/demand axis set. |
| Ink flows across page breaks in vertical scroll | Notability (its signature feature) | could | Makes pages feel like a seamless scroll; pages still export at a fixed size. Complex for strokes that cross a page break. **Question.** |
| Temporary eraser while holding squeeze | Notability, Nebo | should | Quick squeeze toggles the eraser on and off (your choice); squeeze-and-hold is a temporary eraser, and letting go returns to the pen. **Question.** |
| Optional live recognition preview | Nebo | could | Faint text above the line you just finished, confirming search will find it. |
| Zoom box for dense maths | Noteshelf, GN | could | Write large in a magnified strip at the bottom, and it appears small on the page. |
| Focus mode / read-only PDFs until the Pencil touches | Noteshelf | could | Full-screen paper for lectures. |
| Per-page history scrubber | Concepts (older versions) | could | Cheap, because Inkwell stores operations. |
| Recognition word list (oligopoly, Cobb-Douglas…) | Nebo | could | Fixes recognition mistakes for search. |
| Split view via an edge swipe | Notability | should | Already planned post-MVP (tabs/split). |
| Mac at full parity | All (pitfall) | must | Undo, shortcuts, stable scroll position, keyboard and pointer from day one. |

## 4. Pitfalls → rules for Inkwell

1. Never switch tools on the user's behalf, and never move or reorder the toolbar between versions.
2. Never lose or resurrect ink. Save every stroke when the pen lifts; one file per page; a damaged or newer-format notebook opens **read-only** rather than being refused.
3. Never depend on iCloud offloading files. Keep the sync folder downloaded, open from local data instantly, sync in the background, and be honest about sync state (never a false "failed", never silently show a notebook with pages missing).
4. Every smart behaviour gets an off switch. Snapping off means exactly the raw stroke, with no residual pull.
5. Maths and graphs are protected by default. Never touch a long horizontal stroke with ink above and below it (fraction bars). Add a one-gesture "leave this alone" region marker.
6. Nothing ever pops up over the canvas: no menus, downloads, spell-check dots or prompts.
7. Performance stays flat on 300+ page PDFs: only build the pages in view, tile rendering, keep live ink on its own layer.
8. Names aren't IDs. Duplicate names are allowed across folders, and renaming never resets history.
9. Typed text in text boxes snaps to the ruled lines and lays out identically on iPad and Mac.
10. Keep storage small: compact deleted data, and show the library size.

## 5. Apple Notes and platform APIs (detail in `apple-notes/apis.md`, checked against Apple docs)
**Apple Notes users:** 105 items (Apple Community, MacRumors, HN, MacStories).
- **Liked:** refinement that is "subtle, but nice"; scratch-out-and-hold to erase (the hold at the end stops cursive being erased by accident); draw-and-pause to snap.
- **Hated:** Smart Script changing what was written (wrong words, words jumping off the line, noticed "long after", no way back); spell-check dots on handwriting; writing "=" triggering maths; lag after 4–5 pages.

**The current OS is iPadOS / macOS 27.**

| Capability | Available to Inkwell? | Min OS |
| --- | --- | --- |
| Smart Script refine, straighten or spell-correct | **No public API.** Build our own as reversible transforms (planned) | — |
| Shape recognition | **No API.** Build our own; Pencil Pro haptic via `UICanvasFeedbackGenerator.pathCompleted` | 17.5 |
| Maths recognition | **No API** (neither Vision nor PencilKit). Needs our own heuristic classifier (planned) | — |
| Handwriting recognition and search | **Yes: `PKStrokeRecognizer`**, on-device and the same tech as Notes. Returns stroke IDs and bounds, works with Find UI and Spotlight | **27** |
| Squeeze, double-tap, hover, barrel roll, Pencil Pro haptics | Yes | 17.5 |
| Stable stroke IDs, selection API, substroke slicing | Yes | 27 (we keep our own UUIDs anyway) |
| PaperKit (text boxes/shapes) | iPad yes, **Mac Catalyst not listed**, so don't use it; build our own text boxes | 26 |
| iCloud container | **Not on a free account (confirmed)**. Our user-picked folder approach is the right one | — |

**Plan impacts:**
1. **Risk to test in the sync spike:** the system "Auto-refine handwriting" toggle may show up in third-party PencilKit canvases. If it's on, iOS would alter Inkwell's ink. The spike must check this on the iPad. If present, Inkwell detects it and warns, or uses a canvas setup that avoids it.
2. **Search:** use `PKStrokeRecognizer` (iPadOS/macOS 27). Store `recognitionVersion` and re-index when it changes. Use Vision OCR only for the PDF's own text.
3. **Squeeze is a system preference** (`preferredSqueezeAction`). Inkwell adds an in-app setting "Squeeze toggles eraser", on by default.
4. **Barrel roll** affects only the highlighter (Notes users asked how to turn it off for ballpoints).
5. **Scratch-out:** require a short hold at the end (Apple's approach), on top of the zig-zag check. Safer for cursive.
6. **Deployment target:** iPadOS 27 gives the recogniser. One Catalyst target means **the Mac also needs macOS 27** (Luca's Mac is on 26.6.2). See the open question.

## 6. Proposed changes to the plan (pending Luca's approval)

| Area | Change | Phase | Issue impact |
| --- | --- | --- | --- |
| Pens | Smoothing applied when drawing, per pen; pressure limits; fountain nib; predicted points never saved | 1 | expands #14/#18 |
| Gestures | Two/three-finger tap undo/redo + repeat; undo button top-left | 1 | new issue |
| Pages | Paper chips at the page foot, defaulting to the last used, instead of a picker sheet | 1 | changes #17 |
| Navigation | Sidebar of page thumbnails + bookmarks + PDF outline; reopen at last position | 1 | 2 new issues |
| PDF | Insert at position, blank pages between slides, optional margins, Mac drag and drop | 1 | splits #25 |
| Lasso | Tap to select one stroke, grouping, scaling keeps width | 1 | expands #21 |
| Recovery | Page-level Trash; history keyed by ID | 2 | expands #32 |
| Sync | Keep folder downloaded, open from local data, honest status, read-only fallback | 2 | expands #29/#30 |
| Diagrams | Hold-to-snap (P1) and angle/endpoint snapping (P2) move **earlier**, to just after the MVP, as their own issues, separate from text neatening | 4a | splits #45 |
| Neatening | Protect fraction bars; "leave alone" region marker; every behaviour toggleable | 4 | new issue |
| Extras | Insert-space gesture, save-as-stamp, scratch-out (opt-in) | 4+ | new issues |
| Search | Recognised text embedded in exported PDFs; word list | 5 | expands #48 |

## 7. Luca's decisions on the research (2026-10-12)
- **Scratch-out to erase:** yes, **opt-in** (off by default). Needs a dense zig-zag over existing ink, never fires in maths, fades out and can be undone.
- **Squeeze:** a quick squeeze toggles pen ↔ eraser **and** squeeze-and-hold gives a temporary eraser (release returns to the pen).
- **New-page paper:** lined, grid and blank chips at the foot of each fresh page, defaulting to the last paper used. Paper can be changed later on any page.
- **Page breaks:** pages stay separate (no ink flowing across the break). A new page appears when you scroll past the end.
- **Hold-to-snap shapes and angle/endpoint snapping:** moved to a phase **right after the MVP**, ahead of text neatening.
- **Extras planned:** the insert-space gesture only. Save-as-stamp, zoom box and the history scrubber are not planned for now.
- **Nibs:** ballpoint only. The 3 pens are ballpoint presets that differ by colour and width.
- **OS:** update both devices to version 27; deployment target iPadOS 27 / macOS 27.
