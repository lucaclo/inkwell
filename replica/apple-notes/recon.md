# Recon map: Apple Notes with Smart Script and Math Notes (iPadOS / macOS)

Scope: the handwriting slice of Notes. That covers the Markup canvas inside a note, Smart Script (refine, straighten, spell-check, paste as handwriting, scratch-to-erase, insert space), Math Notes (inline solving, variables, graphs), shape snapping, the ruler, the PencilKit tool picker, Apple Pencil Pro gestures, handwriting search, attachments/PDF, export and iCloud sync. It leaves out the typed-text features of Notes (checklists, tables, tags, collaboration, Quick Note, audio transcription).
For: Inkwell, Luca's personal handwritten-notes app (iPad Pro M4/M5 + Apple Pencil Pro, Mac Catalyst). It is not for sale, and Notes is a reference here, not a clone target.
Date: 2026-10-12

**Version note:** the brief asked for "iPadOS 26". As of today, Apple's iPad User Guide and developer docs already cover **iPadOS 27**, and the iPad guide pages cited below are the `/27/ipados/27` versions. I found no Notes handwriting features documented as new in 27; the "What's new in iPadOS 27" page doesn't mention Notes handwriting. The big change in 27 is on the developer side: public PencilKit handwriting recognition (see `apis.md`).

## Sources

| # | source | URL | notes |
| --- | --- | --- | --- |
| 1 | iPad User Guide: Add drawings and handwriting in Notes (iPadOS 27) | https://support.apple.com/guide/ipad/add-drawings-and-handwriting-ipada87a6078/ipados | Smart Selection gestures, Refine, Straighten, spell-correct, paste/convert to handwriting (needs ≥10 unique lowercase characters already saved), scratch-and-hold erase |
| 2 | Apple Support: Use handwriting in Notes on your iPad (published 2025-06-09) | https://support.apple.com/en-us/121259 | Auto-refine toggle path, refine slider, paste-as-handwriting prerequisites |
| 3 | iPad User Guide: Draw and handwrite with Markup | https://support.apple.com/guide/ipad/draw-and-handwrite-with-markup-ipad6350b8dc/27/ipados/27 | toolbar move/auto-minimize, line weight, opacity, colour (Grid/Spectrum/Sliders), ruler (two-finger rotate), lasso, double/triple-tap selection, Copy as Text / Translate / Straighten, pixel vs object eraser |
| 4 | iPad User Guide: Add text, shapes, stickers with Markup | https://support.apple.com/guide/ipad/add-text-shapes-stickers-and-more-with-markup-ipad8869ac3a/27/ipados/27 | draw a shape in one stroke then pause, and it snaps. The list of shapes. Undo keeps the freehand version |
| 5 | iPad User Guide: Draw with Apple Pencil | https://support.apple.com/guide/ipad/draw-with-apple-pencil-ipadc55b6c7a/27/ipados/27 | double-tap, squeeze, barrel roll (fountain pen and highlighter), haptics toggle, hover up to 12 mm, hover preview of highlighter/eraser |
| 6 | iPad User Guide: Accessibility double tap and squeeze | https://support.apple.com/guide/ipad/adjust-double-tap-squeeze-settings-apple-ipad63913965/27/ipados/27 | squeeze firmness slider, Extended Range, double-tap duration |
| 7 | iPad User Guide: Enter formulas and equations in Notes | https://support.apple.com/guide/ipad/enter-formulas-and-equations-ipad10f28bec/27/ipados/27 | solving is triggered by "=", plus stacked columns with a line under them. Red dotted = error, blue dotted = ambiguous character. Insert Graph |
| 8 | iPad User Guide: Solve math with Math Notes | https://support.apple.com/guide/ipad/solve-math-with-math-notes-ipadeb38d0f8/27/ipados/27 | variables (Latin letters only, declare before use), units/currency, scrubber on numbers (Pencil hover too), Insert/Suggest/Off results, light background |
| 9 | iPad User Guide: Work with graphs in Math Notes | https://support.apple.com/guide/ipad/work-with-graphs-in-math-notes-ipad7dfe4006/27/ipados/27 | 2D/3D graphs, pan/zoom, trace coordinates, equalize axes, recentre, multiple equations per graph |
| 10 | iPad User Guide: Change Notes settings | https://support.apple.com/guide/ipad/change-notes-settings-ipaddf4ef746/27/ipados/27 | lines and grids, "On My iPad" account, sort, Lock Screen access |
| 11 | iPad User Guide: Add photos, video and more | https://support.apple.com/guide/ipad/add-photos-video-and-more-ipad48c80318/27/ipados/27 | attachments incl. PDFs from Files, attachment view size |
| 12 | iPad User Guide: Export or print notes | https://support.apple.com/guide/ipad/export-or-print-notes-ipad50c393a8/27/ipados/27 | PDF export via Markup. **A note with a multipage PDF exports only the first page.** Markdown export, Open in Pages (drawings not editable) |
| 13 | iPad User Guide: What's new in iPadOS 27 | https://support.apple.com/guide/ipad/whats-new-in-ipados-27-ipad8d9d296d/27/ipados/27 | no Notes-handwriting items |
| 14 | Apple developer docs + WWDC sessions (see `apis.md`) | https://developer.apple.com/documentation/pencilkit | what's public vs Apple-only |
| 15 | MacStories hands-on review of Smart Script (2024-08-29) | https://www.macstories.net/stories/ipados-18s-smart-script-a-promising-start-but-dont-toss-your-keyboard-out-yet/ | real-world behaviour: refine animates in after a line or two, input briefly dropped while refining, reflow issues |
| 16 | User reports (Apple Support Community, MacRumors, HN) | see `reviews.csv` | behaviour as users see it |

