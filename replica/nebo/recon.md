# Recon map: Nebo, now "MyScript Notes" (iPadOS, plus the iPad app on Apple-silicon Mac)

Scope: the core handwriting slice. That covers the library and folders, the editors (notebook, document, board, PDF), pens, eraser, lasso, shapes, ruler, templates and backgrounds, PDF import, annotation and export, search, sync and backup, Apple Pencil features, the Mac version, and recognition and beautification (text, maths, diagrams, pen gestures). AI, sharing and typed docs are only mentioned.
For: Inkwell, a personal (not App Store) handwriting app for Luca on iPad Pro M4/M5 + Apple Pencil Pro and on Mac via Catalyst. Luca writes cursive English, lots of maths and economics diagrams. Ink is never destroyed, neatening is reversible and skips maths, sync goes through an iCloud Drive folder, and everything stays on-device.
Date: 2026-10-12

> Note on naming: in **September 2025 (v7.0)** Nebo was renamed **MyScript Notes** on iOS and Android (App Store ID 1119601770, v7.5.2 released 2026-10-06, 4.73★ from 38,654 US ratings). Nebo for Windows stays frozen. On iOS this note says "Nebo" throughout.

## Sources

| # | source | URL | notes |
| --- | --- | --- | --- |
| 1 | Help centre, the full text in one public file | https://help.myscript.com/llms-full.txt | Best single source: every help article. Read the sections on note types, gestures, convert, maths, shapes, sync, backup, settings, Pencil and long notes. |
| 2 | Help: FAQ (pricing, free tier, the rename) | https://help.myscript.com/notes/faq/ | Free tier is 5 pages per notebook with no sync and no AI. Plans are monthly, yearly or lifetime. A MyScript account is needed for full features. |
| 3 | Help: iOS version history (changelog) | https://help.myscript.com/notes/versions/ios/ | Versions 3.2 (2021) to 7.3 (2026). Shows what is new and what the team prioritises. |
| 4 | Help: pen gestures | https://help.myscript.com/notes/edit-content/pen-gestures-and-interactions/ | Scratch, join, break, underline, strike and frame. |
| 5 | Help: convert | https://help.myscript.com/notes/edit-content/convert/ | Double-tap in documents. In other note types you lasso, then pick Convert, then choose a type. |
| 6 | Help: maths | https://help.myscript.com/notes/create-content/math/ | Supported symbols, solving, LaTeX copy. |
| 7 | Help: shapes | https://help.myscript.com/notes/create-content/shapes/ | Draw then hold to get a perfect shape, plus the ruler and Pencil Pro haptics. |
| 8 | Help: cloud sync | https://help.myscript.com/notes/export-sync-and-back-up/cloud-sync/ | iCloud, Google Drive or Dropbox. .nebo files are hidden in the cloud. Conflicts keep both copies. |
| 9 | Help: folders and collections | https://help.myscript.com/notes/overview/folders-and-collections/ | Two levels only, with no folders inside folders. |
| 10 | App Store listing and lookup API | https://apps.apple.com/us/app/myscript-notes-ai-handwriting/id1119601770 | Pitch, current version, rating count, release notes. |
| 11 | App Store customer reviews RSS (US pages 1–10, GB pages 1–2) | https://itunes.apple.com/us/rss/customerreviews/page=1/id=1119601770/sortBy=mostRecent/json | 600 reviews, Oct 2023 to Oct 2026. |
| 12 | Hacker News Algolia API | https://hn.algolia.com/api/v1/search?query=nebo%20myscript&tags=comment | 25 relevant comments from 2014 to 2025. |
| 13 | MPU and Literature & Latte forums | https://talk.macpowerusers.com/t/handwriting-to-drafts/5448 , https://forum.literatureandlatte.com/t/handwriting-recognition/40837 | Short excerpts only. |
| 14 | MyScript developer support forum (iink SDK licensing) | https://developer-support.myscript.com/support/discussions/topics/16000031363 | Licensing context only. The info is old, see the SDK section. |
| 15 | Reddit | not reached | reddit.com returned 403 to the JSON API without OAuth, and WebFetch is blocked. **Not used.** |

Not done: no app binary, no network logging, no account login, no screenshots. Screens and tap counts below are **inferred from help docs and reviews**, not from using the app.

## Core loop

