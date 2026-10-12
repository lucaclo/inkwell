# GoodNotes: what users hate, what's missing, what's unsolved, and what Inkwell should take from it

Sample: **553 unique items from 4 sources**:
- 500 App Store reviews from Apple's official customer-reviews RSS feed: the 250 most recent each from the US and GB storefronts, dated 2025-10-27 to 2026-10-11. Star split: 1★ 214, 2★ 62, 3★ 61, 4★ 50, 5★ 113.
- 24 Hacker News comments via the Algolia API.
- 16 Trustpilot reviews (all the 1–3★ ones listed, read in the browser).
- 14 ideas from the official feature-request board, with vote counts (one duplicate text was removed by `reviews.py`).

Reddit could not be reached. It returned HTTP 403 to its JSON endpoint, and the browser extension blocks reddit.com. I did not use third-party mirrors. Each App Store link goes to that storefront's review page, and the exact review id is in `reviews.csv` (column `review_id`).

How to read the counts:
- "n hits" comes from targeted keyword matching over all 554 rows, and I checked a sample by hand. It is an estimate, not an exact tally.
- The theme table from `reviews.py` is in `feedback.md`.
- The App Store sample skews recent and negative. It covers the year after the Oct-2025 redesign and the paywall change. The all-time average is still 4.72★ from 461k ratings.

## 1. What users hate (ranked by evidence)

