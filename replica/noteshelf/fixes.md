# Noteshelf 3: what users hate, what's missing, what's unsolved, and ideas for Inkwell

**Sample:** 396 public reviews.
- 374 from the Apple App Store customer-reviews RSS feed (US 249 + GB 125, 2023-08 to 2026-10; ratings 1★ 132, 2★ 45, 3★ 32, 4★ 38, 5★ 127).
- 18 from Google Play. These are for the **Android** version: same product, different client.
- 4 from Hacker News (Algolia API). They are marginal.

**Unreachable:** Reddit (blocked for the browser tool, 403 on the public JSON), MacRumors and Apple Community (bot-check walls, which I did not try to get past), Trustpilot (no page).

**How the counts were made:** the themed counts come from `feedback.md` (reviews.py with an adapted `themes.json`). The Luca-specific counts below are keyword matches that I then **checked by hand** against the review text. Treat them as approximate (±2).

**Big caveat:** about 120 of the 1–2★ reviews are children or new users angry that templates and stickers sit behind a paywall ("you have to pay"). That dominates the automatic ranking but is irrelevant to a personal app. I list it once and then rank on what matters to Luca.

---

## 1. What users hate (complaints about things the app does)

| # | problem | reviews | sources | relevance to Luca |
|---|---|---|---|---|
| 1 | Paywall, subscription replacing lifetime, $7.99/week | ~126 mention paying; 46 name subscription/lifetime/weekly | 3 | none (personal app). Recorded for completeness |
| 2 | **Crashes that lose recent work, or notebooks that vanish or are wiped** | 18 (hand-checked) | 3 (App Store US, GB, Google Play) | **critical** |
| 3 | **App or notebooks won't open** (launch spinner, "Retry" black screen, "please update the app to open", Mac won't load) | 14 | 2 | **critical** |
| 4 | Support doesn't answer | 26 (reviews.py) | 3 | n/a |
| 5 | **Floating palettes and toolbar covering the page** (added 2025–26) | 8 | 1 store (US+GB) | high |
| 6 | **iCloud offloading**: notebooks evicted, must re-download, slow to open, unusable offline | 6 (+ an official help article) | 1 store (US+GB) | high |
| 7 | AI pushed into the app (privacy, bloat, price) | 7 | 2 | medium (validates on-device-only) |
| 8 | **Zoom changed**: can zoom out below 100%, no snap back, lock disables zoom | 5 | 2 | high |
| 9 | **PDF fidelity**: export doesn't match the screen; imports are blurry | 5 | 2 | high |
| 10 | Auto-shape / lasso misbehaving (unwanted shapes, undo removes the drawing, lasso ignores toggles) | 5 | 2 | high (diagrams) |
| 11 | Pencil Pro squeeze menu appears mid-screen instead of at the pen | 2 (same bug) | 1 | high. **Thin** |
| 12 | Notebook reopens at page 1, not where you left off | 2 | 1 | high. **Thin** |

**#2 Lost work.**
- "The app crashed and it whipped all my notes." (US 2★, 2026-09-24) https://itunes.apple.com/us/rss/customerreviews/page=1/id=6458735203/sortBy=mostRecent/json#review-14588099474
- "It crashes more frequently, and often loses the last couple of minutes of changes that I’ve made." (GB 4★, 2024-05-15) https://itunes.apple.com/gb/rss/customerreviews/page=3/id=6458735203/sortBy=mostRecent/json#review-11269999377

**#3 Won't open.**
- "It refused to open it saying I needed to update it, after updating it said it was corrupted." (US 1★, 2026-01-05) https://itunes.apple.com/us/rss/customerreviews/page=5/id=6458735203/sortBy=mostRecent/json#review-13598345573
- "I have lost my 2024 diary and important notes." (GB 5★, 2024-01-12) https://itunes.apple.com/gb/rss/customerreviews/page=3/id=6458735203/sortBy=mostRecent/json#review-10814196347

**#5 Floating UI in the way.**
- "floating menus and palettes which must be constantly moved around on the page in order to write or read" (US 2★, 2026-07-19) https://itunes.apple.com/us/rss/customerreviews/page=2/id=6458735203/sortBy=mostRecent/json#review-14322629306
- "It gets in the way of my writing and my entire page." (US 1★, 2025-11-15) https://itunes.apple.com/us/rss/customerreviews/page=5/id=6458735203/sortBy=mostRecent/json#review-13402727575

**#6 Offloading.**
- "my notebooks constantly get offloaded from my iPad and into the cloud" (GB 5★, 2024-06-11) https://itunes.apple.com/gb/rss/customerreviews/page=2/id=6458735203/sortBy=mostRecent/json#review-11369215260
- The vendor's own explanation is that the iCloud cache eviction is outside its control. https://noteshelf-support.fluidtouch.biz/hc/en-us/articles/360049162614

**#8 Zoom.**
- "Just give people the option to cap the zoom out at 100%" (US 5★, 2026-05-11) https://itunes.apple.com/us/rss/customerreviews/page=3/id=6458735203/sortBy=mostRecent/json#review-14055154418