You write by hand with Apple Pencil, fix it with pen gestures that need no tool switch (scratch to erase, line to join or split), and turn it into clean text, maths (LaTeX) or perfect shapes when you choose to. Recognition makes everything searchable.

## How Nebo decides text vs maths vs diagram (the bit Inkwell cares about)

- **It mostly does not decide on its own; the user labels it.** In notebooks, boards and PDFs, conversion is lasso, then **Convert…**, then a choice of **Text / Math / Diagram**. The help says you "need to label your content type — like text, math, or diagram — to make conversion easier". A Jan 2025 review complains about "the new popup forcing me to select 'Text' or 'Math'".
- **Documents use explicit blocks.** Text paragraphs are the default. Maths and diagrams must be inserted as objects first: double-tap empty space, then Math or Diagram. "In documents, math must be inserted as a predefined math object."
- **Shapes are triggered by a gesture.** You draw one stroke, then **hold** the pen to snap it to a perfect shape. Lines and arrows work too. With Pencil Pro there is a haptic tick on snap, on 90° connector rotation and on conversion.
- **Pen gestures are always live and cannot be switched off.** Scratch-out and the join and break lines are interpreted all the time. Only the *result* of underline and strike-through can be configured. This is the single biggest source of "it changed my drawing" complaints (≥24 hand-read reviews, see fixes.md).
- **Search runs in the background on all ink.** Handwriting in notebooks has been searchable since v6.2 (Oct 2024) without converting.

## How reversible it is

| action | reversible? | evidence |
| --- | --- | --- |
| Convert handwriting to text, maths or shape | Only by undo. No documented "show original ink" or "revert to handwriting" | Help pages on convert, maths and shapes say nothing about it. A GB review (2023-08-18) says it is "difficult to go back to the handwriting original view once you fixed many words". Confidence: medium |
| Document reflow and auto-list formatting | Users report it **cannot be undone** | A GB 2★ review (2026-02-22): "This formatting cannot be undone, and the only way of correcting it is to erase everything". A GB 3★ review (2026-05-26) says words "move and overlap" |
| Perfect shape | Undo only | Shapes help page |
| Scratch-out erase | Undo, but users say it erased sketches they meant to keep | US 4★ review (2023-11-07) |
| Delete a page | **Not recoverable** | "Once a page has been deleted, it cannot be recovered." |
| Optimise a PDF | **Destroys the original quality** | "Once optimized, the original PDF quality cannot be restored." |
| Delete a note, folder or collection | Trash (v5.8+) | Trash help page |

Takeaway: Nebo's beautification is **destructive by default**. Inkwell's rule of keeping the original ink plus a reversible transform is a real differentiator, not a nicety.

## Screens

| ID | screen | route / how to reach | purpose | key components | states seen |
| --- | --- | --- | --- | --- | --- |
| S01 | First run (language, account, paywall) | first launch | Pick the handwriting language, sign in or create a MyScript account, start the 7-day trial or go free | language list, account form, paywall sheet | reviews: stuck on language "next", sign-in freezes, paywall before trying |
| S02 | Library home | app root | Browse notes | left **side panel** (collections, then folders), folder view (grid or list), top bar (Create, Sort, Search, Study space) | empty, filled, search active |
| S03 | Create menu and new-note sheet | Create (top right) | Pick the type (notebook, board, document, Import as PDF), then name, icon colour, page size, orientation, page colour, pattern and language | menu, form, language list with downloads | the language is **locked after creation** |
| S04 | Notebook editor | open a notebook | Fixed-size pages, zoomable | top bar (title, back, undo/redo, add, search, more), toolbar, left **thumbnail sidebar** | orange or red "note too large" banner |
| S05 | Document editor | open a document | Responsive reflowing text column, no zoom | conversion preview line above the ink, block handles, style menu (title, subtitle, paragraph, lists) | preview on or off |
| S06 | Board editor | open a board | Infinite canvas | zoom-level and zoom-lock pill bottom-left (bottom-right for left-handers) | 100% default zoom |
| S07 | PDF editor | import a PDF | Annotate, fill forms | thumbnail sidebar, page management, Optimise PDF dialog | large-PDF lag (reviews) |
| S08 | Tool option popovers | second tap on a tool | Pen: felt, fountain or brush, width, pressure. Highlighter: type and width. Eraser: stroke or precise, width. Lasso: freehand or rectangle. Plus colours | popover, slider, colour editor (HSB) | |
| S09 | Floating Pencil palette | squeeze (Pencil Pro) or double-tap (Pencil 2) | Quick switching between tools, width and colour | floating toolbar near the pen | |
| S10 | Lasso context menu | lasso around ink | Convert…, Copy as…, Resize, Indent…, Delete, Cut/Copy | menu, then a type picker (Text/Math/Diagram) | |
| S11 | Insert-object menu | double-tap empty space (documents), or the Add button | Math, Diagram, Drawing, Image, board section | menu | |
| S12 | Search | magnifier in the library or in a note | Library-wide search over ink, typed and converted text plus note names. In-note search has up and down arrows | search field, results in the side panel, blue highlights | |
| S13 | Settings | side panel, then …, then Settings | Display, Pen (writing position, active pen), Writing (conversion preview, font size and line height, languages, colours), Interactions (underline and strike results per note type), Advanced (tap for keyboard, ruler unit), Sync, Backup | grouped list | |
| S14 | Sync setup | Settings, then Sync | Sign in to a MyScript account, pick iCloud, Google Drive or Dropbox, auto or manual | provider list, status icons | conflict = both copies kept |
| S15 | Export and share | note …, then Export | Notebook or board: PDF, PNG, SVG, .nebo. Document: text, PDF, docx, .nebo. PDF: flattened or not. Web link (not for notebooks) | sheet, format list, toggles | |
| S16 | Trash | side panel | Restore notes, folders and collections (pages excluded) | list | |
| S17 | Split view | v6.7+ | Two notes side by side | iPadOS split | |
| S18 | Study space and AI | top bar | Summarise, explain, quiz, chat | out of scope | |