I didn't use the user's own account, and I saved no screenshots.

## Core loop

Open a note, write with the Pencil, and let the system quietly tidy, check and compute the writing. Then find it again later by searching the handwriting.

## Screens

| ID | screen | route / how to reach | purpose | key components | states seen (documented) |
| --- | --- | --- | --- | --- | --- |
| S01 | Folders sidebar | launch / back from list | accounts (iCloud, On My iPad), folders, Smart Folders, special "Math Notes" folder | sidebar list, new-folder button | empty, filled, locked notes |
| S02 | Notes list | tap folder | browse/sort/group notes. First handwritten line becomes the suggested title | list or gallery, search field, "View Attachments" | empty, filled, search results |
| S03 | Note editor, typed mode | tap a note / new note | mixed typed text, attachments and inline drawing areas | formatting bar, attachment button (paperclip), Markup button, More (…) menu | empty, filled, locked |
| S04 | Note editor, Markup/handwriting mode | start writing with Pencil or tap Markup | handwriting canvas embedded in the note. The drawing area has a resize handle on the left | tool picker (S05), canvas, resize handle | blank, lines/grid background, zoomed |
| S05 | Tool picker (docked) | visible in Markup mode | choose pen/marker/pencil/monoline/fountain pen/crayon/watercolour/reed (varies), eraser, lasso, ruler, colours. Includes "More" menu | tool wells, colour swatches, colour picker sheet, More (…) | docked, draggable to any edge, auto-minimized, hidden |
| S06 | Tool options popover | tap the selected tool | line weight (preset widths), opacity slider, eraser type (pixel/object) | width chips, slider | per tool |
| S07 | More menu (tool picker) | tool picker "…" | Auto-refine Handwriting toggle, Auto-minimize, finger drawing, (iPadOS 26+) handwriting spell-check toggle per user reports | toggles | on/off, "will download when connected to Wi-Fi" message |
| S08 | Squeeze palette (contextual mini palette) | squeeze Apple Pencil Pro (if Settings, Squeeze = Show Tool Palette) | radial/compact palette under the Pencil tip: recent tools, colours, undo/redo | palette, hover highlight, haptic tick | shown/dismissed. User reports say it can show only undo/redo in some apps |
| S09 | Selection edit menu | lasso / double-tap word / triple-tap sentence / touch-hold-drag | act on handwriting: Cut, Copy, Delete, Duplicate, Copy as Text, Translate, Straighten, Refine (slider), Insert Space Above | callout menu, selection handles, refine slider | word, sentence, paragraph, mixed with drawing |
| S10 | Spell-check suggestion menu | tap blue-dotted handwritten word | replace with a suggestion rendered in the user's handwriting | suggestion list | shown. User reports say it often suggests unrelated words |
| S11 | Paste/insert menu in handwriting | long-press with the Pencil *next to existing handwriting* | Paste as handwriting, Insert Space | callout, insertion cursor | only appears inline with existing handwriting, and only after ≥10 unique lowercase chars have been saved |
| S12 | Math result inline | write expression + "=" | result appears in the user's handwriting style, in the tint colour | inline result, red dotted (error), blue dotted (ambiguous) | Insert Results / Suggest Results (Solve button) / Off |
| S13 | Equation menu | tap "=" or equation | see interpretation, Insert Graph, Add to Existing Graph, Graphs list | callout | 2D/3D options |
| S14 | Graph object | Insert Graph | live plot inside the note: pan, pinch-zoom, trace, axis tools, recentre, centre origin, recolour, duplicate | graph view, handles, axis controls | 2D, 3D, multi-equation |
| S15 | Value scrubber | tap a number (or hover with the Pencil) | drag to change a value. Dependent results and graphs update live | scrubber bar | active/idle |
| S16 | Shape snap | draw one stroke, pause without lifting | replaces stroke with a perfect shape. Undo restores the freehand stroke | snapped shape | lines, arrows, arcs, 90° polylines, squares, circles, rectangles, triangles, pentagons, chat bubbles, hearts, stars, clouds |
| S17 | Ruler overlay | tool picker ruler | straight lines. Move with one finger, rotate with two | ruler with angle readout | shown/hidden |
| S18 | Insert menu (Markup "+") | Markup "+" | Add Text box, Add Shape, Add Sticker, Image Description, signature | menu | |
| S19 | Attachment / PDF view in note | paperclip → Files / Scan Documents | PDFs/scans inline. Markup on them | PDF thumbnail/inline, Markup | small/large view |
| S20 | Search | search field in S02 / Find in Note | full-text search incl. recognised handwriting (supported languages) | search field, results list | no results, results |
| S21 | Share/export sheet | note "…" or share | Markup → PDF, Export as Markdown, Open in Pages, Print, Send a copy | share sheet | locked-note gating |
| S22 | Settings > Apple Pencil (system) | Settings app | Double Tap action, Squeeze action, Hover, Haptics, Scribble, Pencil-only drawing, Try Handwriting | toggles/pickers | Pro vs non-Pro |
| S23 | Settings > Apps > Notes (system) | Settings app | lines and grids default, default account, On My iPad account, sort | toggles | |
| S24 | Math Notes in Calculator | Calculator → Math Notes | same canvas, dark background by default. Notes saved to Notes "Math Notes" folder | sidebar of math notes | dark/light |
| S25 | Notes on Mac | macOS Notes | read handwriting/drawings, typed Math Notes, Math Results under the Format menu (per user report) | | the Mac can't draw. Handwriting is read-only (inference, medium) |

