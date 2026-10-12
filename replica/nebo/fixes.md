# Nebo / MyScript Notes: what users hate, what's missing, what's unsolved, and ideas for Inkwell

Sample: **629 items from 5 sources**:
- 600 App Store reviews (500 US, 100 GB, Oct 2023 to Oct 2026, via Apple's official customer-reviews RSS feed)
- 25 Hacker News comments (Algolia API, 2014 to 2025)
- 4 forum excerpts (Mac Power Users, Literature & Latte)

Star mix of the 600 rated: 257×5, 107×4, 67×3, 49×2, 120×1. **Reddit could not be reached** (403 without OAuth), so it is not in the sample. The App Store feed has no per-review permalink, so each quote links to the feed page that contains it.

Counts come from two places. "Theme" counts are from `feedback.md`, which matches keywords and can over-count. Counts marked **hand-read** are reviews I read and checked one by one. A theme is called **thin** when it has fewer than 5 reviews or only one source.

---

## 1. What they hate (complaints about things the app does)

**1. Paid features taken away by the subscription switch (Sept 2025 rename to MyScript Notes).**
- 118 reviews in the theme, across 3 sources. 45 of the 76 one- and two-star reviews since June 2025 mention paying or subscription.
- Scratch-to-erase and conversion were briefly paywalled. A GB reviewer says scratch-to-erase was later restored to the free tier.
- > "To now lock features I already paid for behind a paywall is illegal." ([US 1★, 2025-09-05](https://itunes.apple.com/us/rss/customerreviews/page=3/id=1119601770/sortBy=mostRecent/json))
- > "basic functions like being able to scribble to erase are now paid subscription only. Greedy, greedy." ([US 1★, 2025-09-08](https://itunes.apple.com/us/rss/customerreviews/page=3/id=1119601770/sortBy=mostRecent/json))
- *For Inkwell: not applicable (personal app). The lesson is never to gate or remove a gesture the hand has already learned.*

**2. Crashes, freezes and lost work.**
- Bugs theme: 105 reviews, 2 sources. **10 hand-read reviews describe actually losing notes.**
- > "I once lost 12h worth of notes because of it and was unable to get them back a day before a big exam." ([US 1★, 2026-05-26](https://itunes.apple.com/us/rss/customerreviews/page=1/id=1119601770/sortBy=mostRecent/json))
- > "it deleted huge amounts of writing and did not give me a way to undo it" ([US 1★, 2025-07-31](https://itunes.apple.com/us/rss/customerreviews/page=3/id=1119601770/sortBy=mostRecent/json))

**3. Auto-magic that rewrites your ink and cannot be switched off.** These are straight-line snapping, fraction bars, scratch misfires, auto-format and reflow. **At least 24 hand-read reviews, 2 sources (App Store US and GB)**, and the average is only about 2.7★.
- > "you can’t turn off the option for it to automatically trying to straighten lines … often the opposite of what I want when i’m trying to write fractions" ([US 4★, 2025-10-29](https://itunes.apple.com/us/rss/customerreviews/page=2/id=1119601770/sortBy=mostRecent/json))
- > "This formatting cannot be undone, and the only way of correcting it is to erase everything that’s been formatted and write it out again" ([GB 2★, 2026-02-22](https://itunes.apple.com/gb/rss/customerreviews/page=1/id=1119601770/sortBy=mostRecent/json))

**4. Sync: conflicted copies, duplicates, re-linking, slowness.**
- 51 reviews mention sync, 23 of them at 1–3★, across 3 sources.
- > "when switching between them, I frequently encounter duplicated notes labeled as “conflicted copies.”(I use iCloud as my sych. cloud)" ([US 3★, 2026-03-21](https://itunes.apple.com/us/rss/customerreviews/page=1/id=1119601770/sortBy=mostRecent/json))
- > "Constantly I get conflicts between the devices - it always creates extra copies" ([US 1★, 2025-09-15](https://itunes.apple.com/us/rss/customerreviews/page=3/id=1119601770/sortBy=mostRecent/json))

**5. Account and login walls.**
- 14 low-star reviews, 2 sources.
- > "CANT SUBMIT A SUPPORT TICKET W/O AN ACCOUNT AND WONT LET YOU SIGN IN." ([US 1★, 2025-09-09](https://itunes.apple.com/us/rss/customerreviews/page=3/id=1119601770/sortBy=mostRecent/json))
- > "Don’t like apps that require users to sign on or create an account." ([US 1★, 2025-10-16](https://itunes.apple.com/us/rss/customerreviews/page=2/id=1119601770/sortBy=mostRecent/json))

**6. Lag with long notes and big PDFs.**
- Performance theme: 40 reviews, 3 sources.
- > "Started noticing 500pg the program struggles. Starts to get real laggy and freezes every other input." ([US 2★, 2025-11-04](https://itunes.apple.com/us/rss/customerreviews/page=2/id=1119601770/sortBy=mostRecent/json))

**7. AI and "study" features distracting from the core.**
- 52 reviews mention AI, but most are neutral or positive. Explicit complaints are **thin, about 4**.
- > "FFS – just focus on being the best note-taking app out there, and cut out all the ridiculous distractions." ([GB 4★, 2026-06-30](https://itunes.apple.com/gb/rss/customerreviews/page=1/id=1119601770/sortBy=mostRecent/json))

## 2. What is missing (asked for by name)

**1. Toggles for every smart behaviour (gestures, line straightening, auto-format).**
- Overlaps Hate #3. **At least 8 hand-read reviews explicitly ask for an off switch.**
- > "the scribble erase can’t be disabled—as far as I can tell. I loss sketches and doodles with in the note because of this feature." ([US 4★, 2023-11-07](https://itunes.apple.com/us/rss/customerreviews/page=10/id=1119601770/sortBy=mostRecent/json))
- > "Beware that all the smart gestures cannot be turned off." ([US 3★, 2024-12-23](https://itunes.apple.com/us/rss/customerreviews/page=5/id=1119601770/sortBy=mostRecent/json))

**2. Nested folders.**
- 5 hand-read reviews, 2 sources (thin, but consistent). The organisation theme has 41 reviews.
- > "I wish I could create folders inside of folders" ([US 4★, 2026-04-07](https://itunes.apple.com/us/rss/customerreviews/page=1/id=1119601770/sortBy=mostRecent/json))
- > "where are the subfolders? … organisation becomes a pain when you can only have two stages of folders." ([GB 3★, 2024-07-01](https://itunes.apple.com/gb/rss/customerreviews/page=2/id=1119601770/sortBy=mostRecent/json))

**3. Continuous vertical scroll in notebooks, and quick add-page.**
- 5 reviews, 1 source (thin).
- > "There is no continuous scroll notebook option and switching from one notebook page to the next is super slow and buggy." ([US 2★, 2026-05-05](https://itunes.apple.com/us/rss/customerreviews/page=1/id=1119601770/sortBy=mostRecent/json))
- > "its a multi step process to add another “page” to a document" ([US 3★, 2024-09-06](https://itunes.apple.com/us/rss/customerreviews/page=6/id=1119601770/sortBy=mostRecent/json))

**4. Better maths: inline maths, advanced notation, editable LaTeX.**
- 28 maths mentions in total, 3 sources. They are mostly positive, but about 6 ask for more.
- > "The math conversion is of minimal usefulness, it is difficult to include in-line math in text. … for more advanced mathematics it is simply not usable. Even to be able to edit the underlying LaTeX code would be extremely useful." ([US 4★, 2026-03-08](https://itunes.apple.com/us/rss/customerreviews/page=1/id=1119601770/sortBy=mostRecent/json))
- > "kill the popup please!" about the forced Text/Math chooser ([US 4★, 2025-01-19](https://itunes.apple.com/us/rss/customerreviews/page=5/id=1119601770/sortBy=mostRecent/json))

**5. Undo gesture.**
- 4 reviews, 1 source (thin). **Already fixed in v6.7 (Feb 2025)** with a two-finger tap. It is still worth noting because it was a top request for years.
- > "I always need to undo because I’m doing math and it’s such a hassle to have to look for the undo button." ([US 4★, 2024-01-31](https://itunes.apple.com/us/rss/customerreviews/page=9/id=1119601770/sortBy=mostRecent/json))

**6. Page templates.**
- About 4 reviews (thin).
- > "I need to setup templates for my notes and Nebo won't allow it unless you do it as a picture." ([US 3★, 2025-08-22](https://itunes.apple.com/us/rss/customerreviews/page=3/id=1119601770/sortBy=mostRecent/json))

**7. A truly uniform stroke (no pressure).**
- About 3 reviews (thin).
- > "Uniform Stroke/Toggle Off pressure sensitivity." ([US 4★, 2025-01-17](https://itunes.apple.com/us/rss/customerreviews/page=5/id=1119601770/sortBy=mostRecent/json))

**8. Visible handwriting search.**
- About 2 reviews (thin). Search existed, but people could not find it.
- > "I don’t see any way to search my handwritten notes. Am I missing something?" ([GB 4★, 2024-12-26](https://itunes.apple.com/gb/rss/customerreviews/page=1/id=1119601770/sortBy=mostRecent/json))

**9. Better shape recognition (hexagons, chemistry).**
- About 3 reviews (thin).
- > "it cannot detect benzene in shape." ([US 3★, 2023-10-30](https://itunes.apple.com/us/rss/customerreviews/page=10/id=1119601770/sortBy=mostRecent/json))

## 3. What is unsolved (whole jobs or groups the app ignores)

**1. STEM and diagram-heavy note-takers whose maths and graphs get "corrected".**
- The text-first engine treats fraction bars, axes and Greek letters as things to fix.
- About 10 hand-read reviews, 2 sources. **This is exactly Luca's profile.**
- > "I am drawing diagrams or using greek letters for my science and math courses, and it is simply not feesible to constantly redraw the symbols during a live lecture." ([US 2★, 2023-11-15](https://itunes.apple.com/us/rss/customerreviews/page=10/id=1119601770/sortBy=mostRecent/json))
- > "Forget drawing any kind of graph on this app because it will automatically try to adjust the lines for you and end up messing up every box you already" ([US 1★, 2024-01-09](https://itunes.apple.com/us/rss/customerreviews/page=9/id=1119601770/sortBy=mostRecent/json))

**2. People who want to keep their own handwriting, made tidier and searchable, not converted to type.**
- Nebo's beautification is all-or-nothing conversion, reversible only by undo.
- Signals: about 3 reviews plus 1 HN comment (thin).
- > "I want to write some notes in handwriting on my iPad, and then ocr and clean up those notes to be liked I typed them, but still preserve the original handwriting." ([HN, 2022-12-27](https://news.ycombinator.com/item?id=34148521))
- > "the words I wrote down move and overlap another section of my writing and I cant move it because it’s merged with the other words now" ([GB 3★, 2026-05-26](https://itunes.apple.com/gb/rss/customerreviews/page=1/id=1119601770/sortBy=mostRecent/json))

**3. Owning your notes.**
- Users want no account, no proprietary format hidden in the cloud, and automatic backups.
- About 6 hand-read reviews, 1 source.
- > "The file format is proprietary, so you’ll have to pay forever just for access to your own notes." ([US 1★, 2025-09-05](https://itunes.apple.com/us/rss/customerreviews/page=3/id=1119601770/sortBy=mostRecent/json))
- > "Lost all my notes because there’s no automatic backup feature if you reset you iPad." ([US 4★, 2024-05-02](https://itunes.apple.com/us/rss/customerreviews/page=8/id=1119601770/sortBy=mostRecent/json))

---

## Ideas for Inkwell

### What Nebo does brilliantly (patterns to take, rebuilt fresh)

1. **Scratch-out to erase, with zero tool switches.** **must**
   - It is the most-loved gesture. Reviewers dropped the app when it was paywalled. "I also love the scribble out to erase." ([US 5★, 2024-09-02](https://itunes.apple.com/us/rss/customerreviews/page=6/id=1119601770/sortBy=mostRecent/json))
   - Inkwell: about 0 taps versus about 2 for an eraser round-trip.
   - Detect a zig-zag (at least 3 direction reversals, dense path) over existing ink.
   - Fade the erased strokes out over about 150 ms so the user sees what went.
   - Keep the strokes in undo history and in a per-page "recently erased" store.
   - **Never fire inside a region marked or detected as maths or diagram**, and offer a toggle.
2. **Recognition that tolerates messy cursive and stays out of the way.** **must** (search) / **could** (convert)
   - > "It's the least in-my-way handwriting recognition that I've used." ([HN, 2020-01-29](https://news.ycombinator.com/item?id=22179729))
   - > "can even read my cursive writing" ([US 5★, 2025-06-03](https://itunes.apple.com/us/rss/customerreviews/page=4/id=1119601770/sortBy=mostRecent/json))
   - Inkwell: index silently in the background with Vision, and never convert unless asked.
   - Users praise that conversion is on demand: "doesn’t immediately convert handwriting to text but instead allows you to double-tap when you’re ready" ([US 5★, 2024-10-10](https://itunes.apple.com/us/rss/customerreviews/page=6/id=1119601770/sortBy=mostRecent/json)).
3. **Live recognition preview as a feedback loop.** **should**
   - A faint line of recognised text above the ink in documents. One reviewer says it improved their handwriting ("document mode shows handwriting recognition as you write, this makes for a very short feedback loop" — [GB 4★, 2023-10-26](https://itunes.apple.com/gb/rss/customerreviews/page=2/id=1119601770/sortBy=mostRecent/json)).
   - Inkwell: an optional, low-contrast preview of the Vision reading for the line just finished. It doubles as a "search will find this" confirmation.
4. **Hold-to-snap shapes, with Pencil Pro haptics.** **should**
   - Draw a box in one stroke, hold, and it becomes a perfect rectangle. Arrows snap to shape edges. A haptic tick fires on snap, every 90° of rotation and on convert.
   - The trigger is deliberate (a hold), not automatic, which is why it works.
   - Inkwell: the same gesture for econ diagrams (axes, curves, arrows). Store the snapped geometry as a reversible overlay on the raw stroke, with a "show original" toggle.
5. **Squeeze or double-tap opens a floating palette at the nib.** **must**
   - 1 tap to switch tool, width or colour without travelling to the toolbar.
   - Inkwell: Luca's plan (squeeze = eraser, double-tap = palette) is a cleaner split. Show the palette near the hover point and let hover preview the tool.
6. **Two-finger tap undo, three-finger tap redo.** **must**
   - 0 taps. Nebo was criticised for years until it shipped this in v6.7.
7. **Make space mid-page with a two-finger long-press and drag.** **should**
   - A blue line appears and you drag down to open room or up to close it. This is a perfect "insert space" for lecture notes.
   - Inkwell: implement it as a translation of everything below the line (a reversible transform), never a reflow.
8. **Gestures that edit without switching tools: join and split with a vertical line, frame to highlight.** **could**
   - Good for text, risky near maths. Off by default inside maths regions.
9. **Ink rendering that looks good.** **should**
   - > "I *love* the way Nebo renders “ink”. It’s so much nicer than Goodnotes, Notability … Their “fountain pen” setting really looks as if I had written it with a fountain pen." ([US 3★, 2024-09-06](https://itunes.apple.com/us/rss/customerreviews/page=6/id=1119601770/sortBy=mostRecent/json))
   - Inkwell: spend real time on stroke smoothing and pressure-to-width curves for 3 pen presets. Also offer one fully uniform preset.
10. **The recognition user dictionary.** **could**
    - Add "oligopoly", "Cobb-Douglas" and similar so search finds them. With Vision, Inkwell can do this as a post-correction list, not true recognition training.

### Pitfalls Inkwell must avoid

1. **Destructive beautification.** **must avoid**
   - Conversion, reflow and auto-format in Nebo can only be undone with undo, and users say auto-format "cannot be undone".
   - Inkwell: raw strokes are immutable. Neatening and snapping are stored transforms, with a per-line and per-page "show original" toggle.
2. **Smart behaviour you can't turn off, especially on maths and graphs.** **must avoid**
   - Fraction bars snapped to lines, graph boxes "adjusted", Greek letters "corrected" (≥24 reviews).
   - Inkwell needs:
     - a global toggle for each behaviour
     - maths and diagram skip by default
     - a one-gesture "leave this alone" region marker
     - never acting on long horizontal strokes with ink above and below (fraction bars)
3. **Sync that makes "conflicted copies" and duplicates, behind an account and a hidden proprietary format.** **must avoid**
   - Inkwell: a plain iCloud Drive folder with one package per notebook and one file per page.
   - Use NSFileCoordinator and NSFilePresenter, and resolve conflicts with NSFileVersion. Merge per page where possible, otherwise keep both versions *inside the same notebook* with a visible badge.
   - No account.
4. **No automatic backups, and deletes that can't be recovered.** **must avoid**
   - Nebo: "We do not keep copies or backups of your notes". Deleted pages "cannot be recovered".
   - Inkwell: automatic rolling local snapshots, a page-level trash, and no destructive "Optimise PDF" (Nebo's is irreversible).
5. **Performance cliffs on long notes and big PDFs.** **must avoid**
   - Nebo shows orange and red banners warning that staying on a page "could cause data loss".
   - Inkwell: tile-render PDFs lazily (PDFKit plus a CATiledLayer approach), virtualise pages in the vertical scroll, and save incrementally per page.
6. **Two-level folders and slow page adding.** **must avoid**
   - Inkwell: unlimited nesting, and adding a page should take 0–1 taps (scrolling past the last page or a single "+" at its foot).
7. **Asking the user to label content type on every conversion (the Text/Math popup).** **should avoid**
   - Inkwell: guess by heuristic and let a one-tap override correct it. Remember the choice per region.
8. **The language locked at note creation.** **should avoid**
   - Inkwell: one global English setting, changeable at any time, then re-index.
9. **Feature creep away from the core (AI, study spaces) while basics regress.** **should avoid**
   - Repeated "used to be better" reviews. Keep the slice small and solid.
10. **The Mac as an afterthought.** **should avoid**
    - Nebo runs the iPad build on Apple silicon. Reviews mention crashes on MacBook Air and login problems.
    - Inkwell's Catalyst build should be tested as a first-class *reader and organiser*, with pointer and keyboard, from day one.

### Note on what is achievable on-device (no MyScript SDK)

- **Easy and reliable:**
  - scratch, join and split detection by geometry
  - hold-to-snap shape fitting
  - undo gestures
  - insert space
  - iCloud folder sync
- **Medium:**
  - cursive search with Apple Vision (test on Luca's real lecture pages early)
  - maths, text and diagram region heuristics
- **Hard or optional:**
  - handwriting-to-LaTeX (needs a custom Core ML model)
  - Nebo-level cursive-to-text conversion quality
- The iink SDK is commercial. Old forum answers mention about 100 free dev licences and paid production packs. Current pricing is unverified, so it is not worth it for a personal app.