## Flows

```
F01 Create a new lined notebook
    S02 -> Create -> New notebook (S03) -> name, page size, pattern, language -> S04
    happy path taps: ~6 + typing a name (inferred from the help steps)
    edge: language locked after creation; wrong page size can't be fixed for existing pages (unverified)

F02 Write, then fix a word without switching tools
    S04: write -> scratch out the word -> rewrite; draw an upward line to join, a downward line to split
    happy path taps: 0
    edge: scratch misfires on sketches/shading; gestures cannot be disabled

F03 Convert handwriting to typed text (notebook/board/PDF)
    S04 -> lasso tool -> loop the ink -> Convert… (S10) -> Text
    happy path taps: 3 + lasso stroke   |  in a document: double-tap the paragraph = 1 gesture
    edge: the Text/Math popup adds friction; reverting to the original ink is undo-only

F04 Turn a handwritten equation into LaTeX
    lasso the equation -> Copy as… -> Math -> paste into a LaTeX editor
    happy path taps: 3 + lasso stroke
    edge: inline maths inside a text line is hard ("difficult to include in-line math in text");
          advanced notation "simply not usable" (4★, 2026-03-08)

F05 Neat diagram: draw shapes and arrows
    draw a box in one stroke -> hold -> it snaps to a perfect rectangle (haptic on Pencil Pro);
    draw an arrow from shape to shape -> it snaps to the shape edge
    happy path taps: 0
    edge: long lines snap into fraction bars or arrows unasked; hexagons aren't recognised (chemistry students)

F06 Add a page to a notebook
    show sidebar -> … on a thumbnail -> Insert blank page
    happy path taps: 3 (reviews: "a multi step process to add another page")
    edge: no continuous vertical scroll in notebooks ("There is no continuous scroll notebook option")

F07 Import a lecture PDF, annotate and export
    S02 -> Create -> Import as PDF… -> Files picker -> S07 annotate -> … -> Export -> PDF -> flatten? -> share
    happy path taps: ~3 to import, ~4 to export
    edge: 500-page PDFs lag or crash; text letters vanish while zooming; "Optimise PDF" is irreversible

F08 Find something I wrote last month
    S02 -> search -> type -> open the side panel for results -> tap a note -> blue highlights, up and down arrows
    happy path taps: ~3 + typing
    edge: search notes by name only arrived in v7.3 (2026)

F09 Switch tool mid-sentence
    squeeze the Pencil Pro -> floating palette at the nib -> tap the eraser or highlighter
    happy path taps: 1 (+ squeeze)
    edge: double-tap sometimes gets "stuck" (4★, 2025-11-08)

F10 Undo or redo
    two-finger tap = undo, three-finger tap = redo (since v6.7, Feb 2025); or the arrows in the top bar
    happy path taps: 0–1
    edge: for years there was no gesture; this was a top 3–4★ request

F11 Make space in the middle of a page
    two-finger long-press between lines -> a blue line appears -> drag down or up
    happy path taps: 0 (1 gesture)

F12 Set up sync to a second device
    side panel … -> Settings -> Sync -> sign in to or create a MyScript account -> choose iCloud -> auto-sync on
    happy path taps: ~6 + account creation
    edge: conflicted copies, duplicates, repeated re-login, sync paused in low battery mode

F13 Back up the whole library
    … -> Settings -> Backup -> Back up library -> location -> Save
    happy path taps: 5–6
    edge: no automatic backup; "We do not keep copies or backups of your notes."
```