## Flows

```
F01 Write a handwritten note
    S01 -> S02 (new note button) -> S03 -> start writing with Pencil -> S04
    happy path taps: 1 (new note) + write. Pencil-down switches to Markup automatically
    edge: finger drawing off by default (needs toggle), drawing area must be resized with left handle,
          long handwritten notes lag (user reports: typing a text line "breaks" the drawing and fixes it)

F02 Make handwriting neater (Smart Script, manual)
    S04 -> select (double-tap word / triple-tap sentence / lasso) -> S09 -> Refine (slider) or Straighten
    happy path taps: 2-3
    edge: Refine/Auto-refine missing on some devices/regions. "Will download when connected to Wi-Fi" stuck state;
          capitals/other scripts refine poorly (user report)

F03 Turn on live auto-refine
    S04 -> S05 "…" -> S07 Auto-refine Handwriting ON
    happy path taps: 2 (users widely say it is hard to find)
    edge: refinement kicks in after a line or two. Input can be dropped "for a beat" while it animates (MacStories);
          users report words sloping or jumping off the line

F04 Correct a misspelled handwritten word
    S04 -> tap blue-dotted word -> S10 -> pick suggestion
    happy path taps: 2
    edge: suggestions unrelated to what was written. The replacement doesn't match line style. Until iPadOS 26
          the underline couldn't be turned off (users)

F05 Erase by scratching
    S04 -> scratch over word with pen tool, hold the Pencil down at the end
    happy path taps: 0 (gesture)
    edge: only with Pen / Monoline / Marker-type tools

F06 Make room / insert space
    S04 -> long-press with Pencil near handwriting -> S11 Insert Space (or drag the cursor) -> write
    happy path taps: 2
    edge: reflow imprecise, left margin not kept (MacStories). Drawing "a line to make space" rarely works (HN)

F07 Paste typed text as handwriting
    copy text elsewhere -> S04 long-press next to existing handwriting -> S11 Paste
    happy path taps: 2
    edge: needs ≥10 unique lowercase characters already saved. No paste option in blank space (users needed hours to discover)

F08 Solve maths inline
    S04 write "12×7 =" -> S12 result appears
    happy path taps: 0
    edge: unintended solving whenever "=" is written. Per-note toggle in "…" menu. No global default-off per HN user;
          Screen Time restriction workaround; variables must be declared before use; Latin variable names only

F09 Graph an equation
    write "y = 2x + 1" -> S13 Insert Graph -> S14
    happy path taps: 1
    edge: y must be on the left; 3D needs z on left

F10 Snap a shape (diagram)
    S04 draw a circle/line in one stroke, pause -> S16 snapped
    happy path taps: 0 (+1 undo to keep freehand)
    edge: triggers accidentally on wavy strokes / kanji (user); can't be disabled (user report, 2021)

F11 Draw a straight axis with the ruler
    S05 ruler -> S17 position (1 finger) / rotate (2 fingers) -> draw along edge
    happy path taps: 1 + positioning

F12 Switch tool fast with Apple Pencil Pro
    squeeze -> S08 -> hover/tap tool or colour
    happy path taps: 1 squeeze + 1 tap
    alt: double-tap -> switch to last-used tool (eraser by default)
    edge: squeeze action set system-wide in Settings. Some users only see undo/redo

F13 Find a handwritten word
    S02 search field -> type word -> S20 -> open note
    happy path taps: 2 + typing
    edge: language mismatch breaks it. Handwriting sent to Mac via AirDrop becomes an unsearchable image (user, 2020)

F14 Annotate a PDF
    S03 paperclip -> Files -> pick PDF -> Markup on it (S19)
    happy path taps: 4
    edge: exported note PDF contains only first page of a multipage PDF (Apple doc)

F15 Export a note as PDF
    S03 "…"/share -> Markup -> save to Files (S21)
    happy path taps: 3
    edge: blank pages / missing content reported on long handwritten notes (user, 2022)

F16 Sync to Mac / iPhone
    automatic via iCloud account
    happy path taps: 0
    edge: handwriting vanishing, notes reverting to older state after crash, blank pages on other devices (users, 2022–2024)
```

