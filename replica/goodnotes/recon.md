# Recon map: GoodNotes (iPad + Mac, current build 7.1.x; "GoodNotes 6" generation)

Scope: the core handwriting slice only. Library and folders, notebook and page editing, pens, eraser, lasso, shapes, templates, PDF import/annotate/export, search, sync and backup, Apple Pencil features, and the Mac app.
For: Inkwell, Luca's personal iPad Pro (M4/M5) + Apple Pencil Pro + Mac Catalyst handwriting app. Not for sale and not on the App Store.
Date: 2026-10-12

Method: public sources only. I used the App Store listing (iTunes lookup API), the official help centre (read in the browser), the public pricing page, the official feature-request board, and 553 user reviews (see `reviews.csv`). I did not open the app, log in, read any code or binaries, or save screenshots. **Tap counts are inferred from the steps in the help articles, not measured on a device.** Each one is marked "doc", and Luca can check them on his own iPad.

Version note: the App Store entry (id 1444383602) is now just called "Goodnotes" and is on 7.1.28. A big redesign shipped in Oct-Nov 2025 (7.0.x). It brought a new floating toolbar, Lasso as the tool the app falls back to, a new text tool, and new shapes. Most of the recent complaints are about that redesign. "GoodNotes 6" in Luca's brief means this generation.

## Sources

| # | source | URL | notes |
| --- | --- | --- | --- |
| 1 | App Store listing + metadata | https://apps.apple.com/us/app/goodnotes/id1444383602 (via https://itunes.apple.com/lookup?id=1444383602) | Marketing description, v7.1.28, 4.72 stars from 461,506 ratings, iPad/iPhone/Mac |
| 2 | Help centre root | https://support.goodnotes.com/hc/en-us | Section list: Taking Notes, Viewing/Searching/Navigating, Templates, Import/Export, Organizing, Sync/Backup, iCloud, Goodnotes Cloud |
| 3 | Apple Pencil Pro | https://support.goodnotes.com/hc/en-us/articles/9757771783823 | Squeeze shows the Palette. Barrel roll drives Dynamic Ink on the fountain pen. Needs v6.3.25+ and iPadOS 17.5+ |
| 4 | Customize the toolbar | https://support.goodnotes.com/hc/en-us/articles/8900755183631 | Hide and reorder tools. Lasso is fixed first. No presets. Undo/Redo can go left or right. Floating menus dock to an edge. The Pencil quick toolbar can't be customised |
| 5 | Undo/redo gestures | https://support.goodnotes.com/hc/en-us/articles/14069931315983 | Two-finger double tap undoes, three-finger double tap redoes. No toggle to turn them off |
| 6 | Shapes and diagrams | https://support.goodnotes.com/hc/en-us/articles/13682939148943 | Shape tool, AutoShape, draw-and-hold with the pen, connectors, lock shape |
| 7 | Edit Handwriting (lasso) | https://support.goodnotes.com/hc/en-us/articles/10779441732111 | Reflow handwriting, straighten lines, alignment, colour |
| 8 | Sidebar navigation | https://support.goodnotes.com/hc/en-us/articles/9497798035983 | Pages, Outline, Audio and Boards tabs. Drag to reorder. Bookmarks filter. Multi-select actions |
| 9 | Search | https://support.goodnotes.com/hc/en-us/articles/7353743594127 | Indexes handwriting, typed text, PDF text (only if the PDF already has OCR), titles and outlines |
| 10 | Scroll direction | https://support.goodnotes.com/hc/en-us/articles/7353695996559 | Horizontal or vertical, per document, with a default in Settings |
| 11 | Change page template | https://support.goodnotes.com/hc/en-us/articles/7353743758991 | More > Change Template, then colour, size and orientation |
| 12 | Import files | https://support.goodnotes.com/hc/en-us/articles/7353717816463 | PDF, images, Office files, .goodnotes. Can import into the current doc before/after the page or at the end |
| 13 | Editable vs flattened PDF export | https://support.goodnotes.com/hc/en-us/articles/8537070839183 | Flattened export can carry a searchable handwriting layer. Editable keeps outlines and links |
| 14 | Auto Backup | https://support.goodnotes.com/hc/en-us/articles/7352786555279 | One-way backup to Drive/Dropbox/OneDrive/WebDAV in .goodnotes, PDF or both. iOS only. Default about every 12 h |
| 15 | Goodnotes Cloud FAQ | https://support.goodnotes.com/hc/en-us/articles/10779870669711 | Its own cloud on AWS, rolling out gradually. Data can be deleted after 2 years inactive without payment |
| 16 | Scribble to Erase | https://support.goodnotes.com/hc/en-us/articles/7443501398671 | Scribble over pen strokes with the pen to erase them. Can be turned off in Pen Gestures |
| 17 | Organizing documents (section) | https://support.goodnotes.com/hc/en-us/sections/7352625352847 | Trash/recover, favourites, folder colour/icon, merge, move, lock objects, password lock |
| 18 | Pricing | https://www.goodnotes.com/pricing | Free: 3 files, 5 MB import. Essential $11.99/yr. Pro $35.99/yr. AI Pass +$9.99/mo |
| 19 | Feature-request board | https://feedback.goodnotes.com/forums/191274-customer-suggestions-for-goodnotes | 7,563 ideas. Vote counts used in fixes.md |
| 20 | Reviews | reviews.csv | 500 App Store (US+GB RSS), 24 Hacker News, 16 Trustpilot, 14 board ideas |

