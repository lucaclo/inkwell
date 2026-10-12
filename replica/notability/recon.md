# Recon map: Notability (iPadOS + macOS)

Scope: the core handwriting slice only. That means the library and folders, note and page editing, pens, eraser, lasso and shapes, paper templates, PDF import, annotation and export, search, sync, Apple Pencil features and the Mac version. AI, Gallery marketplace, collaboration, flashcards and quizzes, audio and typed docs are mentioned but not mapped.
For: Inkwell, Luca's personal (not App Store) handwritten-notes app for iPad Pro M4/M5 + Apple Pencil Pro and Mac Catalyst. Inkwell is on-device only, syncs through an iCloud Drive folder, never alters original ink and uses neatening that can be reversed.
Date: 2026-10-12. App version observed in the public listing: 16.13 (released 2026-10-12). It has 457,834 US ratings with an average of 4.76.

Method: public sources only. I read the help center, App Store listing and pricing page, plus user reviews. I did not log in, did not use a device, did not save screenshots and did not use any code. Tap counts below come from the steps in the help articles, so they are inferred, not measured on a device.

## Sources

| # | source | URL | notes |
| --- | --- | --- | --- |
| 1 | App Store lookup (listing text, version, ratings) | https://itunes.apple.com/lookup?id=360593530 | v16.13 notes: Liquid Glass, imported PDFs no longer land above the last page |
| 2 | Help center home | https://intercom.help/notability/en-us/ | redirects to support.gingerlabs.com |
| 3 | Getting Started | https://support.gingerlabs.com/en-us/articles/16042362-getting-started-with-notability | toolbox tool list, paper picker at the bottom of a new note |
| 4 | Create and Edit Notes | https://support.gingerlabs.com/en-us/articles/16300118-create-and-edit-notes | +New, rename, drag to folder, 30-day Recently Deleted |
| 5 | Organize Notes with Folders | https://support.gingerlabs.com/en-us/articles/16300020-organize-notes-with-folders | 6 nesting levels, sidebar, colours, lock |
| 6 | Subjects and Dividers (v15 and below) | https://support.gingerlabs.com/en-us/articles/16300129-subjects-and-dividers-version-15-and-below | old 2-level model, converted to folders in v16 |
| 7 | Viewing Your Notes | https://support.gingerlabs.com/en-us/articles/16300162-viewing-your-notes | All / Recents (last 10) / Favorites / Unfiled / Shared |
| 8 | Multi-Note and Note Switcher | https://support.gingerlabs.com/en-us/articles/16300213-multi-note-and-note-switcher | edge swipe, Open On Right/Bottom |
| 9 | Note View Settings | https://support.gingerlabs.com/en-us/articles/16300185-note-view-settings | Seamless (vertical) vs Single Page (horizontal) |
| 10 | Squeeze Gestures with Apple Pencil Pro | https://support.gingerlabs.com/en-us/articles/16300052-squeeze-gestures-with-apple-pencil-pro | 5 squeeze actions |
| 11 | Writing with Apple Pencil | https://support.gingerlabs.com/en-us/articles/16300204-writing-with-apple-pencil | double-tap options, hover, haptics, auto-deselect eraser |
| 12 | Settings: Appearances, Tools, & Gestures | https://support.gingerlabs.com/en-us/articles/16300218-settings-appearances-tools-gestures | 2-finger undo, 3-finger redo, hold to straighten |
| 13 | Eraser | https://support.gingerlabs.com/en-us/articles/16300189-eraser | partial vs whole stroke |
| 14 | Perfect Shapes | https://support.gingerlabs.com/en-us/articles/16300159-creating-and-styling-perfect-shapes | hold to snap, 8 shapes, snapping guides |
| 15 | Zoom View | https://support.gingerlabs.com/en-us/articles/16300180-zoom-view | zoom writing window that advances itself |
| 16 | Custom Templates and Note Background | https://support.gingerlabs.com/en-us/articles/16300179-custom-templates-and-note-background | Rule/Grid/Dot, 10 spacing levels, page sizes, one template per note |
| 17 | Customize your Toolbox | https://support.gingerlabs.com/en-us/articles/16300068-customize-your-toolbox | duplicate pens, hide, reorder |
| 18 | Content Manager and Bulk Actions | https://support.gingerlabs.com/en-us/articles/16300226-content-manager-and-bulk-actions | page thumbnails, reorder, bookmarks |
| 19 | Search | https://support.gingerlabs.com/en-us/articles/16300170-search | library search + in-note search |
| 20 | Handwriting and Math Conversion | https://support.gingerlabs.com/en-us/articles/16300114-handwriting-and-math-conversion | lasso > Convert > Text/Math, LaTeX editor |
| 21 | Importing Files | https://support.gingerlabs.com/en-us/articles/16300142-importing-files | add-space margins on import, bulk import |
| 22 | Sharing Notes | https://support.gingerlabs.com/en-us/articles/16300163-sharing-notes | PDF/Note/JPEG/PNG/NTB |
| 23 | Auto-Backup guide | https://support.gingerlabs.com/en-us/articles/16300117-auto-backup-third-party-backup-guide | one-way backup, not to iCloud |
| 24 | iCloud sync | https://support.gingerlabs.com/en-us/articles/16300116-syncing-notes-across-devices-with-icloud | two-way; "iCloud Sync is not a backup" |
| 25 | iCloud version history | https://support.gingerlabs.com/en-us/articles/16300149-icloud-version-history-restore-older-versions-of-notes | renaming a note wipes its versions |
| 26 | Notability Cloud FAQ | https://support.gingerlabs.com/en-us/articles/16300035-notability-cloud-faq | own cloud, account required, iCloud unavailable there |
| 27 | Keyboard shortcuts | https://support.gingerlabs.com/en-us/articles/16300139-keyboard-shortcuts | Mac vs iPad differences |
| 28 | Text and Text Boxes | https://support.gingerlabs.com/en-us/articles/16300260-text-and-text-boxes | tap anywhere to type, draw a text box |
| 29 | Pricing | https://notability.com/pricing | 5 free notes; Lite/Plus/Pro; handwriting search sits in Plus |
| 30 | 9to5Mac on Multi-Note (2018) | https://9to5mac.com/2018/05/22/notability-handwriting-search-more/ | history of split view |
| 31 | Reviews | see `reviews.csv` / `feedback.md` / `fixes.md` | 540 rows |