The happy-path numbers to beat, for Luca's main loops: new note = 1 tap; neaten = 0 taps once enabled (auto) or 2–3 (manual); tool switch = 1 squeeze + 1 tap; erase = 0 taps (scratch).

## Components

| component | variants | states | used on |
| --- | --- | --- | --- |
| Tool picker (palette) | docked full, minimized, squeeze mini-palette | visible, hidden-but-active (responds to squeeze/double-tap), dragged to edge | S04, S05, S08 |
| Tool well | pen, monoline, marker/highlighter, pencil, fountain pen, crayon, watercolour, reed, eraser (pixel/object), lasso, ruler, Scribble (text) | selected, hover-preview, with width/opacity popover | S05 |
| Colour picker | swatches, Grid, Spectrum, Sliders, eyedropper | selected | S05 |
| Selection callout | handwriting menu, drawing menu, text-object menu | word/sentence/paragraph/lasso | S09–S11 |
| Refine slider | inline slider + Refine button | adjusting | S09 |
| Inline annotation marks | blue dotted (spelling/ambiguous), red dotted (maths error), tint-coloured result | tapped → menu | S10, S12 |
| Graph object | 2D, 3D, multi-equation | selected (handles), panning, tracing | S14 |
| Value scrubber | touch, Pencil hover | dragging | S15 |
| Shape snap | the 14 listed shapes | snapped, undo → freehand | S16 |
| Ruler | — | moving, rotating, drawing along | S17 |
| Paper background | blank, lines, grid (sizes) | per note | S04, S23 |
| Drawing area resize handle | — | dragging | S04 |
| Haptic tick (Pencil Pro) | squeeze, snap/alignment | — | S08, S16, S17 (inferred) |

## Inferred data model