## Core loop

Open a notebook from the library, write on paper-like pages with the Pencil (pen, highlighter, eraser, lasso), add pages or PDFs, then find it again later with handwriting search. It all syncs across Apple devices.

## Screens

| ID | screen | route / how to reach | purpose | key components | states seen |
| --- | --- | --- | --- | --- | --- |
| S01 | Library: Documents (root) | App launch | Browse folders and notebooks | Grid/list toggle, "+ New" button, folder tiles with colour/icon, notebook covers, sort, Goodnotes menu (top-right), cloud/backup status icon | empty (new user), filled, list view, syncing, sync-error badge |
| S02 | Folder (nested) | Tap a folder in S01 | Same as S01, one level down | Breadcrumb/back arrow, same grid | empty, filled |
| S03 | New menu (sheet) | S01 "+ New" | Create a notebook/whiteboard/text doc/folder, import, scan, take photo | Action list | default |
| S04 | New notebook sheet | S03 > Notebook | Pick title, cover, paper template, colour, size, orientation | Template gallery (blank/ruled/grid/dotted/Cornell/planner), cover picker, size/orientation menus | default, custom template |
| S05 | Library: Favourites / Shared / Search tabs | Library tab bar | Starred docs, shared docs, global search | Tabs, search field, results list with page thumbnails | empty, results, no results |
| S06 | Document view (notebook) | Open a doc | Write | Top nav bar (back, sidebar, search, bookmark, share, More), main toolbar (lasso, pen, eraser, highlighter, shapes, elements, text, image...), floating Writing Tools menu (colours/sizes), Undo/Redo, page canvas, tabs strip for open docs | horizontal paging, vertical scroll, read-only (free tier limit), locked (password) |
| S07 | Writing Tools floating menu | Select pen/highlighter | Colour swatches, thickness presets, pen style | Swatches, size dots, overflow; dockable to a screen edge | floating, docked, hidden |
| S08 | Pen settings popover | Tap the pen tool again | Pen type (fountain/ball/brush), pressure, stabilisation, Pen Gestures (Scribble to Erase, draw-and-hold shapes), React to Pen Rotation | Segmented control, sliders, toggles | default |
| S09 | Eraser settings | Tap eraser again | Size, erase entire stroke vs partial, highlighter-only, auto-deselect | Options list | default |
| S10 | Pencil Palette (Squeeze) | Squeeze Apple Pencil Pro | Switch tool, colour, thickness and undo next to the pencil tip | Radial/floating palette | shown at hover position |
| S11 | Lasso selection + object menu | Lasso tool, circle content | Move, resize, recolour, copy/cut, convert to text, Edit Handwriting, screenshot, delete | Selection outline, handles, context menu ("Included in Selection" filters: handwriting/images/text) | selected, multi-type selection |
| S12 | Edit Handwriting mode | S11 > More > Edit Handwriting | Reflow width, edit words, straighten lines, alignment, colour | Side handles, straighten button, align controls | active, reflow failure |
| S13 | Shapes / diagram editing | Shape tool, or pen draw-and-hold | Clean shapes, connectors, text in shapes, lock | Handles (scale/resize/rotate), connector dots, style menu | selected, locked |
| S14 | Add Page menu | "+" at page end / add-page icon | New page before/after/at end, choose template, import into doc | Template thumbnails, position control | default |
| S15 | Change Template sheet | More > Change Template | Swap paper on the current page | Colour, Size and orientation menus, template library, Apply | default |
| S16 | Sidebar (Pages / Outline / Audio) | Sidebar icon, top-left of S06 | Thumbnails, reorder, bookmarks filter, multi-select (copy, rotate, export, move, trash), outline jump | Thumbnail grid, filter menu, select mode | sidebar vs window mode |
| S17 | In-document search | Magnifier in nav bar | Find a word in handwriting, PDF text or typed text | Field, results list | results, no results |
| S18 | Export / Share sheet | Share icon | Export page or whole document as PDF (editable/flattened, handwriting recognition), image, .goodnotes | Scope (current page / all), format, options | exporting, error |
| S19 | Settings (Goodnotes menu) | S01 top-right menu | Document Editing (scroll direction, undo position, toolbar customisation), Stylus & Palm Rejection, Handwriting Recognition language, Cloud & Backup | Grouped lists | default |
| S20 | Cloud & Backup status | Cloud icon in S01 | Sync state, Auto Backup queue, Back Up Now, Goodnotes Cloud opt-in | Status list, queue, toggles | synced, pending, failed, migration prompt |
| S21 | Toolbar Customization | Accessories > Toolbar Customization | Hide or reorder tools | Rows with +/- and drag handles, Reset | default |
| S22 | Trash | Library > Trash | Recover deleted documents, folders and pages | List, Recover, Empty | empty, filled |
| S23 | Paywall / upgrade sheet | Creating a 4th file on Free; old purchases | Upsell | Plan cards | blocking, dismissible |
| S24 | Mac window | Mac app | Same library and doc views in a window. Users report no visible undo/redo button and few shortcuts | Sidebar, toolbar, tabs | n/a |

