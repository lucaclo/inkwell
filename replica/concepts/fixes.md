# Concepts: what users hate, what's missing, what's unsolved (and what Inkwell should take from it)

Sample: 916 reviews from 4 sources.
- App Store US: 500, through the official customer-reviews RSS feed, 10 pages.
- App Store GB: 405, same feed, 10 pages.
- Hacker News: 8 comments, through the Algolia API.
- Google Play: 3 reviews visible on the public listing, read in the browser.

Star ratings across the 905 App Store reviews: 512 five, 127 four, 94 three, 57 two, 115 one. Dates run from 2012-10 to 2026-10, weighted toward recent reviews by reviews.py (`--months 18`).

Reddit could not be reached. reddit.com is blocked both for the fetch/search tools and in the browser extension ("This site is not allowed"). Product Hunt returned no readable page. No Reddit quotes are used.

App Store review links point to the official RSS feed page that contained each review, with the review ID as a fragment. Apple does not publish per-review web URLs.

Counts below come from `feedback.md` theme matches, or from targeted keyword counts over reviews.csv. Keyword counts are approximate: one review can match several items.

## 1. What they hate (complaints about what the app does)

1. **Basic editing behind a paywall or subscription.** About 91 reviews rated 3 stars or below mention paying or subscriptions. The price theme in feedback.md has 174 reviews, 3 sources, average 3.2 stars. Lasso, selection, guides and straight lines all sit behind payment. This is out of scope for Inkwell, but the lesson is that editing tools are core, not extras.
   - "Paying to edit your drawings, i.e. Lasso, etc., is quite greedy because it is one of the main mechanics of drawing apps as a whole." (https://itunes.apple.com/us/rss/customerreviews/page=1/id=560586497/sortBy=mostRecent/json#review-14292605571)
   - "You need to pay to draw a straight line." (https://itunes.apple.com/gb/rss/customerreviews/page=4/id=560586497/sortBy=mostRecent/json#review-3665586250)
2. **Unintuitive UI and a steep learning curve.** 29 reviews rated 3 stars or below. The UX theme has 139 reviews across 3 sources. The tool wheel, hidden controls and custom terminology come up repeatedly.
   - "Terminology used only really seems to make sense to the people that made it." (https://itunes.apple.com/gb/rss/customerreviews/page=6/id=560586497/sortBy=mostRecent/json#review-1518081104)
   - "...designers have thrown usability guidelines out the window, to come up with an 'innovative' interface, which I personally find really annoying to use." (https://news.ycombinator.com/item?id=25275606)
3. **Lost work, crashes and lag.** 10 reviews describe lost files. 26 reviews rated 3 stars or below mention lag or crashes. The sync and data theme has 77 reviews across 4 sources.
   - "I had to delete and redownload it, and with it I lost all my files." (https://itunes.apple.com/gb/rss/customerreviews/page=1/id=560586497/sortBy=mostRecent/json#review-13187964886)
   - "When writing there is a massive delay between my brush strokes and it appearing on the page. ... Makes using the app for uni notes very difficult" (https://itunes.apple.com/gb/rss/customerreviews/page=1/id=560586497/sortBy=mostRecent/json#review-12370008500)
4. **Precision tools that half work.** 31 reviews mention snap or straight lines, all from the App Store. Complaints include snapping a few pixels off, residual snap when snapping is off, and grabbing guide handles by accident.
   - "Even with no grid snap on, the dragging of straight line still tends to have slight snap, it’s not Freeform." (https://itunes.apple.com/us/rss/customerreviews/page=1/id=560586497/sortBy=mostRecent/json#review-14106892906)
   - "When trying to snap a rectangle to the actual grid it’s always a few pixels out." (https://itunes.apple.com/gb/rss/customerreviews/page=4/id=560586497/sortBy=mostRecent/json#review-2229698104)
5. **Shape recognition that fires when not wanted.** 7 reviews mention recognition. **Thin**: App Store only, but recent (2025–2026) and directly relevant to Inkwell.
   - "lingering at the end of a stroke shouldn't invoke anything). What's worse, it can't be disabled" (https://itunes.apple.com/us/rss/customerreviews/page=3/id=560586497/sortBy=mostRecent/json#review-12611700856)
   - "All shape recognition to be just lines, circles and ellipses. Annoying arrow heads and other odd shapes is almost a workflow killer" (https://itunes.apple.com/us/rss/customerreviews/page=1/id=560586497/sortBy=mostRecent/json#review-14106892906)
6. **Masking eraser instead of a real eraser.** 4 explicit reviews. **Thin**, but stable across 2017–2022. The eraser theme overall has 30 reviews.
   - "the way the eraser works by "masking" drives me insane." (https://itunes.apple.com/us/rss/customerreviews/page=9/id=560586497/sortBy=mostRecent/json#review-8608967161)
7. **Lasso grabs the wrong things.** 21 selection or lasso mentions across 3 sources.
   - "whenever i relocate items, parts of my drawing/writing are erased!" (https://itunes.apple.com/us/rss/customerreviews/page=8/id=560586497/sortBy=mostRecent/json#review-9103678419)
8. **The pressure pen is bad for handwriting.** 13 reviews mention handwriting or pressure, across 3 sources.
   - "Concepts’ dynamic pen goes from a hairline (with light pressure) to maximum width (with heavy pressure). ... it lends itself to quite unnatural handwriting." (https://itunes.apple.com/us/rss/customerreviews/page=3/id=560586497/sortBy=mostRecent/json#review-12656005227)

## 2. What is missing (asked for by name)

1. **Cross-device sync and a Mac app.** 46 reviews mention sync or cross-platform, across 4 sources. 11 mention a Mac app, all on the App Store.
   - "still no macOS version - why??" (https://itunes.apple.com/gb/rss/customerreviews/page=1/id=560586497/sortBy=mostRecent/json#review-14123601554)
   - "There isnt even a viewing mode or useable concepts app on Mac yet." (https://itunes.apple.com/us/rss/customerreviews/page=1/id=560586497/sortBy=mostRecent/json#review-14045882754)
2. **A better text tool.** 22 reviews ask for typing inline, font choice and font size.
   - "A better text writing interface (write into text box rather than separate ’label’ UI menu)" (https://itunes.apple.com/gb/rss/customerreviews/page=2/id=560586497/sortBy=mostRecent/json#review-7378000964)
3. **Auto-shapes and straight lines without fiddly guides.** Most of these requests predate 6.23 (2025), which added recognition.
   - "an option to “auto-recognise” and correct a free drawn shape (squares, triangles etc)" (https://itunes.apple.com/gb/rss/customerreviews/page=2/id=560586497/sortBy=mostRecent/json#review-7316374857)
   - "a better implementation of drawing straight lines without needing 100% smoothing which seems ‘hacky’" (https://itunes.apple.com/gb/rss/customerreviews/page=3/id=560586497/sortBy=mostRecent/json#review-5475898378)
4. **Pencil undo on squeeze or double-tap.** 8 reviews mention double-tap or squeeze. **Thin.**
   - "Please allow me to either double tap or squeeze my apple pencil pro to undo a stroke." (https://itunes.apple.com/us/rss/customerreviews/page=2/id=560586497/sortBy=mostRecent/json#review-13121451902)
5. **A maths x-y grid and maths features.** **Thin**: 2 reviews.
   - "A ‘maths’ grid type (x, y plane)" (https://itunes.apple.com/gb/rss/customerreviews/page=2/id=560586497/sortBy=mostRecent/json#review-7378000964)
6. **Scale shapes without changing line thickness.** **Thin**: 1 named request plus related complaints about resizing.
   - "Ability to scale shapes without changing thickness" (https://itunes.apple.com/gb/rss/customerreviews/page=2/id=560586497/sortBy=mostRecent/json#review-7378000964)
   - "When resizing a square as an example… the shape will go out of alignment as you size up." (https://itunes.apple.com/gb/rss/customerreviews/page=2/id=560586497/sortBy=mostRecent/json#review-9688786863)

## 3. What is unsolved (jobs and groups the app ignores)

1. **Students taking notes.** The notes theme has 162 reviews across 3 sources, average 4.2 stars. People use Concepts for notes, maths and uni work, yet it has no pages, no paper-like page flow, a weak text tool, and pens tuned for art. The happiest note-takers love the space and the vector editing. The unhappy ones hit lag, text and handwriting problems.
   - "I am mainly using it as an infinite canvas for my long mathematical calculations." (https://itunes.apple.com/gb/rss/customerreviews/page=2/id=560586497/sortBy=mostRecent/json#review-7265800376)
   - "Concepts has a smoothing parameter that makes one's handwriting look better than it would on paper, if one selects 8% to 12%." (https://news.ycombinator.com/item?id=31720342)
2. **Everything outside one iPad.** No Mac app, incompatible file formats across platforms, and iCloud only arriving in 2024.
   - "I manage my life in Concepts ... My boards grew to gigabytes and I got worried - what if the app stops working for my use case? So I built a viewer as a backup plan." (https://news.ycombinator.com/item?id=46336223)
3. **Getting lost on the canvas.** 15 reviews about the infinite canvas mention getting lost or zoom not being infinite. A notes app with pages does not have this problem.
   - "• can get lost somewhere else" (https://itunes.apple.com/us/rss/customerreviews/page=2/id=560586497/sortBy=mostRecent/json#review-13518422643)

## 4. Ideas for Inkwell (diagram and tool patterns worth borrowing)

Tags are priority for Luca: must, should, could or skip. Each idea describes the behaviour only. Inkwell should use its own names and UI.

1. **must. Hold-to-snap shapes, then keep adjusting before lift.** Recognition fires only when the Pencil is held still at the end of a stroke. Concepts' default is about 0.5 s; use roughly 0.45–0.6 s with a movement tolerance of about 2 pt. Do not trigger on lift. Once the shape snaps, the shape follows the Pencil until lift: moving the Pencil away scales and rotates it, like Concepts does. Give a subtle haptic tick and a ghost preview at the moment of snap. Recognise only line, axis pair (an L-shape), arrow (line plus head as one gesture), circle, ellipse, rectangle and smooth curve. Do not recognise triangles or other odd polygons. Each type can be turned off in settings, and the whole feature has a master toggle. Both answer the 1-star and 3-star complaints above.
2. **must. Snapping is always reversible and never destroys ink.** Store the raw points unchanged. Store each snapped result as a separate "shape interpretation" on the stroke. Three ways to undo a snap: tap the "show original" chip that appears for about 3 s after the snap, use normal undo (the first undo reverts only the snap and keeps the raw stroke), or select the stroke later and toggle "original / neat". Concepts has no documented way to revert a recognised shape to its freehand stroke. Inkwell's hard rule makes this its edge.
3. **must. Angle and endpoint snapping for axes and arrows.** When a recognised line is within ±5° of horizontal or vertical, lock it to 0° or 90°. Also lock to 45° on grid pages. When a stroke's end lands within about 12 pt (screen space) of another stroke's endpoint or an axis, join to it. Show a small target dot at the join point before lift, like Concepts' auto-complete circles. This draws supply and demand axes and arrowheads that meet cleanly.
4. **must. Per-pen smoothing as a stroke property, computed at render time.** Each of the 3 pens gets a smoothing value, low by default (about 10%, matching the HN user's 8–12% for handwriting). Apply it to the rendered path, never to stored points, so it can be changed later. Maths regions skip neatening but can still have light smoothing.
5. **must. Transform keeps stroke width.** When scaling or stretching a diagram selection, scale the geometry and keep each stroke's width, which is Concepts' "Stretch" mode. Pinch rotates and scales. Add parallel-move snapping so a shifted demand curve stays parallel and lines up with an axis endpoint. This borrows Concepts' "snap while editing" to key points: ends, corners and centre.
6. **should. Partial erase that cuts vector strokes cleanly**, like Concepts' Slice, and no mask-style eraser. Squeeze turns on the eraser. Choose between whole-stroke and partial erase with a long-press on the eraser state. The cut pieces keep their original raw points. The eraser stores which parts are hidden, rather than editing the points, so undo is exact and the original ink stays intact.
7. **should. Lasso without switching tools.** A finger long-press of about 0.4 s starts a lasso. Pick whole strokes by default, with partial selection as an option. Exclude hidden or erased fragments from the selection, which avoids the "parts of my drawing are erased" bug. Group a diagram into one object so it moves as a unit.
8. **should. Highlighters render underneath ink automatically.** This borrows Concepts' idea of sorting layers by tool family, without showing users any layers UI.
9. **should. Fixed slots in a slim toolbar, each remembering its own preset.** Use Concepts' tool bar mode, not its wheel. Tap-hold-slide on a slot changes its size without opening a menu. Offer 4 size presets per pen. Squeeze is the eraser, double-tap opens the palette, a two-finger tap undoes, and a three-finger tap redoes.
10. **could. A temporary straight-edge guide for one stroke.** A two-finger long-press on the page shows a ruler you can rotate, with 15° detents. It disappears after one stroke, so it never becomes a persistent on-canvas guide that clutters notes. Optional; ideas 1 and 3 probably make it unnecessary.
11. **could. Per-page operation history scrubber.** Older Concepts reviews loved being able to "move through the entire creative process". Because Inkwell stores operations, not edited points, a scrubber is cheap to add later.

Skip for a notes app: the radial tool wheel, persistent shape guides with handles, measurement and drawing scale, perspective grids, user-visible layers and focus mode, Nudge, masks, and the infinite canvas.

## 5. Pitfalls Inkwell must avoid

1. **must. Accidental recognition.** Natural pauses in cursive or maths must never snap. Gate recognition on the hold time and a stillness threshold. Never run it inside maths regions or on text-like strokes, meaning short strokes in a line of writing. Keep a master off switch. (Recognition reviews: 7, thin but recent.)
2. **must. Residual snapping when snapping is off.** If snapping is off, output must be exactly the raw stroke plus the pen's smoothing setting, with no hidden pull. (See https://itunes.apple.com/us/rss/customerreviews/page=1/id=560586497/sortBy=mostRecent/json#review-14106892906)
3. **must. Losing work.** Write atomic saves into the iCloud Drive folder, keep a recoverable trash, and never auto-delete local files on conflict: keep both versions. (Data theme: 77 reviews across 4 sources; 10 explicit "lost" reports.)
4. **must. Mask-style erasing and selection bugs.** Erased parts must move with the stroke they belong to, and selection must not resurrect or drop fragments. (Eraser 30 reviews; selection 21.)
5. **should. Hidden controls and custom terminology.** Keep every pen, highlighter and eraser visible in the top bar. Use plain words. (UX theme: 139 reviews.)
6. **should. A pressure curve that ruins handwriting.** Clamp the minimum and maximum width ratio for the pens, roughly 0.6–1.4× of nominal, not hairline to fat. (13 reviews.)
7. **should. Lag while writing on large documents.** Render only the visible pages and keep live ink on a low-latency layer. (26 low-rated lag or crash reviews.)

## 6. Fix plan (top items by evidence × cheapness, for Inkwell)

| # | build | size | evidence |
| --- | --- | --- | --- |
| 1 | Raw-ink-plus-interpretation stroke model (snap and neaten as reversible layers) | M | pitfall 1–2, missing 3 |
| 2 | Hold-to-snap recognition with a per-type toggle and a "show original" chip | M | hate 5, missing 3 |
| 3 | Angle and endpoint snap for axes and arrows | S | hate 4 |
| 4 | Partial erase that hides parts of a stroke without editing it; squeeze toggles the eraser | S | hate 6, missing 4 |
| 5 | Lasso with whole-stroke default, grouping, and width-preserving scale | S | hate 7, missing 6 |
| 6 | Pressure curve clamp and per-pen smoothing | S | hate 8, unsolved 1 |
| 7 | Mac Catalyst plus iCloud Drive folder with keep-both on conflict | L | missing 1, unsolved 2 |

## 7. Angle (personal app, for reference only)

For students who write maths and draw economics diagrams by hand, and who find that art apps make them fight the tools while notes apps can't draw a clean axis, Inkwell keeps the handwriting untouched while it neatens and snaps diagram strokes in a way that can always be undone.
Evidence: notes theme 162 reviews across 3 sources; precision complaints 31; recognition complaints 7 (thin).