**#9 PDF fidelity.**
- "with Noteshelf, what you see on screen is not what you get on the output file" (US 1★, 2026-02-03) https://itunes.apple.com/us/rss/customerreviews/page=4/id=6458735203/sortBy=mostRecent/json#review-13710669521
- "imported PDFs look VERY blurry" (Google Play 3★, 2026-09-05) https://play.google.com/store/apps/details?id=com.fluidtouch.noteshelf3&hl=en_GB#review-13

**#10 Shapes.**
- "when I undo it, it undoes my actual drawing too" (US 1★, 2025-12-23) https://itunes.apple.com/us/rss/customerreviews/page=5/id=6458735203/sortBy=mostRecent/json#review-13546300758

**#11 Squeeze.**
- "the menu will suddenly break and only pop up near the middle of the screen, no matter where the pencil is hovering" (US 2★, 2026-09-24) https://itunes.apple.com/us/rss/customerreviews/page=1/id=6458735203/sortBy=mostRecent/json#review-14588488336

**#12 Reopen position.**
- "Notebooks don’t open where you last used and so need to scroll down to last page." (GB 1★, 2026-01-12) https://itunes.apple.com/gb/rss/customerreviews/page=2/id=6458735203/sortBy=mostRecent/json#review-13624735523

## 2. What is missing (features asked for by name)

| # | request | reviews | sources |
|---|---|---|---|
| 1 | **Stroke stabilisation / live handwriting beautification / auto-refine as you write** | 6 | 2 (App Store, Google Play) |
| 2 | Lifetime / one-time purchase back | 20+ | 3 |
| 3 | Infinite canvas / whiteboard / flexible page size | 4 | 2 |
| 4 | Better folder tree: folders in folders, collapsible sidebar, column view | 5 | 2 |
| 5 | More quick-access colours than 3 | 3 | 1 (thin) |
| 6 | Fixed zoom levels / cap zoom at 100% | 4 | 2 |
| 7 | Type directly on the page without sliding text boxes | 3 | 1 (thin) |
| 8 | Read-only by default for PDFs | 1 | 1 (thin) |
| 9 | Cross-platform sync (Android/Windows) | 5 | 2 (not relevant) |

Quotes:
- **Stabilisation.** "it’s missing a crucial feature: stroke stabilization" (US 4★, 2026-06-19) https://itunes.apple.com/us/rss/customerreviews/page=3/id=6458735203/sortBy=mostRecent/json#review-14202943215
- **Stabilisation.** "live handwriting beautification" (Google Play 4★, 2026-08-20) https://play.google.com/store/apps/details?id=com.fluidtouch.noteshelf3&hl=en_GB#review-8
- **Auto-refine.** "Auto-refine handwriting as you write, like what the Apple Notes app does." (US 3★, 2025-10-28) https://itunes.apple.com/us/rss/customerreviews/page=5/id=6458735203/sortBy=mostRecent/json#review-13327003844
- **Infinite canvas.** "An infinite canvas option for notebooks would be a game-changer." (GB 4★, 2024-01-28) https://itunes.apple.com/gb/rss/customerreviews/page=3/id=6458735203/sortBy=mostRecent/json#review-10873934617
- **Folder tree.** "add a feature of section divider to group/collapse folders on the side panel" (US 5★, 2026-06-03) https://itunes.apple.com/us/rss/customerreviews/page=3/id=6458735203/sortBy=mostRecent/json#review-14141600368
- **Text boxes.** "I want to be able to type directly onto the page without text boxes." (GB 1★, 2025-02-25) https://itunes.apple.com/gb/rss/customerreviews/page=2/id=6458735203/sortBy=mostRecent/json#review-12353329481

## 3. What is unsolved (whole jobs the app ignores)

1. **Trustworthy long-term archive.** 18 lost-work + 14 won't-open reviews, across 3 sources. People with "years and years of journaling" lost them, and the only fix path is emailing the notebook file to support (help 3j). No self-serve repair, no file-per-page storage, and backups are in a proprietary format.
   - "I am truly devastated as I have lost years and years of journaling" (US 2★, 2026-04-10) https://itunes.apple.com/us/rss/customerreviews/page=4/id=6458735203/sortBy=mostRecent/json#review-13943440580
2. **Serious STEM / graduate note-taking.** This is a positioning gap (4 reviews, 2 sources, so thin). Reviewers say it is "better suited for journaling" and ask for whiteboards, stabilisation and faithful export for problem sets.
   - "I would say the app is better suited for journaling, or secondary school classes, but definitely not graduate level." (US 3★, 2025-10-28) https://itunes.apple.com/us/rss/customerreviews/page=5/id=6458735203/sortBy=mostRecent/json#review-13327003844