## Components

| component | variants | states | used on |
| --- | --- | --- | --- |
| Top navigation bar | library, editor | title editing, undo/redo enabled or disabled | S02, S04–S07 |
| Tool strip | keyboard, pen, highlighter, eraser, lasso, laser, ruler, colour swatches | selected, second-tap popover | S04–S07 |
| Tool popover | pen (type, width, pressure), highlighter, eraser (stroke or precise), lasso (freehand or rect) | — | S08 |
| Floating Pencil palette | — | appears at the pen on squeeze | S09 |
| Colour swatch row and HSB editor | default palette, custom | add, edit, delete, long-press drag to reorder | S04–S07 |
| Lasso selection | freehand, rectangle | selected (handles), context menu | S10 |
| Context menu | lasso, object, empty-space long-press (Paste, Adjust space) | — | all editors |
| Type picker | Text / Math / Diagram | — | S10 |
| Conversion preview line | — | candidates popover on tap | S05 |
| Content blocks | paragraph, math, diagram, drawing, image, board section | selected, resizing | S05 |
| Page thumbnail sidebar | notebook, PDF | shown, hidden, page "…" menu | S04, S07 |
| Ruler overlay | — | drag, rotate, snap | S04–S07 |
| Laser pointer trail | — | fades | S04–S07 |
| Zoom pill and zoom lock | — | locked or unlocked, % | S06 |
| Large-note banner | orange, red | — | S04 |
| Sync status icon | up to date, refreshing, offline, "To sync" | — | S02, S14 |
| Side panel tree | collection, folder | expanded, select mode | S02 |
| Note card | grid, list | — | S02 |
| Haptic tick | snap, 90° rotate, convert | — | Pencil Pro |

## Inferred data model

```
Library     collections[], settings, palette, user_dictionary
            evidence: S02, S13, user-dictionary help | confidence: high

Collection  id, name, folders[] (sorted alphabetically, cannot be reordered)
            evidence: folders help | confidence: high
Folder      id, name, icon_color, collection_id   (no nesting)
            evidence: "You can't create folders within folders" | confidence: high

Note        id, folder_id, type (notebook | document | board | pdf), title, language (immutable),
            background {color, pattern}, page_size, orientation, created_at, modified_at,
            sort_index, zoom_state (kept up to 30 days)
            evidence: create-notes help, zoom help | confidence: high

Page        id, note_id, index, size, background, sync_version
            evidence: notebook and PDF page management; v5.0 "page-level cloud sync" | confidence: high (page-level sync), medium (fields)

Stroke      id, page_id, points[{x,y,t,pressure,tilt?}], pen_type (felt | fountain | brush),
            width, color, tool (pen | highlighter)
            evidence: pen settings, "active pens detect pressure and angles" | confidence: medium

Block/Object  id, page_id, kind (text-paragraph | math | diagram | drawing | image | board-section),
            bbox, style (title | subtitle | paragraph | list), stroke_ids[] or converted_content
            evidence: documents help ("dedicated blocks") | confidence: medium

Recognition id, block_id, candidates per word, chosen label, bbox, links to strokes
            evidence: conversion preview with tappable word suggestions; the public iink SDK
            documents a "JIIX" JSON export with words, candidates and stroke references | confidence: medium (guess for the app's storage)

ConvertedContent  text | latex/mathml | shapes {type, geometry}; replaces ink in the view (undo-only)
            evidence: convert help, reviews | confidence: medium

SyncAccount MyScript account id, provider (icloud | gdrive | dropbox), auto (bool), last_sync
            evidence: sync help | confidence: high
Conflict    note_id, versions[2], kept in library as two notes
            evidence: "will save both versions in your library" | confidence: high

File format .nebo per note (hidden in the cloud), .nebobackup = zip of collections
            evidence: backup help ("Rename your .nebobackup file to have a .zip extension") | confidence: high
```