Screens Luca could add to `replica/screens/` from his own iPad (reference only, never shipped). They would firm up the guesses above: **S01** library root, grid and list; **S04** new-notebook template sheet; **S06** document view at default toolbar with no tool menus open; **S07** writing-tools menu, floating and docked; **S08** pen settings popover; **S10** squeeze palette; **S11** lasso context menu; **S12** Edit Handwriting with straighten; **S14** add-page menu; **S15** change template; **S16** sidebar pages + multi-select; **S05/S17** search results showing a handwriting hit; **S18** PDF export options; **S19** Document Editing + Stylus settings; **S20** cloud & backup status; **S24** the Mac window. Short screen recordings of F02, F05 and F07 would also give real tap counts.

## Flows

Tap counts come from documented steps (doc). Pencil strokes don't count as taps.

```
F01 Create a nested folder and a new lined notebook in it
    S01 -> S03 (+New) -> Folder -> name -> open S02 -> S03 -> Notebook -> S04 pick template/colour -> Create -> S06
    happy path taps: ~8 (doc). Title entry by keyboard.
    edge: free tier counts folders/files toward the 3-file limit (user report); default template remembered from last time (guess)

F02 Write a page of lecture notes, switching pen <-> highlighter <-> eraser
    S06 -> tap tool (1) -> pick colour in S07 (1) ; or squeeze -> S10 -> tool (1)
    happy path taps: 1 per switch (toolbar) or squeeze+1 (palette). Erase by scribbling: 0 taps.
    edge: after text/shape use the tool reverts to Lasso (7.0 redesign; 543-vote complaint); palm triggers long-press popups (zoom / add link / comment); accidental 2-finger undo

F03 Add a new page with a different template (e.g. grid after lined)
    S06 -> Add Page (+) -> S14 pick position + template -> done
    happy path taps: ~3 (doc). Changing an existing page: More -> Change Template -> template -> Apply = 4.
    edge: page size mismatch with imported PDF pages

F04 Draw a clean economics diagram (axes, curves, labels)
    S06 -> pen: draw line and hold (snaps straight; adjust angle/scale while holding) -> release
    happy path taps: 0 extra taps (draw-and-hold). Shape tool path: 1 tap to select tool + 1 to return to pen.
    edge: 3/4 arcs autocorrect to ovals (user report), snapping guides fight free placement, shape stroke width doesn't match pen (board idea 103 votes)

F05 Lasso, move and resize part of the handwriting
    S06 -> Lasso (1) -> circle -> drag / pinch handles -> tap pen (1)
    happy path taps: 2. Palm can also invoke lasso (board idea "Disable Palm Gestures").
    edge: lasso includes unwanted object types unless "Included in Selection" is set; copy/cut moved into a sub-menu in 7.0 (user report)

F06 Neaten handwriting (closest existing analogue to Inkwell's neatening)
    S11 lasso -> object menu -> More -> Edit Handwriting (S12) -> straighten / drag side handles to reflow
    happy path taps: ~4-5 (doc). Manual, after the fact, per selection. Not live.
    edge: reflow fails on mixed content ("Why isn't my text reflowing correctly?" article)

F07 Import a lecture PDF and annotate it
    S01 -> +New -> Import -> Files picker -> file -> Open -> S06 (PDF pages as pages)
    happy path taps: ~4 (doc). Into an existing doc: Add Page -> Import -> file -> position = ~4.
    edge: free tier 5 MB import limit; Office files convert imperfectly; PDF text searchable only if it already has OCR

F08 Export annotated PDF (selected pages)
    S06 -> Share -> Export -> current page OR all pages -> PDF -> Flattened/Editable -> Share target
    happy path taps: ~5 (doc). No arbitrary page range from the share sheet (2 reviews). Workaround: Sidebar select pages -> Export (~4 + n page taps).

F09 Find a handwritten word across all notes
    S01 -> Search tab -> type -> tap result -> S06 at match
    happy path taps: 2 + typing (doc). In-doc: magnifier -> type -> result = 2.
    edge: recognition language must be downloaded per language; some users say search highlight was removed (1 review); capitals misread (3 reviews)

F10 Navigate a long notebook
    S06 -> Sidebar (1) -> tap thumbnail (1); bookmarks: filter (2) -> tap (1); outline tab for PDFs with TOC
    happy path taps: 2. Return to library and back to the open doc: no direct way back (2 reviews + 337-vote board idea).

F11 Recover a deleted page/document
    S01 -> Trash (S22) -> select -> Recover
    happy path taps: ~3 (doc)

F12 Set up sync + backup
    iCloud sync: Settings -> Cloud & Backup -> iCloud toggle. Auto Backup: Goodnotes menu -> Cloud & Backup -> Automatic Backup -> provider -> sign in -> format -> Done
    happy path taps: ~3 (iCloud), ~7 + OAuth (backup). Recent builds push migration to Goodnotes Cloud (2 reviews).
```

