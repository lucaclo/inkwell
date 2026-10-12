# Recon map: Noteshelf 3 (iPadOS + macOS, also iPhone/Watch/Android/Windows)

Scope: the core handwriting slice only. Library and folders, notebook and page editing, pens/eraser/lasso/shapes, templates and paper, PDF import/annotate/export, search, sync and backup, Apple Pencil features, Mac version. AI, template marketplace, sharing, audio and typed docs are only mentioned.
For: Inkwell, Luca's personal handwriting app (iPad Pro M4/M5 + Apple Pencil Pro, plus Mac Catalyst). It is not going on the App Store. The goal is to study patterns, not to copy the app.
Date: 2026-10-12
Method: public sources only. I did not use the app or an account, I saved no screenshots, and I read no code or binaries. **Tap counts are estimates** built from the help-centre step lists. Nobody counted them on a device.

## Sources

| # | source | URL | notes |
| --- | --- | --- | --- |
| 1 | App Store listing + lookup API | https://apps.apple.com/us/app/noteshelf-ai-notes-pdf/id6458735203 , https://itunes.apple.com/lookup?id=6458735203 | v8.0 (2026-10-11), 4.56 stars from 6,951 ratings (US). Min iPadOS 18 / macOS 15. 486 MB |
| 2 | App Store version history + IAP list | same page | 7.x to 8.0 notes: Two-Page View, navigation pill, zoom presets, toolbar at bottom, shape snapping, context menus. IAPs: weekly $7.99, monthly $9.99, yearly $19.99 to $49.99, lifetime $14.99, NS2 upgrade $9.99 |
| 3 | Help centre (Zendesk public Help Center API, 179 articles) | https://noteshelf-support.fluidtouch.biz/api/v2/help_center/en-us/articles.json | The HTML help site sits behind a Cloudflare challenge. The official public JSON API was readable. Key articles are listed below |
| 3a | What's new in NS3 | https://noteshelf-support.fluidtouch.biz/hc/en-us/articles/22024757963929 | customisable toolbar, floating mini toolbar, focus mode, content views, home |
| 3b | Floating mini toolbar | https://noteshelf-support.fluidtouch.biz/hc/en-us/articles/21887313617305 | 3 colour swatches + preset sizes, long-press to edit, eyedropper |
| 3c | Focus mode | https://noteshelf-support.fluidtouch.biz/hc/en-us/articles/21890045420313 | 4-finger tap |
| 3d | Hold to convert to shape / editable shapes | https://noteshelf-support.fluidtouch.biz/hc/en-us/articles/16039616039705 , https://noteshelf-support.fluidtouch.biz/hc/en-us/articles/22746403936793 | |
| 3e | Groups and sub-groups | https://noteshelf-support.fluidtouch.biz/hc/en-us/articles/22521828227609 | drag one notebook onto another |
| 3f | Templates store and custom templates | https://noteshelf-support.fluidtouch.biz/hc/en-us/articles/22808638737689 | Plain/Ruled/Checked/Dotted/Legal + colour, rule size, orientation, device size |
| 3g | Auto-backup (Drive/Dropbox/OneDrive/WebDAV) | https://noteshelf-support.fluidtouch.biz/hc/en-us/articles/49110156650137 | one-way; deletes do not propagate |
| 3h | iCloud sync troubleshooting / launch delay | https://noteshelf-support.fluidtouch.biz/hc/en-us/articles/30505571756569 , https://noteshelf-support.fluidtouch.biz/hc/en-us/articles/32015682831385 | 13-step checklist; app launch blocked on an iCloud error |
| 3i | Notebooks greying out / re-download | https://noteshelf-support.fluidtouch.biz/hc/en-us/articles/360049162614 | iCloud cache eviction |
| 3j | Recover a notebook that won't open | https://noteshelf-support.fluidtouch.biz/hc/en-us/articles/49369264213145 | send the file to support |
| 3k | Saved clips | https://noteshelf-support.fluidtouch.biz/hc/en-us/articles/30438120078873 | lasso, then Save Clip |
| 3l | Bookmarks as TOC, tags, page move/copy | https://noteshelf-support.fluidtouch.biz/hc/en-us/articles/18175000074521 , https://noteshelf-support.fluidtouch.biz/hc/en-us/articles/22809060465561 , https://noteshelf-support.fluidtouch.biz/hc/en-us/articles/4402386285081 | |
| 3m | Writing styles / palm rejection | https://noteshelf-support.fluidtouch.biz/hc/en-us/articles/4411279536281 | 6 hand postures, 3 of them left-handed |
| 3n | Zoom box | https://noteshelf-support.fluidtouch.biz/hc/en-us/articles/4414988800025 | older article; still present per source 4 |
| 3o | Mac keyboard shortcuts | https://noteshelf-support.fluidtouch.biz/hc/en-us/articles/360046216094 | older (NS2-era) article |
| 4 | Paperlike long-form review (2026) | https://paperlike.com/blogs/paperlikers-insights/noteshelf-review | pen types, eraser modes, zoom box options, ruler, tape, pricing |
| 5 | Google Play listing (Android version) | https://play.google.com/store/apps/details?id=com.fluidtouch.noteshelf3&hl=en_GB | Android sells a one-time purchase; iOS is subscription-led |
| 6 | Public reviews (396) | see reviews.csv / feedback.md / fixes.md | |

