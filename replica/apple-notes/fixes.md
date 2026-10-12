# Apple Notes (Smart Script, Math Notes, Pencil): what users hate, what's missing, what's unsolved

**Sample:** 105 verbatim items from 45 distinct pages across 4 sources: Apple Support Community (60 items, 24 threads), MacRumors Forums (21 items, 4 threads), Hacker News (16 comments, via the official Algolia API), and MacStories (8 excerpts from one hands-on review, which counts as press, not a user). None has star ratings, since Notes has no store reviews. Dates run 2020-10 to 2026-01, with 2024-25 dominant (iPadOS 18 launch of Smart Script/Math Notes). Reddit was **not** reachable: both `reddit.com` and its JSON endpoint were blocked (HTTP block and browser "site not allowed"), so there are no Reddit items. Apple Community and MacRumors blocked plain HTTP fetching (bot check), so those threads were read in the browser one page at a time.

**Counting method:** `feedback.md` is the automatic keyword ranking from `reviews.py` with the adapted `themes.json`. Keyword matching mis-files some rows (e.g. Math Notes *praise* lands in the "math intrusive" theme), so the counts below come from **hand-coding each of the 105 rows** into one primary theme. Row numbers refer to the order in `reviews.csv` (0-based, newest first). Bias warning: support forums over-sample problems, and threads were found by searching for problems. Treat these as frequencies of complaint *types*, not of how common they are among users.

## 1. What they hate (ranked by items, then by source spread)