## Components

| component | variants | states | used on |
| --- | --- | --- | --- |
| Top nav bar (document) | iPad, iPhone, Mac | default, with open-doc tabs, read-only banner | S06 |
| Main toolbar | tool icons; Lasso fixed first | selected tool, overflow, customised order | S06 |
| Writing Tools menu | floating, docked vertically at an edge, hidden | colour swatches, size presets | S06, S07 |
| Pencil Palette (squeeze) | tools, colours, thickness, undo | shown at pencil | S10 |
| Tool settings popover | pen, eraser, highlighter, lasso, shape | default | S08, S09 |
| Lasso selection | outline + handles + object menu | single type, mixed, locked objects | S11, S12 |
| Shape object | rectangle (rounded default), ellipse, line, arrow, connector | selected, locked, with text | S13 |
| Page canvas | template backgrounds (blank, ruled, grid, dotted, Cornell, planner), PDF page | paging (horizontal), continuous (vertical), zoomed | S06 |
| Page thumbnail | normal, bookmarked, selected | drag-reorder | S16 |
| Library tile | folder (colour/icon), notebook cover, PDF | selected, syncing, locked | S01, S02 |
| Template picker | gallery + colour + size + orientation | default | S04, S14, S15 |
| Search results list | grouped by document, page thumbnail + snippet | results, empty | S05, S17 |
| Export dialog | page scope, format, flatten/editable, recognition toggle | exporting | S18 |
| Sync status icon | idle, syncing, error | tap -> S20 | S01 |
| Upsell modal | plan cards | blocking | S23 |

## Inferred data model