Could not reach: Reddit (blocked for this browser tool, and the public JSON returned 403), MacRumors forums and Apple Community (bot-verification walls, which I did not try to get past), Trustpilot (no page, 404). I found no public walkthrough video transcript.

## Core loop

Open a notebook from the shelf, then write with Apple Pencil on paper you choose, switching among 3 pens/colours from a mini toolbar. Notes sync through iCloud and you find them later through groups, bookmarks, tags and handwriting search.

## Screens

| ID | screen | route / how to reach | purpose | key components | states seen |
| --- | --- | --- | --- | --- | --- |
| S01 | Shelf (library) | app launch | browse notebooks | sidebar (Home, Unfiled, categories, Content Views: Photos/Recordings/Bookmarks, Tags, Templates, Trash), notebook grid/list with cover thumbnails, sort (last opened/modified/name/custom), + button, search, Quick Note button | empty (free: 3-notebook cap), filled, notebook "greyed out / needs download" (iCloud evicted), launch stuck on spinner / "Retry" (reviews) |
| S02 | Group view | tap a group on S01 | nested folder | same grid, breadcrumb, drag to regroup | empty, filled |
| S03 | New notebook sheet | S01 then + then New Notebook | create a notebook | title, cover picker, paper template row (Plain, Ruled, Checked, Dotted, Legal, More), colour, rule height, orientation, device size | default, custom template, premium-locked (crown) |
| S04 | Template store / library | S03 More Templates, or sidebar Templates | browse and save templates | categories, fullscreen preview, Library, Custom (import PDF/image/camera) | locked/unlocked, downloading |
| S05 | Cover picker | S03 or long-press notebook then Change Cover | personalise | built-in covers, photo, Unsplash search, writable cover | default, custom |
| S06 | Notebook editor | tap a notebook | write | top toolbar (customisable; can sit at top or bottom), floating mini toolbar (3 colours + sizes), navigation pill bottom-left (vertical / horizontal / two-page, zoom presets), page canvas | editing, read-only, focus mode, loading, "please update the app to open" (reviews) |
| S07 | Pen rack | tap the pen tool again | configure pen | pen types (ball, felt, fountain, pencil), size presets + slider (0.1 mm steps), colour grid + hex/custom, pressure toggle, hold-to-convert-to-shape toggle, favourites | |
| S08 | Highlighter rack | highlighter, tap again | | round/chisel tip, 3 sizes, fixed translucency, "draw straight lines" | |
| S09 | Eraser options | eraser, tap again | | 3 sizes + auto, erase whole stroke, erase highlighter/pencil/tape only, clear page, auto-return to previous tool | |
| S10 | Lasso + context menu | lasso, then encircle | edit selection | move/resize, colour, convert to text, save clip, screenshot, send to back/front, cut/copy/delete (icon menu since 7.3/7.4) | |
| S11 | Shapes panel | shapes tool | geometric shapes | presets (line, arrow, rectangle, circle, polygons), freeform, shape snapping (7.6.1), editable handles | |
| S12 | Add (+) menu | toolbar + | insert | page, page from template, import document (PDF/Word/PPT/images), photo, camera/scan, audio, text box, sticker/emoji, saved clips, web clip | |
| S13 | Page thumbnails ("Finder") | 4-squares icon | navigate pages | thumbnail grid (2 columns since a 2026 update), bookmark toggle per page, Edit (multi-select: move, copy, tag, trash), filter (bookmarked/tagged), search in notebook, outline for PDFs | |
| S14 | Zoom box | More, then Zoom Box toggle, then magnifier icon | write large, render small | blue target rect on page, magnified lower panel, margins, line spacing, auto-advance, resize handle | |
| S15 | Focus / read-only / presentation modes | 4-finger tap; ROM icon; More, then Present | distraction-free / review / external display | hidden chrome, tap to reveal, laser pointer | |
| S16 | Global search | search on S01 | find anything | query field, tag suggestions, results across handwriting (60+ languages), typed text, PDF text | indexing, no results |
| S17 | Settings | 3-dot, then Settings | configure | Sync & Backup (Use iCloud, auto-backup provider, export all data), Handwriting (6 writing styles, recognition language), Apple Pencil (pressure, double-tap action), appearance (light/dark), Help (logs, contact) | |
| S18 | Toolbar customisation | long-press toolbar, or More | choose tools | add/remove/reorder tools | |
| S19 | Export / share sheet | long-press notebook, Share; or in notebook | export | scope (current/selected/all pages), format (PDF, image, native), include template/cover/page numbers toggles | |
| S20 | Notebook options | long-press notebook | manage | rename, move, duplicate, tag, password/Face ID lock, open in new window, pin, delete | |
| S21 | Trash | sidebar | recover | deleted notebooks/pages, recover | |
| S22 | Mac window (Catalyst-style) | macOS app | same as iPad | menu bar, keyboard shortcuts, multiple windows | black screen with "Retry" (reviews) |
| S23 | Paywall | any premium item (crown) | upsell | weekly/yearly plans, trial | |
| S24 | Migration from NS2 | NS2 settings | one-way import | progress, "stuck on one book" | |
| S25 | AI panel (out of scope) | toolbar AI | summarise/explain/translate | | |