## Core loop

Tap **+New**. The note opens on the default paper, already titled with the date if that setting is on. You write with the Pencil and scroll down through a continuous vertical document where the ink flows over page breaks. Later you find the note in a folder or through search, and share it as a PDF.

## Screens

| ID | screen | route / how to reach | purpose | key components | states seen |
| --- | --- | --- | --- | --- | --- |
| S01 | Home tab (v16.7+) | app launch | recents, record, import in one place; reviewers say it adds 2 taps before notes | recent-notes row, quick actions, upsell card | filled, upsell banner |
| S02 | Library | sidebar / ⌘L on Mac | browse and organise notes | sidebar (All, Recents, Favorites, Unfiled, Shared, Folders tree), note grid/list, +New, sort/view menu, search bar | empty, filled, grid, list, collapsed folders, "loading/downloading" spinner (reviews) |
| S03 | Folder edit sheet | long-press / right-click a folder > Edit | rename, colour, emoji, lock, delete | text field, colour toggle, lock toggle, Save | default |
| S04 | New-note paper bar | inside a fresh note, at the bottom | choose Rule / Grid / Dot / Scan / Import / Templates | segmented paper chips | first open only |
| S05 | Note editor, Seamless (vertical) | open any note | handwriting on continuous vertically scrolling pages | title at top, toolbox (pen, pencil, highlighter, partial and whole eraser, text, select, media, hand, zoom, tape, ruler, laser), undo/redo, options, content-manager button | empty page, filled, PDF background, dark "content matches theme" |
| S06 | Note editor, Single Page (horizontal) | Options > View settings | page-by-page like slides | same as S05 | — |
| S07 | Pen style popover | tap selected tool again | colour, size, line style (solid/dashed/dotted) | 8 pinned colours, custom colour menu, size presets | — |
| S08 | Squeeze / arc palette | Pencil Pro squeeze (if set) | quick tool/colour/size switch near the nib | radial arc menu | open, closed |
| S09 | Selection (lasso) menu | Select tool, circle ink | move, resize, recolour, convert, copy, mirror | floating action menu | ink, mixed content |
| S10 | Template settings | Options > Template settings, or long-press +New | pick paper, size, colour, spacing | Gallery / My Templates tabs, size dropdown (Letter…A7), 10-step spacing slider | — |
| S11 | Content Manager | icon at top-right of the note | page thumbnails, bookmarks, in-note search | thumbnail list/grid, All Pages / Bookmarks / Notes switch, Select, Add Page | — |
| S12 | Note Switcher | swipe from the left edge inside a note | jump between notes, open a second note | vertical thumbnail strip, long-press menu "Open On Right/Bottom" | — |
| S13 | Multi-Note split | from S12 | two notes side by side or top/bottom | two editors, divider, Switch Notes / Switch Orientation | left-right, top-bottom |
| S14 | Zoom View | toolbox zoom icon, or tap and hold while writing | write large in a bottom window that maps to a small box | zoom pane, target box, return/advance buttons, anchor handle | — |
| S15 | Import sheet | long-press +New > Import, or the share sheet | bring in PDF, PPT, images | source list (Files, Dropbox, Drive…), add-space option (None/Left/Right/Both) | — |
| S16 | Export / Share | share icon or Options > Export Options | PDF / Note / JPEG / PNG | format picker, "More options" (paper toggle), Apple share sheet | — |
| S17 | Search results | library search bar / ⌘F | find text and handwriting | results pane on the right, folder filter | no results, results |
| S18 | Settings | gear in the library | defaults, gestures, Pencil, sync, backup | grouped lists | — |
| S19 | Recently Deleted | Settings > Recently Deleted | restore within 30 days | list, Recover | empty, filled |
| S20 | Paywall / upsell | hitting the free note limit, banners | sell Plus/Pro | plan cards | read-only state on notes (reviews) |
| S21 | Mac window | Mac app (Catalyst-style, shares iPad UI) | same library + editor; Open in a New Window instead of in-app split | menu bar, keyboard shortcuts | — |

