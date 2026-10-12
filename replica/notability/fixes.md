# Notability: what users hate, what's missing, what's unsolved, and ideas for Inkwell

**Sample:** 540 reviews from 5 sources (see `reviews.csv` and `feedback.md`):

| source | reviews |
| --- | --- |
| App Store US, via the official customer-reviews RSS feed | 250, dated 2026-08-24 to 2026-10-10 |
| App Store UK | 250, dated 2025-04-03 to 2026-10-10 |
| Hacker News, via the Algolia API | 35 comments, 2013–2026 |
| Trustpilot | 4, which is every review on the page |
| Goodnotes public feedback board | 1 comment about Notability |

- **Ratings:** 504 of the 540 have stars. 252 are 1★, 63 are 2★, 34 are 3★, 43 are 4★ and 112 are 5★.
- **Why so many 1★:** the RSS feed sorts by most recent, so the sample is weighted toward the 2026 cloud-migration backlash. It is far more negative than the 4.76 lifetime average.
- **How counts were made:** each count is the number of reviews matching a keyword regex over the whole CSV, so treat them as approximate. "src" is the number of distinct sources.
- **Reddit:** both the API and the website were blocked from this environment, so no Reddit rows are included.

Quote links: App Store quotes link to the official RSS page plus `#review-<id>`. HN quotes link to the comment.

---

## 1. What users hate (ranked by evidence)