## Flows

```
F01 Create a lined notebook and start writing
    S01 -> S03 -> S06
    happy path taps: 4 (+, New Notebook, pick Ruled, Create) - estimated
    edge: free tier hits 3-notebook cap; premium templates locked; new-page orientation bug (gb review 2025-11-20)

F02 Quick note
    S01 Quick Note button -> S06
    happy path taps: 1 (settings remembered from last time: size, line height, colour, orientation)

F03 Add a new page with a different paper
    S06 + -> Page from template -> pick -> S06
    happy path taps: 3 (plain "Page" = 2; in vertical scroll a swipe past the last page was removed, per a reviewer: "New page is a switch and a tap")
    edge: template must be created from the shelf to show up inside a notebook

F04 Switch pen / colour / size while writing
    S06 mini toolbar
    happy path taps: 1 (tap swatch or size). Pen type change: 2 (pen tool, pick type in S07)
    edge: only 3 quick colours; mini toolbar covers content; Pencil Pro squeeze menu appears mid-screen (bug)

F05 Erase
    S06 eraser (1 tap) or Pencil double-tap (configurable), auto-returns to previous tool after one stroke (optional)
    happy path taps: 1 (0 with Pencil gesture)

F06 Draw a clean shape (economics diagram axes)
    S06 pen -> draw -> hold at end -> shape snaps -> long-press to edit handles
    happy path taps: 0 extra (hold gesture)
    edge: auto-shape fires unintentionally; undo removes the drawing too (us review 2025-12-23)

F07 Move / recolour handwriting
    S06 lasso -> encircle -> S10 menu
    happy path taps: 2-3

F08 Import a PDF and annotate
    S01 + -> Import Document -> Files picker -> S06
    happy path taps: 3-4
    edge: imported PDFs/images look blurry (2 GP reviews); duplicates when used as default PDF viewer

F09 Export pages as PDF
    S06 share -> scope -> PDF -> share sheet
    happy path taps: 3-4
    edge: exported strokes look different from on-screen (us review 2026-02-03); highlighter exports as outline (GP)

F10 Organise: make a nested group
    S01 drag notebook onto another notebook -> group; inside group drag again -> sub-group
    happy path: 1 drag
    edge: cannot group from Home; categories cannot nest (Paperlike)

F11 Find a handwritten word
    S01 search -> type -> result -> S06 at page
    happy path taps: 3
    edge: indexing delay

F12 Bookmark as chapter / TOC
    S13 bookmark icon on thumbnail; long-press -> name + colour; filter -> Bookmarked -> List view
    happy path taps: 2 (bookmark), 5 (named TOC entry)

F13 Write in zoom box
    More -> Zoom Box toggle -> magnifier
    happy path taps: 3 first time, then 1
    edge: icon moved to More menu in an update

F14 Turn on backup
    3-dot -> Settings -> Sync & Backup -> Auto Backup -> toggle -> provider -> sign in
    happy path taps: 6+
    edge: one-way only; first backup needs the app kept open; NS3 backups failing for some notebooks (GP 2026-07-05); restore fails (us 2026-06-23)

F15 Recover a notebook that won't open
    long-press -> Share .nsa -> email support with logs
    happy path: there is no self-serve repair
```