| # | problem | hits | sources | quotes |
| --- | --- | --- | --- | --- |
| 1 | **Paid once, now locked**: free tier is 3 files, old notebooks go read-only, Goodnotes 5 buyers asked to pay again | 97 match price/paywall, 50 match "already paid / lifetime / read-only / 3 notebooks" | app-store, trustpilot, HN | "3 years of work gone down the drain!" ([GB 14419086064](https://apps.apple.com/gb/app/goodnotes/id1444383602?see-all=reviews)) · "now all my docs/schoolwork are view only" ([US 14601639394](https://apps.apple.com/us/app/goodnotes/id1444383602?see-all=reviews)) |
| 2 | **Bugs that eat content**: erased ink comes back, pages blank, work deletes itself, copy/paste crashes | 81 bugs/crash; 30 match vanish/come-back/lost | app-store, trustpilot, HN | "If I clear a page, the content I’ve deleted comes back. And nothing saves." ([GB 14505540329](https://apps.apple.com/gb/app/goodnotes/id1444383602?see-all=reviews)) · "I will do an entire problem and it will start to delete itself" ([US 14586165034](https://apps.apple.com/us/app/goodnotes/id1444383602?see-all=reviews)) |
| 3 | **Toolbar redesign and tool snap-back**: the floating toolbar covers the page, tools move between updates, and after a text box the app falls back to Lasso | 16 toolbar + 13 lasso hits; board: 640 votes (revert toolbar), 543 votes (stop lasso default) | app-store, board | "now every-time I finish one text box lasso is then automatically switched on" ([GB 13530820077](https://apps.apple.com/gb/app/goodnotes/id1444383602?see-all=reviews)) · "You get used to where your eraser pen is and then they move it every week." ([US 14492079165](https://apps.apple.com/us/app/goodnotes/id1444383602?see-all=reviews)) |
| 4 | **AI forced in, can't be turned off**, plus credit and upsell pop-ups | 38 hits | app-store, trustpilot, HN | "it’s not possible for me to use the app where AI tools are forced on me and can’t be switched off" ([GB 14559471556](https://apps.apple.com/gb/app/goodnotes/id1444383602?see-all=reviews)) |
| 5 | **Sync unreliable or coerced**: iCloud loss, false "sync failed", Mac shows missing pages, pressure to move to their own cloud | 29 hits | app-store, HN, board | "Lost ALL my notes because of poor iCloud sync." ([GB 14048693273](https://apps.apple.com/gb/app/goodnotes/id1444383602?see-all=reviews)) · "still shows 23 pages when there are 28 pages" ([US 14554792673](https://apps.apple.com/us/app/goodnotes/id1444383602?see-all=reviews)) |
| 6 | **Mac (and non-iPad) version is second-class**: no undo button, few shortcuts, typing jumps, crashes | 30 hits | app-store, HN, trustpilot | "THERE ISNT AN UNDO OR REDO BUTTON ON COMPUTER." ([US 14472739186](https://apps.apple.com/us/app/goodnotes/id1444383602?see-all=reviews)) · "Good notes has a great iPad and iPhone app, but the Mac app is awful." ([US 14608402390](https://apps.apple.com/us/app/goodnotes/id1444383602?see-all=reviews)) |
| 7 | **Ink quality**: stroke flicks and artefacts, lag, predicted strokes left in the ink, some prefer competitors' rendering | 18 hits (avg rating higher: "love it, but") | app-store, HN, board, trustpilot | "predicted strokes get baked into the final result even with stroke correction off" ([US 14515779886](https://apps.apple.com/us/app/goodnotes/id1444383602?see-all=reviews)) · "I’ve turned stroke stabilisation [line break] down to zero but still at the end of letters the writing changes direction." ([GB 14103364800](https://apps.apple.com/gb/app/goodnotes/id1444383602?see-all=reviews)) |
| 8 | **Overheating, battery drain, slow on big documents** | 31 performance hits | app-store, trustpilot | "my iPad immediately starts to get hot enough to fry an egg" ([GB 14626855994](https://apps.apple.com/gb/app/goodnotes/id1444383602?see-all=reviews)) |
| 9 | **Forced sign-in and session expiry**, including offline | 13 hits | app-store, trustpilot | "it frequently says “Login session expired” and needs me to sign back in" ([US 14468270192](https://apps.apple.com/us/app/goodnotes/id1444383602?see-all=reviews)) · "sign in, sorted… but I had no internet" ([GB 13487038665](https://apps.apple.com/gb/app/goodnotes/id1444383602?see-all=reviews)) |
| 10 | **Gesture misfires while writing**: palm triggers long-press popups or the lasso, accidental undo, no off switch | 7 hits (thin-ish) + board 136 votes | app-store, board | "the option for (zoom, add comments) keeps popping up and messing up my flow" ([US 14598382353](https://apps.apple.com/us/app/goodnotes/id1444383602?see-all=reviews)) |
| 11 | **Shapes/snapping regressions**: arcs forced to ovals, guides stop free placement | 10 shape hits | app-store | "Can no longer ‘snap’ 3/4 shapes, they autocorrect to ovals (RIP Chemistry notes)" ([GB 13376109284](https://apps.apple.com/gb/app/goodnotes/id1444383602?see-all=reviews)) |
| 12 | Support only via bot and slow tickets | 22 | app-store, trustpilot | n/a for Inkwell (personal app) |

## 2. What is missing (asked for by name)

| # | request | evidence | quotes |
| --- | --- | --- | --- |
| 1 | **Handwriting neatening / beautification** (live, keeps your own style) | 8 review hits (avg 3.7★, i.e. "love it, but") + board: Auto-refine Handwriting 452 votes, Personal Handwriting Model 25 votes | "I can give 5 stars if you all add real time hand writing beautify mode" ([US 14512277538](https://apps.apple.com/us/app/goodnotes/id1444383602?see-all=reviews)) · "a way to straighten handwritten text in different languages — both the lettering itself and its alignment with the lines, so it doesn’t end up crooked when writing by hand" ([US 14609227665](https://apps.apple.com/us/app/goodnotes/id1444383602?see-all=reviews)) |
| 2 | **Notes as plain files in iCloud Drive / Files** | board 697 votes | "I'd like for my notes to be accessible through the apple files app" ([board](https://feedback.goodnotes.com/forums/191274-customer-suggestions-for-goodnotes/suggestions/50653646)) |
| 3 | **Faster navigation**: a way back to the open document, a persistent sidebar, one-tap bookmark, pinnable tabs | 2–4 reviews + board 337 (sidebar), 733 (bookmark icon), 161 (pin tabs) | "please add a one-click way to return to open documents" ([US 14636774576](https://apps.apple.com/us/app/goodnotes/id1444383602?see-all=reviews)) |
| 4 | **Continuous scrolling / no hard page breaks**; dual-page view | board 371 (continuous), 1,399 (double-page); 1 review | "CAN YOU GUYS PLEASE MAKE A DUAL PAGE VIEW OPTION?" ([US 14486786569](https://apps.apple.com/us/app/goodnotes/id1444383602?see-all=reviews)) |
| 5 | **Export a page range** | 2 reviews (both 4★) | "you can either only export a single page or all the pages" ([US 14611161412](https://apps.apple.com/us/app/goodnotes/id1444383602?see-all=reviews)) |
| 6 | **Better undo/redo gestures and gesture toggles** | board 272 + 136 votes | "Subsequent undo actions: Single tap with two fingers" ([board](https://feedback.goodnotes.com/forums/191274-customer-suggestions-for-goodnotes/suggestions/50957381)) |
| 7 | **Focus / full-screen writing mode** | board 1,084 votes, 1 review | "Application needs a focus/fullscreen mode where the page tabs disappear" ([GB 13939337189](https://apps.apple.com/gb/app/goodnotes/id1444383602?see-all=reviews)) |
| 8 | **Recognition that handles capitals and cursive; global spellcheck-off** | 3 capital-letter reviews; 1 cursive; 1 spellcheck | "No matter how big I try to make the letter look it always ends up being lowercase." ([GB 14585840447](https://apps.apple.com/gb/app/goodnotes/id1444383602?see-all=reviews)) |
| 9 | Maths/science writing aids: subscript/superscript, more shapes (arcs, sectors), shape width = pen width | board 277, 619, 103 votes | "it would be very useful for those of us doing chemistry" ([board](https://feedback.goodnotes.com/forums/191274-customer-suggestions-for-goodnotes/suggestions/50957591)) |
| 10 | Colour palettes / grouped colours; highlighter size; rectangle highlighter | board 642, 461 votes; 1 review | "Please give an option to change size of highlighter" ([US 14592323145](https://apps.apple.com/us/app/goodnotes/id1444383602?see-all=reviews)) |

Thin items (fewer than 3 reviews, or only one source): export page range, highlighter size, capitals. These are listed for Luca's needs, not as trends.

## 3. What is unsolved (whole jobs or groups the app ignores)

1. **People who want a private, local, buy-once notebook with no account.** Paywall, sign-in, AI and cloud-coercion complaints together are the largest block of negative reviews. "My notes are private and I don't want to give them to you." ([Trustpilot](https://www.trustpilot.com/reviews/655f516f5af42e020cb3ae75)). An HN builder: "Notability/Goodnotes seem to have become overly bloated" ([HN 46310152](https://news.ycombinator.com/item?id=46310152)). **Inkwell is exactly this by design.**
2. **Ink-first writers.** The pen feel is treated as finished while the roadmap goes to AI. "For a handwriting app, the pen feel should come first." ([US 14515779886](https://apps.apple.com/us/app/goodnotes/id1444383602?see-all=reviews)). An M5 + Pencil Pro owner rates the writing below cheaper rivals ([GB 14374604818](https://apps.apple.com/gb/app/goodnotes/id1444383602?see-all=reviews)).
3. **STEM / maths note-takers.** There is no maths awareness. "Neither app can recognize math" ([HN 18757865](https://news.ycombinator.com/item?id=18757865)), and the shape regressions hit chemistry and economics-style diagrams. Inkwell's "skip maths when neatening" is a small but real answer.
4. **Mac as a real second workspace.** The iPad is fine and the Mac is "only helpful to see what I did on iPad" ([GB, 2026-05-14, see reviews.csv](https://apps.apple.com/gb/app/goodnotes/id1444383602?see-all=reviews)).
5. **Data ownership.** The proprietary format pushed one user to reverse-engineer it "to unlock .goodnotes files" ([HN 49377665](https://news.ycombinator.com/item?id=49377665)). Inkwell's files-in-a-folder approach solves this.
6. Smaller groups: left-handed writers ([US 14647488523](https://apps.apple.com/us/app/goodnotes/id1444383602?see-all=reviews)), RTL/Arabic, older users wanting simpler UI (2 reviews). Thin, and not Luca's needs.

## Fix plan for Inkwell (top items, evidence × cheapness)

| # | build/change | size | evidence | features.csv row |
| --- | --- | --- | --- | --- |
| 1 | Append-only stroke log per page, plus file-coordinated saves to the iCloud Drive folder, plus conflict copies, never silent overwrite. Trash for pages and docs | L | hate #2, #5; 697-vote idea | "Conflict copies...", "Documents visible as files..." |
| 2 | Fixed slim toolbar (3 pens + 2 highlighters + eraser + lasso + text). The selected tool stays selected until Luca changes it. No auto-fallback | S | hate #3 | "Lasso never becomes the sticky fallback tool" |
| 3 | Ink pipeline: predicted touches drawn transiently and replaced by actual samples, stabilisation default 0, latency budget tested on M4/M5 | M | hate #7 | "Stroke stabilisation setting..." |
| 4 | Live reversible neatening as a render transform over the untouched strokes, line by line, maths skipped, toggle per page | L | missing #1 | "Live reversible line-by-line neatening" |
| 5 | Gesture settings: undo/redo taps on/off, no long-press popups on the canvas, palm never switches tools | S | hate #10 | "Gesture toggles" |
| 6 | Mac Catalyst: visible undo/redo, ⌘Z/⇧⌘Z, ⌘F, arrow-key page nav, drag-drop PDF | M | hate #6 | "Mac app with undo/redo..." |
| 7 | Export dialog with page range + flattened PDF with recognised-text layer | S | missing #5 | "Export arbitrary page range" |
| 8 | "Back to last document" button in the library + recent docs | S | missing #3 | "Return to last open document..." |

Angle (for Luca's own use, not for sale): *for a writer who hated losing notes and fighting the toolbar, Inkwell keeps every stroke as a file he owns, never changes tools behind his back, and neatens without touching the original.* Evidence: hate #1–#3 and #5, about 200 keyword hits across 3 sources.

## Ideas for Inkwell: what GoodNotes does brilliantly

These are patterns to learn from. Rebuild them clean, with no names, icons, templates or copy taken.

1. **Draw-and-hold to snap, with no tool switch** (help: Shapes). Draw a line or shape with the normal pen, keep the tip down, and it snaps clean. While still holding, you can adjust scale and angle, then lift to commit. That's 0 extra taps for axes, supply/demand lines and boxes. **must**
2. **Undo/redo anywhere with finger taps.** Two-finger double tap undoes, three-finger redoes, without putting the Pencil down. Inkwell should add the board's improvement: after the first double tap, single taps repeat. Also add an off switch. **must**
3. **A palette at the pencil tip.** Squeeze pops a compact palette with tool, colour, thickness and undo where the pencil is, so your eyes stay on the page. Inkwell puts this on double-tap (squeeze = eraser), but keeps the "appears at the tip, disappears on next stroke" behaviour. **must**
4. **Edit Handwriting: reflow and straighten** (help: lasso). Lasso some handwriting, choose straighten, and multiple lines level out. Drag a side handle and the words reflow like text. This is GoodNotes's manual, after-the-fact version of Luca's neatening. Inkwell should do it live and reversibly, and could borrow the "drag width to reflow" handle for selections. **should**
5. **Sidebar as the page manager.** Thumbnails with drag-reorder, a "Bookmarks only" filter, multi-select (move/copy/rotate/export/trash), and an Outline tab that auto-imports a PDF's table of contents. Navigating a long notebook takes 2 taps. **must**
6. **Template per page, decided at the moment of adding.** The Add Page menu picks position (before/after/end) and paper in one sheet, and Change Template swaps an existing page's paper, colour, size and orientation. This matches Luca's lined/grid/blank per new page; 1 tap if the menu remembers the last choice. **must**
7. **One search box for everything**: handwriting, typed text, PDF text layer, titles and outlines. Tapping a hit opens the exact page. The flattened PDF export can embed the recognised handwriting so the PDF stays searchable outside the app. **must**
8. **Import straight into the current document at a position** (after current page, before, or end), with drag-and-drop on iPad and Mac. Lecture slides drop into the lecture notebook. **should**
9. **Scroll direction per document with a global default.** Lets Luca default to vertical but flip a PDF to paging. **could**
10. **Backup as a separate, one-way, readable copy** (Auto Backup to a chosen folder as native file, PDF or both, with a "-exclude" naming trick). For Inkwell this means an optional PDF mirror next to the source files in the iCloud folder, so the notes are readable even without Inkwell. **should**
11. **Hover preview** on M-series iPads: the stroke colour and width show before touching down. Cheap delight. **should**
12. **Zoom window for small writing** (cited by an HN maths user, [HN 6433723](https://news.ycombinator.com/item?id=6433723)). Useful for dense equations. **could**

## Pitfalls Inkwell must avoid

1. **Never switch tools on Luca's behalf.** No reverting to lasso, and the palm never selects a tool. (543-vote idea, 13 lasso hits.) **must**
2. **Never move or re-layout tools between versions.** Muscle memory is the product. Ship one toolbar layout and leave it alone. (Toolbar complaints, 640-vote revert idea.) **must**
3. **Never lose or resurrect ink.** No erased strokes reappearing, no blank pages after relaunch, no "deleted the wrong pages" with no undo after leaving the doc. Use an append-only log, undo that survives closing the document, and Trash for pages. ([GB 13388593445](https://apps.apple.com/gb/app/goodnotes/id1444383602?see-all=reviews)) **must**
4. **Never let predicted or smoothed points persist.** Predicted touches are display-only, and stabilisation is opt-in. (Ink-quality complaints.) **must**
5. **No sign-in, no session, no server, ever.** Writing must work offline from a cold launch. (13 sign-in hits.) **must**
6. **Sync honesty.** Show true sync state per document. Never report a false failure. Never show a document with fewer pages than exist without saying it's still downloading. (us 14541754938, us 14554792673.) **must**
7. **Mac must not be a viewer.** It needs undo/redo, shortcuts, and stable scroll position while editing. **must**
8. **Big notebooks must not overheat the iPad.** Use tiled, cached page rendering and only keep visible pages live. Test a 300-page PDF. **must**
9. **No pop-ups over the canvas while writing**: no long-press menus, recognition-language download prompts, red spellcheck dots, or upsells. Recognition runs silently in the background. ([US 14598820803](https://apps.apple.com/us/app/goodnotes/id1444383602?see-all=reviews) on cursive being scanned in "a dozen different languages".) **must**
10. **Snapping must be optional.** Free placement by default; snapping shouldn't fight the hand. Partial arcs mustn't be forced into ovals. **should**
11. **Text tool defaults should be remembered** (font, size, colour), with no re-setting every box. **should**
12. Storage bloat: one review reports 11 GB for two notebooks after deletions. Compact deleted data and show the library size. **could**