```
Folder      id, parent_id (nullable, nested), name, colour, icon, sort_order, created_at, deleted_at
            evidence: S01/S02, "Customize Folder Color and Icons", "Move documents and folders", Trash article
            confidence: high

Document    id, folder_id, type (notebook | whiteboard | text_doc), title, cover_id, created_at, modified_at,
            scroll_direction (horizontal | vertical), is_favourite, password_locked, deleted_at, outline (json)
            evidence: S03, scroll-direction article (per document), favourites, password protection, outline tab
            confidence: high (fields), medium (exact storage)

Page        id, document_id, index, template_id, template_colour, size (w,h), orientation,
            background_pdf_ref (nullable: source PDF + page number), bookmarked, seen, deleted_at
            evidence: change-template article (colour/size/orientation per page), import into doc, bookmarks filter, "mark as seen"
            confidence: high

Stroke      id, page_id, layer_id, tool (pen | highlighter | pencil), pen_style (fountain | ball | brush),
            colour, width, points[(x, y, pressure, azimuth/roll?, t)], created_at
            evidence: pen styles, React to Pen Rotation (roll stored or baked into width), scribble-to-erase works on Pen strokes only
            confidence: medium (point schema is a guess)

Layer       id, page_id, name, order, visible
            evidence: "Organize content with layers" article
            confidence: medium

Element     id, page_id, kind (image | text_box | shape | connector | sticker | tape | sticky_note), frame, rotation,
            style (json), locked
            evidence: shapes article (lock shape, connectors attach), lock objects article, text box, tape tool
            confidence: high (existence), guess (schema)

Template    id, name, kind (blank | ruled | grid | dotted | cornell | planner | custom_pdf), colours[], sizes[]
            evidence: S04, import custom templates article
            confidence: high

RecognitionIndex  page_id, language, words[(text, bbox)], updated_at
            evidence: search across handwriting, recognition language downloads, flattened export with handwriting layer
            confidence: medium (on-device or server unknown; GN states languages are downloaded on device)

Bookmark/OutlineItem  document_id, page_id, title, level
            evidence: outline tab, bookmarks filter, PDF TOC auto-import
            confidence: high

SyncState   document_id, cloud (icloud | goodnotes_cloud), status, last_synced_at; BackupJob queue (one-way)
            evidence: S20, Auto Backup article (queue, one-way, format)
            confidence: medium
```

Relationships: Folder 1-n Folder (nesting), Folder 1-n Document, Document 1-n Page, Page 1-n Layer, Layer 1-n Stroke/Element, Page n-1 Template, Page 0..1 PDF source page, Document 1-n OutlineItem, Page 1-1 RecognitionIndex.

The file format (.goodnotes, a zip package) is proprietary. Per the rules I did not inspect it. One HN author did reverse-engineer it to escape lock-in (https://news.ycombinator.com/item?id=49377665). That is evidence the lock-in hurts, not something to copy.

## Feature matrix

See `features.csv`. 91 rows. Must: 35, should: 25, could: 17, skip: 14 (including Inkwell-only rows with original = no or partial).

## Out of scope (cannot or should not be cloned)

- Goodnotes AI (summaries, Math AI, quiz generation, AI credits), Meeting/Audio AI, transcription. Mentioned only.
- Marketplace (stickers, planners, paid templates): their content and their creators.
- Collaboration, link sharing, comments, real-time co-editing, Teams/Enterprise admin.
- Study Sets / flashcards, Text Documents (typed docs), Whiteboard infinite canvas, presentation mode / laser pointer. Mentioned only.
- Goodnotes Cloud (their own AWS-backed sync service), accounts, sign-in, subscriptions, paywalls. Inkwell has no server by design.
- Android/Windows/Web clients.
- Their templates, covers, icons, names, fonts, marketing copy. Record patterns only.

## Size

Screens 24, flows 12, entities 10. Hard parts:
1. Ink engine: low latency with Pencil Pro, pressure, roll and hover, plus predicted-touch handling. Reviews show this is where GoodNotes is weakest.
2. Sync through an iCloud Drive folder with no data loss. That means file coordination, conflict versions, and append-only stroke logs.
3. On-device handwriting recognition for search on cursive English, with maths skipped.
4. PDF import/annotate/export with a searchable flattened layer.
5. Live reversible neatening, which GoodNotes doesn't have (it only has manual Edit Handwriting).
6. Large-document performance (tiling, lazy page load).

Size: **L** (a quarter) for the core slice to GoodNotes-level polish. An M-sized vertical slice is realistic: library + vertical-scroll notebook + 3 pens / 2 highlighters + eraser + lasso + templates + folder sync.