## Components

| component | variants | states | used on |
| --- | --- | --- | --- |
| Top toolbar | top / bottom placement, customisable tool set | normal, hidden (focus/ROM) | S06 |
| Floating mini toolbar | vertical left/right, horizontal under main bar, minimised | 3 swatches, 3 sizes, custom colour, eyedropper | S06 |
| Navigation pill | vertical / horizontal / two-page; zoom presets | | S06 |
| Tool rack popover | pen, highlighter, eraser, shapes | selected type, size slider | S07 to S11 |
| Colour swatch | preset, custom, edit, restore default | selected, long-press edit | S06, S07 |
| Notebook tile | cover thumbnail, title, date | downloaded, greyed (cloud-only), locked, pinned | S01, S02 |
| Sidebar | iPad / Mac | collapsed, expanded | S01 |
| Context menu | notebook, page thumbnail, lasso selection (icons since 7.3) | | S01, S10, S13 |
| Template card | basic, store, custom | premium crown, downloading | S03, S04 |
| Page thumbnail | bookmark flag (colour, name), tags | selected | S13 |
| Zoom box | target rect + magnified pane | auto-advance | S14 |
| Paywall sheet | plans | trial | S23 |

## Inferred data model

```
Library        settings, iCloudEnabled, backupProvider, writingStyle (6), recognitionLanguage
               evidence: S17, help 3g/3h/3m           confidence: high
Category       id, name, order  (top-level shelf section; cannot nest)
               evidence: Paperlike, help "Categorize Shelves"     confidence: high
Group          id, name, parentGroupId?, categoryId, order (nests arbitrarily)
               evidence: help 3e                     confidence: high
Notebook       id, title, coverId|customCover(image, writable), categoryId, groupId?,
               defaultTemplate, password?/biometric, pinned, tags[], createdAt, modifiedAt,
               lastOpenedAt, lastViewedPage? (reviews say it reopens at page 1, so maybe not stored)
               storage: one package file per notebook (.noteshelf iOS / .nsa Android), in the iCloud container
               evidence: S19 export formats, help 3j, 3i            confidence: medium
Page           id, notebookId, index, template(type, colour, ruleHeight, orientation, size)|pdfPageRef,
               bookmark{name, colour}?, tags[], rotation
               evidence: help 3l, 3f, Paperlike         confidence: high
Annotation     id, pageId, kind (stroke | highlighter | shape | text | image | sticker | audio | tape | link),
               z-order (send to back / bring to front)
Stroke         points(x,y,pressure,time?), penType(ball|felt|fountain|pencil), colour, width, lineStyle(solid|dotted|dashed)
               evidence: S07, Paperlike    confidence: medium (point fields are a guess)
Shape          kind(preset|freeform), controlPoints, rotation, fromHoldToConvert(bool)
               evidence: help 3d          confidence: medium
SavedClip      id, category, payload(annotations)      evidence: help 3k   confidence: high
FavoritePen    penType, colour, width, order (NS2 favourites migrate to "Favorites" tool)
               evidence: migration guide   confidence: high
SearchIndex    pageId, recognisedText, language   evidence: S16   confidence: medium
Backup         one-way mirror per notebook in PDF or native format; deletes are not propagated
               evidence: help 3g          confidence: high
```