3. **Users in control of their own UI.** Updates change defaults: zoom, scroll mode (there's a help article admitting an accidental switch), toolbar position, two-column thumbnails, icon-only lasso menu. 14 "update made it worse" reviews across 3 sources.

---

## Ideas for Inkwell

### What Noteshelf does brilliantly (patterns to adopt, not copy)

1. **Ink that is precise and unsmoothed, with distinct nib personalities: ball, felt, fountain, pencil.** **must**
   - The single most-praised trait: about 16 reviews call it the best or most natural writing feel. "Really precise (& not smoothed) writing" (US 5★) https://itunes.apple.com/us/rss/customerreviews/page=1/id=6458735203/sortBy=mostRecent/json#review-14577066500
   - Inkwell: render raw input faithfully. Do neatening as a separate reversible layer and never as smoothing baked into the stroke. A fountain-like nib suits cursive.
2. **One-tap swatches with long-press to edit.** **must**
   - Colour or size changes cost 1 tap. Long-press a swatch to edit it or eyedrop from the page, and "restore default" lives in the same menu.
   - Inkwell: each of the 3 pen and 2 highlighter slots in the slim top bar is a fixed preset (nib + colour + width). Tap selects; long-press edits in place. No floating palette.
3. **Undo placed for the off hand (top-left).** **must**
   - "the undo button being in the top left (unlike Notability) so it’s easy to press with your left hand while writing with your right" https://itunes.apple.com/us/rss/customerreviews/page=1/id=6458735203/sortBy=mostRecent/json#review-14585340190
   - Also add two-finger-tap undo / three-finger-tap redo.
4. **Hold at the end of a stroke to snap it to a shape, and keep the shape editable with handles.** **must**
   - Zero extra taps. This is ideal for economics axes and curves.
   - Inkwell twist: keep the original stroke underneath, and make the snap its own undo step. This avoids the "undo removed my drawing" complaint and fits never-alter-original-ink.
5. **Quick Note remembers the last paper settings** (size, line height, colour, orientation). **must**
   - Inkwell's per-page paper picker should default to the last-used paper. Then 0 extra taps is the common case.
6. **Focus mode with a 4-finger tap; read-only mode where a tap hides chrome.** **should**
   - Full-bleed paper for lectures, and no stray marks while scrolling through PDFs. Consider opening imported PDFs in read mode until the Pencil touches the page, which answers a reviewer's request.
7. **Named, coloured bookmarks turn into a clickable table of contents.** **should**
   - 2 taps to bookmark, long-press to name. Great for lecture chapters.
8. **Save a lasso selection as a reusable clip.** **should**
   - Lasso, then Save Clip, then insert from the + menu. Inkwell: save a blank supply/demand axis set or a recurring maths layout as a stamp.
9. **Hand-posture palm-rejection presets** (6 styles, 3 left-handed). **should**
   - Choose how you hold the Pencil once, and the UI and palm rejection adapt.
10. **Zoom box with auto-advance and margins.** **could**
    - Write big, render small: useful for subscripts and dense maths. Also add a zoom-preset pill (v8.0) with snap to fit-width.
11. **Backup that never propagates deletes; whole-library export that keeps the folder structure.** **should**
    - A separate one-way safety copy (PDF + native) where deleting in the app never deletes the backup.

### Pitfalls Inkwell must avoid

1. **Losing the last minutes on a crash.** **must**
   - Seen in 18 reviews (lost work or wiped notes). Persist every stroke immediately: append-only journal per page, flushed on pen-up, with a snapshot compacted later.
2. **One corrupt file or a newer format version locks the whole notebook.** **must**
   - Use per-page files inside a notebook folder and a versioned, documented format.
   - Unknown newer fields: open read-only, never refuse. Ship a self-repair and "open as read-only" path.
3. **Depending on iCloud eviction and blocking launch on iCloud.** **must**
   - Keep the iCloud Drive folder contents downloaded (request downloads; keep a local working copy). Launch from local state immediately and sync in the background. Show per-notebook sync state rather than greying things out.
   - Use file coordination and conflict versions: never last-writer-wins on a whole notebook.
4. **Floating palettes over the writing area.** **must**
   - Keep the slim top bar and inset content below it so nothing ever covers the first ruled line in vertical scroll (a GB reviewer complains planners' dates hide behind menus).
5. **Export that doesn't match the screen.** **must**
   - Export PDF from the same vector stroke geometry the renderer uses: highlighters filled and translucent, pressure widths preserved. Import PDFs as vector pages and render at device scale (no blur).
6. **Reopening at page 1.** **must**
   - Store the last viewport (page + offset + zoom) per notebook and restore it on open.
7. **Squeeze menu not anchored to the pen.** **should**
   - Inkwell maps squeeze to the eraser, so this matters less. If a squeeze palette is ever shown, anchor it to the reported hover location and fall back to the last touch point.
8. **Changing defaults in updates (zoom, scroll, toolbar).** **should**
   - Personal app, but still: changed behaviours get a toggle, and zoom-out stops at fit-width by default.
9. **Auto-shape firing unintentionally.** **should**
   - Require a deliberate hold of about 0.5 s with the pen still, give a visible snap preview, and let a single undo revert only the snap.
10. **Paywalled basics and premium-locked templates.** **skip** (a personal app has no paywall). Recorded only because it dominates the ratings.

### Apple Pencil Pro notes for Inkwell

- Noteshelf supports squeeze (it opens a tool menu) and a configurable double-tap.
- I found **no evidence** of barrel-roll or hover support anywhere public.
- Barrel roll driving a fountain/chisel highlighter angle would be a clear edge for Inkwell (**should**).