| # | problem | reviews | src | quotes |
| --- | --- | --- | --- | --- |
| 1 | **Notes or folders vanish**, often after an update or during sync | 50 | 2 | "Yesterday a hundred page note just up and disappeared." [link](https://itunes.apple.com/us/rss/customerreviews/page=1/id=360593530/sortBy=mostRecent/json#review-14650514673) · "All my folders sorting my 800 note pages just gone for no reason, and no way to reverse it." [link](https://itunes.apple.com/gb/rss/customerreviews/page=1/id=360593530/sortBy=mostRecent/json#review-14642106445) |
| 2 | **Support doesn't help**: an AI bot, tickets closed without a fix (regex is broad) | 66 | 3 | "the support ticket was responded to with a general AI bot so there’s nothing else I can do" [link](https://itunes.apple.com/us/rss/customerreviews/page=5/id=360593530/sortBy=mostRecent/json#review-14491746038) · "Notability is a deeply flawed system with virtually no customer support." [Trustpilot](https://www.trustpilot.com/reviews/6a169927ef7b6a735668afc2) |
| 3 | **An update removed a habit** (squeeze eraser, one-finger scroll with the text tool, custom templates, text wrap) | 53 | 2 | "Unfortunately some of the updates are really annoying, like the squeeze eraser being removed." [link](https://itunes.apple.com/gb/rss/customerreviews/page=1/id=360593530/sortBy=mostRecent/json#review-14224928960) · "the app has removed so many things" [link](https://itunes.apple.com/us/rss/customerreviews/page=3/id=360593530/sortBy=mostRecent/json#review-14531720276) |
| 4 | **Crashes and freezes**, on Mac too | 43 | 2 | "Love Notability, but the Mac version crashes multiple times a day." [link](https://itunes.apple.com/us/rss/customerreviews/page=2/id=360593530/sortBy=mostRecent/json#review-14582289576) |
| 5 | **A login and account are now required**, and offline access fails | 38 | 2 | "It used to be a simple download and use, now it requires an account." [link](https://itunes.apple.com/us/rss/customerreviews/page=5/id=360593530/sortBy=mostRecent/json#review-14490406114) · "Today I attempted to use the app and it prompted me to login in." [link](https://itunes.apple.com/us/rss/customerreviews/page=5/id=360593530/sortBy=mostRecent/json#review-14490829105) |
| 6 | **Subscription switch** that betrayed one-time buyers (2021, still cited) | 29 | 2 | "It is not acceptable to force your former paid users of the application into a subscription whatsoever." [link](https://itunes.apple.com/us/rss/customerreviews/page=1/id=360593530/sortBy=mostRecent/json#review-14625741595) · "They even put iCloud sync behind the subscription, that's not using their servers or datacenters." [HN](https://news.ycombinator.com/item?id=40662917) |
| 7 | **Lag, slowness, heat, battery** | 27 | 2 | "It takes nearly a full minute just to add a page between my notes." [link](https://itunes.apple.com/us/rss/customerreviews/page=1/id=360593530/sortBy=mostRecent/json#review-14638371818) · "it cannot handle huge PDFs without draining the battery" [link](https://itunes.apple.com/us/rss/customerreviews/page=2/id=360593530/sortBy=mostRecent/json#review-14584607281) |
| 8 | **The free tier stops you writing** (5 notes, then read-only or usage limits) | 22 | 1 | "Spent hours working on a scrapbook for a message to pop up saying my work will become read only if I don’t pay." [link](https://itunes.apple.com/gb/rss/customerreviews/page=3/id=360593530/sortBy=mostRecent/json#review-13503059184) |
| 9 | **Forced move from iCloud to their own cloud** (privacy, consent) | 14 | 1 | "This is a forced transfer of my private documents from iCloud (secure) to Notability Cloud (stored on servers in the US) - a huge privacy risk!" [link](https://itunes.apple.com/gb/rss/customerreviews/page=1/id=360593530/sortBy=mostRecent/json#review-14309420165) · "they scheduled the move of all the notes to their cloud service, with just a postpone button" [link](https://itunes.apple.com/us/rss/customerreviews/page=4/id=360593530/sortBy=mostRecent/json#review-14498898680) |
| 10 | **AI pushed in, bloat** | 14 | 2 | "More AI bloat gives us none of those things." [link](https://itunes.apple.com/us/rss/customerreviews/page=2/id=360593530/sortBy=mostRecent/json#review-14584607281) · "Notability/Goodnotes seem to have become overly bloated" [HN](https://news.ycombinator.com/item?id=46310152) |
| 11 | **Mac app problems** (crashes, sync, typing drifts from its spot on iPad) | 13 | 2 | "PLEASE fix the spacing issue between iPad and Mac I’m begging." [link](https://itunes.apple.com/us/rss/customerreviews/page=4/id=360593530/sortBy=mostRecent/json#review-14510028740) · "Their macOS apps (I feel) really terrible." [HN](https://news.ycombinator.com/item?id=24532083) |

Items 1, 5 and 9 share one root cause: the 2025–26 move to Notability's own cloud plus accounts. That is the dominant story in the 2026 sample.

## 2. What is missing (asked for by name)

| # | request | reviews | src | quotes |
| --- | --- | --- | --- | --- |
| 1 | **Different paper per page in one note**, and more or custom templates | 16 (template mentions) | 2 | "could you please allow different templates on different pages within the same document" [link](https://itunes.apple.com/gb/rss/customerreviews/page=5/id=360593530/sortBy=mostRecent/json#review-12536535630) · "it will be nice to be able to customise each page with different templates" [link](https://itunes.apple.com/gb/rss/customerreviews/page=1/id=360593530/sortBy=mostRecent/json#review-14623860223) |
| 2 | **Better Pencil options**: scribble-to-erase, hover, squeeze opens the palette | 10 | 2 | "I would really like a scribble to erase feature" [link](https://itunes.apple.com/us/rss/customerreviews/page=2/id=360593530/sortBy=mostRecent/json#review-14584607281) · "At least give us the option to squeeze for the tool palette like EVERY OTHER NOTES APP." [link](https://itunes.apple.com/us/rss/customerreviews/page=2/id=360593530/sortBy=mostRecent/json#review-14584607281) |
| 3 | **Control over snapping, layers and pen stabilisation** | 8 | 2 | "a toggle for turning off snapping" [link](https://itunes.apple.com/us/rss/customerreviews/page=4/id=360593530/sortBy=mostRecent/json#review-14517812495) · "There is also no clear way to rearrange layers." [link](https://itunes.apple.com/us/rss/customerreviews/page=3/id=360593530/sortBy=mostRecent/json#review-14530082754) · "the lack of stabilization in the pen" [link](https://itunes.apple.com/us/rss/customerreviews/page=4/id=360593530/sortBy=mostRecent/json#review-14506617945) |
| 4 | **Outlines, links, comments** (thin) | 6 | 2 | "And there are no outlines?" [link](https://itunes.apple.com/gb/rss/customerreviews/page=2/id=360593530/sortBy=mostRecent/json#review-13924322378) |
| 5 | **Better file management**: subfolders, manual sort, duplicate names (thin) | 5 | 1 | "you cant have two documents with the same name even if they are in different “subjects”" [link](https://itunes.apple.com/gb/rss/customerreviews/page=3/id=360593530/sortBy=mostRecent/json#review-13405930593) |
| 6 | **Typed text that sits on the ruled lines** (thin) | 1 | 1 | "the typing does not line up with the lines of the page" [link](https://itunes.apple.com/us/rss/customerreviews/page=3/id=360593530/sortBy=mostRecent/json#review-14540204223) |
| 7 | **Infinite canvas or whiteboard note** (thin) | 4 | 1 | "please add an infinite canvas whiteboard" [link](https://itunes.apple.com/gb/rss/customerreviews/page=2/id=360593530/sortBy=mostRecent/json#review-14009055559) |
| 8 | **Tables** (thin) | 4 | 2 | "doesn't allow the creation of tables" [link](https://itunes.apple.com/gb/rss/customerreviews/page=3/id=360593530/sortBy=mostRecent/json#review-13286624834) |
| 9 | **Windows/PC sync** (thin; irrelevant to Luca) | 3 | 1 | "I'm hoping this app can sync with my Dell laptop" [link](https://itunes.apple.com/us/rss/customerreviews/page=3/id=360593530/sortBy=mostRecent/json#review-14547795846) |

## 3. What is unsolved (whole jobs the app now ignores)

1. **A private, offline, account-free notebook that never loses work.** This rolls up the hate items about vanished notes, logins, the forced cloud and support (50+38+14 overlapping reviews, 2–3 sources). Notability is moving the other way, toward a server, accounts and AI. "If only Notability could *reliably* back up my notes then it would be brilliant." [link](https://itunes.apple.com/gb/rss/customerreviews/page=1/id=360593530/sortBy=mostRecent/json#review-14580764969) · "What note takers want is 1) app reliability" [link](https://itunes.apple.com/us/rss/customerreviews/page=2/id=360593530/sortBy=mostRecent/json#review-14584607281)
2. **Long-term archive of important records**, where years of notes must survive (thin as a stated job, but severe). "Notability is a deeply flawed system with virtually no customer support." [Trustpilot](https://www.trustpilot.com/reviews/6a169927ef7b6a735668afc2) · "unfortunately 5 years of teaching notes  have gone missing" [link](https://itunes.apple.com/gb/rss/customerreviews/page=3/id=360593530/sortBy=mostRecent/json#review-13375699167)
3. **Linear notes and a free canvas in one app** (thin). "It would be really cool if I could do both in one app." [link](https://itunes.apple.com/us/rss/customerreviews/page=4/id=360593530/sortBy=mostRecent/json#review-14513712398)
4. **Maths and science handwriting** (thin in this sample, 4 mentions; maths conversion is paywalled). "Neither app can recognize math unfortunately" [HN, 2018](https://news.ycombinator.com/item?id=18757865). This is old and now partly solved by paid LaTeX conversion.

---

## Ideas for Inkwell

### What Notability does brilliantly: patterns to learn from (functionality only, nothing copied)

1. **Seamless vertical scroll where ink crosses page breaks.** This is Notability's signature. Pages keep a fixed shape for export, but writing at the bottom of a page flows straight onto the next with no "page full" moment. A new page appears when you scroll past the end. Evidence: "Endless scrolling makes it so it doesn’t feel size limiting" [HN](https://news.ycombinator.com/item?id=29373570) · "I love being able to just scroll up endlessly to see what I was thinking about" [HN](https://news.ycombinator.com/item?id=39434852) · "when you write at the bottom of a page, it seamlessly lets you draw through to the next page" [Goodnotes board](https://feedback.goodnotes.com/forums/191274-customer-suggestions-for-goodnotes/suggestions/42908904-continuous-scrolling?page=2). **must**
2. **One tap to a blank note on your default paper.** +New opens straight into the editor. A default title with the date and a default template remove every decision, and a paper picker sits as small chips at the bottom of a fresh page instead of a modal. Inkwell should do the same on every new page: show lined, grid and blank chips at the bottom, have them disappear on the first stroke, and default to the last choice. **must**
3. **Gestures that cost zero taps.** Two-finger tap undoes and three-finger tap redoes. One finger scrolls while the Pencil draws. Squeeze-and-hold gives a temporary eraser and release returns to the pen. Double-tap switches to the eraser or palette. The eraser auto-returns to the last pen. Evidence: "quick gestures/features that drastically speed up note taking, like double or triple taps to undo and redo strokes" [link](https://itunes.apple.com/us/rss/customerreviews/page=2/id=360593530/sortBy=mostRecent/json#review-14593065639). **must**
4. **Hold to snap.** Draw a line or shape and keep the nib down about a second: it becomes a straight line or a clean shape, aligned to the grid with guides, and you can edit its points afterwards. This is ideal for supply/demand axes and curves. Add what users asked for: a toggle and a hold-time setting. **must**
5. **A simple UI that stays put.** Users explicitly credit stability of the layout: "the UI is simple which I like. And I appreciate that they don’t change it every month" [link](https://itunes.apple.com/us/rss/customerreviews/page=2/id=360593530/sortBy=mostRecent/json#review-14584607281) · "despite having plenty of features, its really easy to get the hang of" [link](https://itunes.apple.com/gb/rss/customerreviews/page=1/id=360593530/sortBy=mostRecent/json#review-14224928960). Inkwell: one slim top bar with 3 pens and 2 highlighters as duplicated presets, which mirrors Notability's "duplicate tool" idea. Hide everything else behind long-press. **must**
6. **PDF import that leaves room to write.** On import you can add blank margin to the left, right or both sides of every page. Dropping a PDF onto an open note on Mac appends it. Users love annotating slides with the same pen toolbar: "I absolutely love importing a PDF and annotating pages with the Notability toolbar" [link](https://itunes.apple.com/us/rss/customerreviews/page=4/id=360593530/sortBy=mostRecent/json#review-14517812495). Also let users insert blank pages between PDF pages ([HN](https://news.ycombinator.com/item?id=40662917)). **must** (margins and appending: **should**)
7. **Two notes at once through an edge swipe.** Swipe from the left edge to open a thumbnail strip of notes. Long-press one and choose right or bottom to get a split, then swap orientation from the same menu. That is 3 gestures to have a textbook and your notes together. **should** (later, alongside tabs)
8. **Handwriting search that just works.** "the search function directly in my handwritten notes is fantastic" [link](https://itunes.apple.com/us/rss/customerreviews/page=1/id=360593530/sortBy=mostRecent/json#review-14626694868). Inkwell gets this on-device and free; Notability puts it in its Plus tier. **must**
9. **Circle to grab, move or zoom ink.** The lasso handles move, resize, recolour and convert, and the original ink can stay. "features like circle a piece of text to move/zoom it makes usual paper feel outdated" [HN](https://news.ycombinator.com/item?id=29373570). Add tap-to-select a single stroke, which users requested. **must**
10. **A recovery net.** Recently Deleted keeps notes for 30 days, and per-note version history restores an older copy as a separate note rather than overwriting. Inkwell should keep this but never tie history to the file name; Notability wipes history on rename. **must**

### Pitfalls Inkwell must avoid

1. **Never move, migrate or re-host the user's files.** Notability's 2026 collapse in ratings comes from its forced move to its own cloud, mandatory logins and notes disappearing. Inkwell: the iCloud Drive folder *is* the library, with no accounts and no migrations. On conflict, write both versions as files. Never delete on sync. **must**
2. **Never let a note become unopenable.** Users report hours of syncing, files stuck on "swirling icon as it is constantly downloading" ([link](https://itunes.apple.com/gb/rss/customerreviews/page=3/id=360593530/sortBy=mostRecent/json#review-13240470160)), and notes inaccessible when storage is low. Open whatever is local immediately and sync in the background. **must**
3. **Don't change muscle-memory defaults in updates.** Moving the squeeze eraser, breaking one-finger scroll and dropping custom templates all produced 1★ reviews. Inkwell's gestures are its UI, so freeze them. **must**
4. **Don't let rename destroy history,** and don't use titles as unique IDs. Notability blocks duplicate names across folders and wipes version history on rename. Use stable IDs inside the files and allow any name. **must**
5. **Keep performance flat on 300+ page notes and big PDFs.** Users report lag, heat, battery drain and a minute to insert a page. Render tiles lazily and keep ink separate from PDF rasterisation. **must**
6. **Keep the Mac app at parity.** Avoid drifting text, missing shortcuts or shortcut clashes (⌘-I is both italics and night mode on Notability's Mac app). Also avoid asking for unrelated permissions: one reviewer says the Mac app needs audio access. **should**
7. **No feature creep in the editor.** AI, gallery, stickers and upsell banners crowd out reliability: "More AI bloat gives us none of those things." **must**
8. **Paper per page, not per note.** Notability allows only one template per note, so this is a known gap and already planned in Inkwell. **must**
9. **Typed text should snap to ruled lines,** and the iPad and Mac must lay out text identically. **should**
10. **Pencil Pro done fully but configurable:** hover preview, optional haptics (one user found the selection haptic annoying), squeeze as eraser or palette by choice, and scribble-to-erase only as an opt-in so it doesn't fight cursive. **should**

### Not verified
- **Reddit:** blocked from this environment, so it is not represented.
- **Device behaviour:** tap counts and behaviours come from help-center steps, not hands-on use.
- **Lasso menu items** beyond move, resize, convert and mirror are inferred.
- **Mac app built on Catalyst:** this is inferred and not confirmed by an official source.
- **Notability Cloud timeline and how forced it is:** taken from reviews plus the FAQ. The FAQ calls it "partly opt-in".