Relationships: Library 1-n Category 1-n Group (self-nesting) 1-n Notebook 1-n Page 1-n Annotation; Notebook n-n Tag; Page n-n Tag; Page 0-1 Bookmark.

## Apple Pencil support (what is verifiable)

- Pressure toggle and a configurable double-tap action in Settings (Paperlike, source 4).
- **Squeeze (Pencil Pro): supported.** It opens a tool menu around the pen tip. Two US App Store reviews (2026-09-24, 2026-09-21) say the menu often pops up mid-screen instead of at the hover point, and one says the bug has been reported since Nov 2025 and is still unfixed.
- **Barrel roll, hover preview, haptics: no evidence found** in the help centre, App Store page, version history or reviews. Treat them as unsupported or unverified.
- Palm rejection is tuned by picking 1 of 6 hand postures (3 left-handed).

## Sync approach

- iCloud only among Apple devices (an iCloud container, not a user-visible folder). There is no Apple to Android/Windows sync.
- Notebooks can be evicted locally and then "grey out" and need re-download (help 3i, 6 reviews). Launch can block on an iCloud error (help 3h).
- Separate one-way auto-backup to Drive/Dropbox/OneDrive/WebDAV in PDF or native format. Deletes are never pushed to the backup.
- "Export entire data" zip keeps the category/group structure.

## Feature matrix

See `features.csv`. Must: 37, should: 19, could: 15, skip: 11 (82 rows) (priorities are for Luca's Inkwell).

## Out of scope (cannot or should not be cloned)

- Template/sticker/cover marketplace content, Unsplash/Pixabay integrations (licensed content)
- Noteshelf AI (server-side LLM; conflicts with on-device / no-server)
- Collaboration/sharing, Watch app, Android/Windows clients, cross-platform sync
- Subscription/paywall machinery
- Brand assets: names, icons, covers, the "shelf" metaphor art, templates

## Size

Screens 25, flows 15, entities 12. Hard parts:
1. Ink engine quality (pen textures, pressure, latency) that reviewers rate above rivals
2. iCloud Drive file sync that never evicts or loses data
3. Vector-faithful PDF export
4. On-device handwriting recognition for search, with maths skipped
5. Pencil Pro squeeze anchored at the hover point

Inkwell's in-scope slice is about **L** (a quarter). The full Noteshelf surface would be XL.