```
Account     id, kind (iCloud | On My iPad | IMAP), name
            evidence: S01, Settings > Notes "On My iPad" account
            confidence: high

Folder      id, account_id, parent_folder_id?, name, is_smart, sort
            evidence: S01, "Math Notes" folder
            confidence: high (nesting: high, Notes supports subfolders)

Note        id, folder_id, title (first handwritten line suggested), created_at, modified_at, is_locked,
            is_pinned, paper_style (blank|lines|grid + size), math_results_mode (insert|suggest|off, per note)
            evidence: S02, S03, S23, HN "per note basis in the three dot menu"
            confidence: high (math mode per note: medium)

Block       id, note_id, order, kind (text | drawing | attachment | table | checklist)
            evidence: typed text and drawing areas interleave. Users fix lag by "typing a line of text" between handwriting
            confidence: medium (drawings are separate embedded objects in the note body)

Drawing     id, block_id, pkdrawing_data (PencilKit/PaperKit), height, content_version, thumbnail
            evidence: Meet PaperKit (WWDC25) says Notes uses PaperKit and saves a pre-rendered thumbnail for version mismatch
            confidence: high that it's PaperKit/PencilKit data; medium on exact fields

Stroke      id (UUID; public in PencilKit iOS 27), ink (type, colour, width), path points
            (location, timeOffset, size, opacity, force, azimuth, altitude, roll from content v3), transform, mask (pixel erase), renderGroupID
            evidence: PencilKit docs
            confidence: high

RefinedState (Smart Script)  per-stroke or per-word replacement geometry, user handwriting style model (on-device)
            evidence: "uses an on-device model to refine handwriting in a style similar to yours", "requires ≥10 unique lowercase characters"
            confidence: guess. Unknown whether Notes keeps the original strokes after auto-refine
                        (no Apple doc says it does; undo works right after, per normal undo stack)

HandwritingStyleModel  per-user glyph samples learned from saved notes (on-device)
            evidence: paste/convert needs 10 unique lowercase characters
            confidence: medium

MathExpression  id, drawing_id/text_range, parsed expression, variables declared, result, error state, ambiguity flags
            evidence: S12, S13; red/blue dotted lines
            confidence: medium

Graph       id, note_id, equations[], dimension (2|3), axis ranges, colours
            evidence: S14
            confidence: high

Attachment  id, note_id, kind (pdf | image | scan | link | audio), file, preview_size (small|large)
            evidence: S19, "Attachment View"
            confidence: high

RecognitionIndex  note_id, recognised text (multiple candidates), language, recognition_version
            evidence: handwriting search in S20; PKStrokeRecognizer.indexableContent/recognitionVersion
            confidence: medium (Apple says Notes uses the same tech as the public API)
```

Relationships: Account 1-n Folder (self-nesting), Folder 1-n Note, Note 1-n Block, Block 0-1 Drawing, Drawing 1-n Stroke, Note 1-n Attachment, Note 0-n Graph, Note 0-1 RecognitionIndex.

## Feature matrix

See `features.csv`. Must: 31, should: 14, could: 12, skip: 10 (67 rows). Priorities are set from **Luca's** needs, not from Apple Notes' own weighting. `clone` is `no` throughout.

## Out of scope (cannot or should not be cloned)

- The Smart Script learned-handwriting synthesis model (paste-as-handwriting, convert-to-handwriting, spell-correct-in-your-hand). It is private Apple ML with no public API (see `apis.md`), and it would also break Inkwell's rule against generating ink.
- Math Notes' maths engine, unit/currency conversion and live graphing. There's no public API, and Inkwell skips maths for neatening.
- Apple Intelligence features (Image Wand, Siri AI, Writing Tools), which are Apple-only.
- iCloud-account Notes sync (CloudKit-based, Apple-internal). Inkwell uses its own iCloud Drive folder.
- Collaboration, shared notes and mentions, which need a server/Apple's service. Not wanted.
- The system-wide Settings for Apple Pencil (squeeze action, double-tap action, hover). Inkwell reads these preferences but can't own them.

## Size

Screens 25, flows 16, entities 11. Hard parts for Inkwell are reversible live neatening without touching original ink, a maths-skip classifier, recognition/search across a large notebook (PKStrokeRecognizer helps on iPadOS 27+), no-data-loss iCloud Drive file sync with conflict handling, PDF import/annotate/multi-page export, and performance on long notes, which is Notes' own weak point. Size for the Inkwell slice that matches this: **L** (a quarter), mostly because of neatening and sync.