## Flows

```
F01 Start a new handwritten lecture note
    S02 -> tap +New (1) -> S05 opens on the default paper -> write
    happy path taps: 1 (with a default template set). If you set paper per note: +1 on the bottom chip (S04)
    edge: free tier's 5-note limit turns notes read-only (S20); a Home tab added in v16.7 puts the library 2 taps away (review 14511238925)

F02 Write continuously across pages
    S05: write and scroll with one finger; ink crosses the page boundary in Seamless view; a new page appears automatically at the end
    happy path taps: 0
    edge: scrolling with the Pencil draws instead (review 14555153463); one-finger scroll stopped working with the text tool selected (review 14531720276)

F03 Switch pen / colour / eraser mid-sentence
    Pencil Pro: squeeze-and-hold = eraser, release = back (option 1), or squeeze = palette/arc menu (options 4/5)
    Gen-2: double-tap = current tool <-> eraser
    Toolbox: tap tool (1); tap again for colour/size (2)
    Auto-deselect eraser: after one erase it jumps back to the previous pen
    happy path: 0 taps (squeeze) / 1 tap
    edge: a 2026 update removed or changed the squeeze/long-press eraser default and users complained (reviews 14224928960, 14191516223)

F04 Undo / redo
    2-finger tap = undo, 3-finger tap = redo (or 3-finger swipe left/right)
    happy path taps: 1 gesture

F05 Draw a clean diagram (axes, curves)
    Draw a line or shape, hold the nib about 1 s -> it snaps to a straight line or perfect shape; red snapping guides align to the grid; edit points afterwards
    happy path: 0 extra taps
    edge: no toggle for snapping strength or hold time (review 14517812495); no layers (review 14530082754)

F06 Lasso, move and convert
    Select tool (1) -> circle ink -> menu: move/resize/colour/Convert > Text or Math (2-3)
    Math becomes a scalable image with editable LaTeX (paid tier)

F07 Annotate lecture slides (PDF)
    Long-press +New (1) -> Import (2) -> Files (3) -> pick file (4) -> optional add-space margin (5) -> S05 with PDF pages as background
    Mac: drag a PDF onto the library or an open note (appends at the end)
    edge: very large PDFs drain the battery (review 14584607281); before v16.13 imported PDFs could land above the last page

F08 Export a note as PDF
    In note: share icon (1) -> destination in share sheet (2). Or Options > Export Options > PDF > More options (paper on/off)
    happy path taps: 2

F09 Organise into folders
    Sidebar + (1) -> Add Folder (2) -> name; long-press a note -> drag onto folder
    Nest: long-press folder -> Insert Folder; up to 6 levels
    edge: a note can't share a name with another note even in a different folder (reviews 13405930593, 14593065639); no manual sort inside a folder (review 14634524612)

F10 Find something you wrote
    Library search bar (1) -> type -> results on the right -> tap result
    Handwriting search: the pricing page lists "Instant handwriting search" in Plus
    edge: search on one device but not another (review 14547533538)

F11 Two notes at once (textbook + notes)
    In a note: swipe from the left edge (1) -> long-press a thumbnail (2) -> Open On Right / Bottom (3)
    Switch orientation: long-press the open note's thumbnail -> Switch Orientation
    Mac: right-click a note -> Open in a New Window

F12 Sync and recover
    iCloud: Settings > Connected Services > iCloud Syncing toggle. Two-way; deleting in iCloud deletes in the app
    Version history: long-press note -> iCloud Version History -> restored as a separate note (renaming wipes history)
    Notability Cloud (2025-26): account login required; iCloud sync is unavailable once migrated
    edge: many 2026 reviews report notes or folders vanishing during the migration (see fixes.md)
```

## Components