1. **Spell-check underlines and "corrections" on handwriting.** Blue dots everywhere, suggestions unrelated to what was written, and the replacement doesn't match the pen. It couldn't be switched off for about a year. **15 items, 4 threads, 2 sources** (Apple Community, MacRumors). Users report a toggle arrived in iPadOS 26 (3 more items, rows 4–6).
   - "I have blue dots under most handwritten words. If one clicks on the word a completely different word gets suggested?" ([MacRumors, 2025-01-20](https://forums.macrumors.com/threads/ipados-cannot-disable-spellcheck-in-handwritten-notes.2429349/))
   - "imagine going back to refer my notes and i get 200+ spelling underlines." ([Apple Community, 2024-11-27](https://discussions.apple.com/thread/255769701))
2. **Lag, heat and dropped input on long handwritten notes.** **11 items, 2 threads + 1 review, 2 sources** (Apple Community, MacStories). Users' workaround is to type a text line to "break" the drawing, or to start a new note.
   - "This is especially prominent as the size of the notes increase (i.e. more than 4 - 5 pages). At this point, the current note is completely unusable." ([Apple Community, 2022-10-31](https://discussions.apple.com/thread/254333517))
   - "if I’m furiously taking notes and refinement kicks in while I’m writing, Notes will stop accepting my writing for a beat" ([MacStories, 2024-08-29](https://www.macstories.net/stories/ipados-18s-smart-script-a-promising-start-but-dont-toss-your-keyboard-out-yet/))
3. **Maths detection fires when not wanted.** Writing "=" triggers solving, red error underlines, and autofill of a previous variable. You can switch it off per note but there's no global default-off. **10 items, 5 threads/stories, 2 sources** (Apple Community, HN).
   - "The equal sign should not be the “switch” to disable this ”feature.”" ([Apple Community, 2025-02-13](https://discussions.apple.com/thread/255970121))
   - "I use notes with pencil to help my kids with their math homework and it started randomly trying to solve what I was writing." ([HN, 2024-11-08](https://news.ycombinator.com/item?id=42091305))
4. **Neatening/auto-correction changes what was written.** Wrong words substituted, words sloped or pushed off the line, colour changed, curves straightened into shapes, writing made "worse". **9 items, 8 threads/pages, 4 sources** (Apple Community, HN, MacRumors, MacStories). This is the theme with the widest source spread, and it's the one closest to Inkwell's core idea.
   - "it so often replaces my handwriting with the entirely wrong word as to be infuriating. On top of that, it often does so long after I wrote it so I might not even notice that it happened until I try to read the note back later." ([HN, 2024-11-09](https://news.ycombinator.com/item?id=42094512))
   - "Without warning, it will move part of a line of my handwriting in Apple notes above or below the line on which the rest of the content is written" ([Apple Community, 2024-12-18](https://discussions.apple.com/thread/255892247))
5. **Feature hidden, missing on a device, or stuck "downloading".** **9 items, 5 threads, 2 sources** (Apple Community, MacRumors). Of these, 6 are about availability ("will download when connected to Wi-Fi" while on Wi-Fi, missing on some iPads) and 3 about discoverability (toggle buried in the tool picker's "…", paste only appears when long-pressing next to existing writing).
   - "Apple certainly has a way about burying the settings for featured features in obscure places." ([MacRumors, 2024-06-11](https://forums.macrumors.com/threads/notes-handwriting-correction.2428842/))
   - "You don’t get the insertion cursor unless you long press next to a handwritten letter. It took me several hours to figure this out." ([MacRumors, 2024-09-22](https://forums.macrumors.com/threads/notes-paste-as-handwriting-doesnt-seem-to-work.2437483/))
6. **Handwriting vanishes or a note reverts (sync/crash).** **8 items, 4 threads, 2 sources** (Apple Community, HN). Most are 2022–2024 (iPadOS 16–17), so they may be partly fixed.
   - "the app just crashed and suddenly all my hours of notes progress was lost" ([Apple Community, 2023-08-07](https://discussions.apple.com/thread/255050173))
   - "I then found that the note reverted to an earlier state, missing a few hours of updates. The timestamp on the note was current, but the content was old." ([Apple Community, 2024-02-15](https://discussions.apple.com/thread/255050173))
7. **Apple Pencil Pro barrel roll / squeeze misbehaving in Notes.** **8 items, 3 threads, 1 source (thin: Apple Community only).** Barrel roll changes the nib angle of the pen unexpectedly, there's no off switch, magnetic cases interfere, and squeeze shows only undo/redo.
   - "the barrel roll changes direction constantly when writing without rotating it and as well every time you switch between tools" ([Apple Community, 2024-05-28](https://discussions.apple.com/thread/255613792))

## 2. What's missing (features asked for by name)

1. **An off switch / opt-in for every automatic behaviour** (maths, spell-check, refine, barrel roll), ideally default-off and per note. **10 items, 2 sources** (Apple Community, HN). This overlaps with hate #1/#3.
   - "there is no way to default it to off, which I have seen some people request." ([HN, 2024-11-09](https://news.ycombinator.com/item?id=42092704))
   - "Sometimes a tool just shutting the hell up is a good thing." ([HN, 2024-11-09](https://news.ycombinator.com/item?id=42091851))
2. **Precise insert-space / reflow / paste in handwriting.** **5 items, 3 sources** (HN, MacRumors, MacStories).
   - "If I need to go back and add a sentence or two mid note I can try to draw a line to make space but it rarely works like one would expect." ([HN, 2024-11-09](https://news.ycombinator.com/item?id=42094512))
3. **Faithful export: all pages to PDF, and handwriting staying vector/searchable on other devices.** **4 items, 2 sources** (HN, Apple Community), plus Apple's own doc: "the exported PDF contains only the first page of the original PDF" ([Apple](https://support.apple.com/guide/ipad/export-or-print-notes-ipad50c393a8/27/ipados/27)).
   - "The built in Notes app is garbage for handing in multi-page PDFs, bafflingly this is impossible" ([HN, 2024-11-09](https://news.ycombinator.com/item?id=42096862))
4. **Handwriting stabilisation (jitter smoothing).** **3 items, 1 thread, 1 source (thin).**
   - "Why hasn’t there been any attempt to include a handwriting stabilization feature, or am I missing something?" ([Apple Community, 2023-06-30](https://discussions.apple.com/thread/254964555))
5. **More serious maths** (calculus, linear algebra notation, typed column sums, unit handling). **3 items, 1 source (thin, HN).**
6. **Show what the recogniser understood**, so you can trust it. **2 items, 1 source (thin, HN).**
   - "I need to be able to spot and fix misinterpretations as quickly as possible, otherwise errors accumulate real fast." ([HN, 2024-11-09](https://news.ycombinator.com/item?id=42093012))
7. **Better handling of capitals / non-Latin scripts.** **2 items (thin).**

## 3. What's unsolved (jobs and groups Notes doesn't serve)

1. **Long-form lecture note-taking.** Notes is one long canvas that lags after a few pages, can't hand in multi-page PDFs, and exports badly. **~6 items** (rows 40, 91, 96, 98, 100, 11), **2 sources**. This is exactly Luca's use case (university lectures plus work).
2. **People who want their own ink left alone.** For them, handwriting's value is that it is *not* text. **5 items, 2 sources** (MacRumors, HN).
   - "the whole purpose of handritten notes is to not be like text. I want colors, line styles, different placement, size and tilt of words." ([MacRumors, 2024-06-16](https://forums.macrumors.com/threads/ipados-cannot-disable-spellcheck-in-handwritten-notes.2429349/))
   - "when I see my handwriting transform into printed symbols, I feel as if the system stole it from me." ([HN, 2024-11-10](https://news.ycombinator.com/item?id=42099870))
3. **Maths-heavy writers who use maths to think, not to compute.** Notes either interrupts with answers and red underlines, or (for anything past arithmetic) does nothing useful. There's no "this is maths, leave it alone" mode. **4 items, 2 sources** (thin-ish).

**What users praise** (12 items, 3 sources). Math Notes' live demo ("If there was anything that you could show 'a vision of the future' to someone from 1980... Math Notes would be it." [MacRumors](https://forums.macrumors.com/threads/apple-unveils-calculator-app-for-ipad-with-math-notes-apple-pencil-support.2428646/page-2)). Refinement that is "subtle, but nice" ([MacRumors](https://forums.macrumors.com/threads/notes-handwriting-correction.2428842/)). Mixed drawing and writing that is all searchable without conversion ([Apple Community](https://discussions.apple.com/thread/251870395)). And the iPadOS 26 spell-check toggle.

## Fix plan for Inkwell (top items by evidence × cheapness)

| # | build / change | size | evidence |
| --- | --- | --- | --- |
| 1 | Neatening is a **separate transform layer** keyed by stroke ID. Original points are never edited, and there's a visible per-line "show original" plus a global off | M | hate #4 (9 items, 4 sources), unsolved #2 |
| 2 | **Never refine a line while the Pencil is on that line.** Neaten the *previous* line only after the Pencil moves down/away, and never drop input | S | hate #2 (MacStories), hate #4 |
| 3 | **Neatening is limited to level/rotate/scale/spacing.** No glyph re-synthesis, no word substitution, no spell-check, no colour changes | S | hate #1, #4 |
| 4 | **Maths and diagrams are skipped** by a conservative classifier. When unsure, don't touch | M | hate #3/#4, unsolved #3 |
| 5 | **Page-based storage, rendering only visible pages**, so long lectures don't degrade | M | hate #2, unsolved #1 |
| 6 | Atomic per-page files, conflict copies via `NSFileVersion`, nothing auto-deleted, and a local "last good" snapshot | M | hate #6 |
| 7 | One settings screen listing every automatic behaviour with an off switch (not buried in the tool picker) | S | missing #1, hate #5 |
| 8 | Multi-page PDF export that includes every imported page plus ink | M | missing #3 |

## Ideas for Inkwell: what Notes does brilliantly (concrete patterns, not assets)

1. **Writing starts the moment the Pencil touches.** There's no "enter drawing mode" tap, the finger scrolls, and the Pencil writes. **must**
2. **Scratch-out-and-hold to erase**, with no tool switch. Notes only accepts it if you *hold* at the end of the scratch, which prevents accidental erasing of real zig-zags. Make it undoable. **should**
3. **Draw-and-pause to snap shapes, with one undo to get the freehand back.** The pause is the intent signal, and a Pencil Pro haptic tick confirms it (`pathCompleted(at:)`). For economics diagrams (axes, straight supply/demand lines, arrows), snapping *straight lines and arrows only* is enough. Inkwell should keep the freehand stroke stored and show the snapped geometry as a transform/overlay, which matches the "never destroy ink" rule. **should**
4. **Ruler moved with one finger and rotated with two**, drawing along its edge. It's ideal for axes, and adding a haptic tick at 0°/45°/90° helps. **should**
5. **Text-like selection gestures for handwriting**: double-tap selects a word, triple-tap a line, and touch-hold-drag a range. Combined with recognition word boxes, this gives "Straighten this line" or "neaten / restore original" on a selection. **should**
6. **Hover preview**: holding the Pencil within ~12 mm shows the nib size/colour before marking (Notes does this for the highlighter and eraser). **should**
7. **Squeeze shows a palette under the nib**, and a *hidden* tool picker still responds to squeeze/double-tap (PKResponderState, iPadOS 26). Inkwell maps squeeze to the eraser, but should still respect the system `preferredSqueezeAction`. **must** (squeeze/double-tap) / **should** (hover palette)
8. **Search that just finds handwriting** without converting it. Now public via `PKStrokeRecognizer` on iPadOS 27, with stroke-ID bounds for highlighting and `UIFindInteraction` for the system find bar. **must**
9. **Subtle, learnable refinement.** Users who like Smart Script say it's subtle and doesn't look like a font. The lesson for Inkwell's geometric neatening: small corrections (baseline, slant, spacing), not makeovers. **must**
10. **Ambiguity shown as a gentle mark you can tap** (Math Notes' blue = ambiguous, red = error). It's a good pattern for "neatening skipped this line because it looked like maths", but keep it off by default and never permanent. **could**

## Pitfalls Inkwell must avoid

1. **Never replace or redraw the user's strokes.** Notes' auto-refine has no documented way to get the original ink back once refined, and users report wrong words and sloped lines discovered "long after". **must**
2. **Don't run automatic behaviour while the user is still writing on that line.** Notes drops input mid-refine. **must**
3. **Don't let one symbol (like "=") trigger anything.** Notes' "=" turns writing into computation. Inkwell has no maths features, so keep it that way. **must**
4. **No spell-check or "suggestions" on ink, ever.** It was the most-complained-about item in the sample. **must** (as a non-feature)
5. **Every automatic behaviour gets a visible, default-respecting off switch in one obvious place**, not inside the tool picker's "…" menu. **must**
6. **Don't let long notes degrade.** Notes' lag after 4–5 pages is a long-running complaint, so page-based storage and rendering are needed. **must**
7. **Don't trust sync silently.** Notes users lost hours of writing to crashes and reverts. Inkwell should save per page atomically and often, keep conflict copies, and never let a stale device overwrite newer ink. **must**
8. **Barrel roll shouldn't change a ballpoint-style pen.** Users wanted it *off* for note-taking. Apply roll only to the highlighter (chisel) if at all, with an off switch. **should**
9. **Don't hard-override system Pencil settings without telling the user.** Squeeze/double-tap are system preferences, and users got confused when squeeze did something unexpected. **should**
10. **Don't make export lossy.** Notes exports only the first page of an attached multipage PDF, and handwriting becomes an image on other devices. **must**
11. **Check whether the system "Auto-refine Handwriting" toggle leaks into Inkwell's PencilKit canvas** (one user saw the toggle's message in third-party apps). If it does, it would alter Inkwell's ink outside Inkwell's control, so it has to be tested on device before shipping neatening. **must**

## Positioning (personal app, so this is just for Luca's own clarity)

For a student who writes cursive and maths and hates apps that "fix" his handwriting behind his back, Inkwell neatens lines geometrically and reversibly, skips the maths, and never invents ink. Evidence: hate #4 (9 items, 4 sources), unsolved #2 (5 items, 2 sources).