Relationships: Library 1-n Collection 1-n Folder 1-n Note 1-n Page 1-n Stroke; Page 1-n Block; Block 1-1 Recognition; Note 0-n Conflict copies.

## What is achievable on-device for a solo dev without MyScript's SDK

| Nebo capability | on-device route for Inkwell (no server) | difficulty | confidence |
| --- | --- | --- | --- |
| Text recognition for search | Render each line of ink to an image and run Apple Vision `VNRecognizeTextRequest` (accurate mode, English). It handles handwriting. Cursive quality is OK for search, weaker than MyScript | M | medium. Test on Luca's own cursive first |
| Live conversion preview and word candidates | Vision returns the top-N candidates per observation, so a preview line is possible | M | medium |
| Scratch-out gesture | Pure geometry: many direction reversals, high path length to bbox ratio, overlaps existing strokes → delete the overlapped strokes (keep them in an undo/trash layer) | S | high |
| Join and split lines | Geometry: a short vertical stroke between words → adjust spacing. In Inkwell it should only move the *transform*, never the ink | S–M | high |
| Hold-to-snap shapes | Pause detection after a stroke, then fit a line, rect, ellipse, triangle or arrow (least squares or corner detection). Keep the raw stroke, store the snapped geometry as a reversible override | M | high |
| Maths detection (for "skip maths" in neatening) | **No public Apple maths-recognition API** (Math Notes is private). Use heuristics: a long horizontal bar with ink above and below, superscript offsets, isolated symbols, a high digit or operator ratio and low Vision confidence on the line. Or let Luca mark a region as maths with one gesture. Optional later: a small Core ML image-to-LaTeX model | M (heuristics), L (ML) | medium |
| Handwriting to LaTeX | Not practical without a model. Treat as "could" | L | low |
| Text vs diagram segmentation | Heuristics: stroke size, aspect ratio, closed shapes, lines longer than about 3× the x-height, ink on the axes → diagram. Again, a manual override is the reliable part | M | medium |
| Search across all ink | Background Vision pass per page, store text + bbox in a local index (SQLite FTS) | M | high |

**MyScript iink SDK (context only, not for Inkwell):** a commercial SDK. Developer-forum answers (around 2020) say MyScript gives about **100 free licences for development and testing**, and production needs paid licence packs quoted by sales. The old cloud tier was **2,000 free requests per month** (MacTech 2017, forum around 2020). The current pricing page was not reached. **Unverified for 2026.** It would also put a commercial dependency into a personal app, so Apple Vision is the right call.

## Feature matrix

See `features.csv`. Must: 34, should: 18, could: 17, skip: 13 (82 rows, incl. Inkwell-only rows with original=no).

## Out of scope (cannot or should not be cloned)

- MyScript's recognition engine and models (iink): proprietary and licensed. Inkwell uses Apple Vision plus its own geometry.
- The .nebo file format and its compatibility: proprietary, and not needed.
- AI features (Summarise, Explain, Quiz, Chat, Study space): not wanted, and they need a server.
- Web-link sharing, collaboration, the MyScript account system, Google Drive and Dropbox sync: they need a server or account.
- Windows and Android apps.
- Document-mode reflow of handwriting: technically possible, but it rewrites the ink layout and so conflicts with "never alter ink". At most, a reversible line-by-line transform.
- Paywall and trial machinery: Inkwell is personal.
- Names, icons, pen names, colour palettes and marketing copy: never copied.

## Size

Screens 18 (about 14 in scope), flows 13, entities 11.
Hard parts:
1. Reliable, non-destructive gesture recognition (scratch, join, split) that never fires on maths or diagrams.
2. Maths and diagram detection for "skip neatening" without a maths API.
3. Vision-based handwriting search on cursive.
4. iCloud Drive folder sync with zero loss, including conflicts.
5. Large-PDF performance.
6. PencilKit, or a custom ink engine that keeps the original strokes alongside reversible transforms.

Size: **L** (a quarter) for the full slice. The core loop (notebook, pens, scratch-erase, iCloud folder) is about **M**.