| component | variants | states | used on |
| --- | --- | --- | --- |
| Toolbox strip | default, customised (duplicated pens, hidden tools), swipe for more | selected tool, open popover | S05, S06, S13 |
| Tool popover | pen/pencil/highlighter (colour, size, style), eraser (partial/whole, size) | open/closed | S05 |
| Colour row | 8 pinned + custom | selected | S07, S08 |
| Arc / radial menu | squeeze | open near the nib | S08 |
| Lasso action menu | ink, image, text, PDF | — | S09 |
| Paper chips | Rule, Grid, Dot, Scan, Import, Templates | first-open only | S04 |
| Sidebar tree | smart lists, nested folders with disclosure arrows, colour bullets | expanded, collapsed, selected, count | S02 |
| Note card | grid thumbnail, list row | selected, swipe-to-delete, long-press menu | S02, S12, S17 |
| Thumbnail strip | page thumbnails, note thumbnails | dragging, bookmarked | S11, S12 |
| Split container | left-right, top-bottom | resizing | S13 |
| Zoom pane | target box + writing pane | advancing | S14 |
| Share/export sheet | format list + system share | — | S16 |
| Upsell banner / paywall | inline card, modal | — | S01, S02, S20 |
| Context menus (long-press / right-click) | note, folder, page | — | S02, S11 |

## Inferred data model

```
Folder     id, parent_id (null = root), name (duplicates allowed), colour?, emoji?, locked, sort_order, depth <= 6
           evidence: src 5 (folders), src 6 (dividers -> folders migration)
           confidence: high (fields), medium (sort_order)

Note       id, folder_id (null = Unfiled), title (unique across the library, reviews), created_at, modified_at,
           favourite, view_mode (seamless | single_page), template_id, page_size, handwriting_language,
           locked?, deleted_at (30-day trash)
           evidence: src 4, 7, 9, 16, 20; reviews 13405930593
           confidence: high

Page       id, note_id, index, background (template | pdf_page ref | scan), bookmarked, rotation (PDF pages)
           evidence: src 18 (add/delete/clear/rotate/copy background/bookmark)
           confidence: medium. Seamless view suggests pages are fixed-size and stacked vertically, with ink allowed to cross the boundary (Goodnotes-board comment). So ink may be stored per note in note coordinates rather than per page: guess

Stroke     id, note_id/page_id, tool (pen | pencil | highlighter | calligraphy), colour, width, style (solid|dashed|dotted),
           points [x, y, pressure, tilt?, t], is_shape (shape kind + control points), locked
           evidence: src 11, 13 (partial erase leaves editable segments => strokes are split on erase), src 14
           confidence: medium

MediaItem  id, note_id, kind (image | text_box | sticky | math_image(latex) | audio_marker | tape), frame, z_order
           evidence: src 3, 20, 28
           confidence: medium

Template   id, kind (basic: rule|grid|dot|plain, gallery, custom-from-pdf), size (Letter..A7, "Letter Optimized"), orientation, colour, spacing (1..10)
           evidence: src 16
           confidence: high

Recognition index  note_id, page, text, bbox — built on device (2018 handwriting search), now gated to Plus
           evidence: pricing, src 19, src 30
           confidence: medium

Sync       iCloud (per-note files in the app container, two-way) OR Notability Cloud (account, server); version history (iCloud, or 7/30/90 days by plan)
           evidence: src 24-26, pricing
           confidence: high for behaviour, guess for file layout
```

Relationships: Folder 1-n Folder (≤6 deep), Folder 1-n Note, Note 1-n Page, Note 1-n Stroke (or Page 1-n Stroke), Note 1-n MediaItem, Note n-1 Template.

## Feature matrix

See `features.csv`. Must: 33, should: 22, could: 16, skip: 14 (85 rows).

## Out of scope (cannot or should not be cloned)

- Notability Cloud, accounts, live collaboration, shared libraries: these need a server, and Inkwell has a no-server rule.
- AI (summaries, chat, quizzes, flashcards, "Learn"), audio transcription: skip, or later on-device only.
- Gallery marketplace and community templates: licensed content. Inkwell makes its own papers.
- Business plans, LMS calendar, iPhone/Android/web apps.
- Names, icons, sticker packs, template art and marketing copy: never copied.

## Size

Screens 21, flows 12, entities 7.

Hard parts:
1. Low-latency PencilKit-or-custom ink with pressure and tilt, and erasing part of a stroke without altering the originals. The Inkwell rule means erasing hides ranges and never rewrites points.
2. A seamless vertical document where ink crosses page boundaries but pages stay iPad-shaped for PDF export.
3. Sync through an iCloud Drive folder with per-note files, conflict copies and no data loss. This is the area where Notability's users are angriest.
4. On-device handwriting recognition for search with cursive and maths.
5. Shape snapping plus a neatening layer that can be reversed.
6. Split view on Catalyst.

Size: **L** for the full slice (a quarter). An M-sized thin slice works: library + seamless note + 3 pens/2 highlighters + eraser + lasso + PDF import/export.
