# Which Apple Notes / Apple Pencil capabilities are available to third-party apps

Checked 2026-10-12 against Apple's developer documentation. I read each symbol's own doc page (`developer.apple.com/documentation/...`), and its availability metadata is the source for the "min OS" column. WWDC pages were read for context. "Mac Catalyst" is listed because Inkwell's Mac target is Catalyst.

Confidence key:
- **high**: the symbol page exists, and I read its availability and description.
- **medium**: the docs or a WWDC transcript say it, but I didn't verify the exact symbol/behaviour.
- **low/none**: absence of evidence. I searched and didn't find it.

## Verdict summary

| capability (as in Apple Notes) | available to Inkwell? | API | min iPadOS | Mac Catalyst | confidence |
| --- | --- | --- | --- | --- | --- |
| Smart Script **refine / straighten / auto-refine** | **No public API found** | none | — | — | medium-high (absence: the iOS 27 PencilKit index lists recognition, path conversion, slicing, stroke IDs, but nothing for refine/straighten) |
| Smart Script paste-as-handwriting / convert-to-handwriting / spell-correct in your hand | **No** | none | — | — | medium-high (absence) |
| Scratch-to-erase gesture | **No API**, so build it yourself (detect a zig-zag over strokes, then erase via stroke IDs / programmatic slicing) | none built-in | — | — | medium |
| Handwriting recognition / search / Spotlight indexing | **Yes (new)** | `PKStrokeRecognizer` | **27.0** | 27.0 | high |
| Maths recognition (handwritten equations → structure) | **No public API found**. Neither `PKStrokeRecognizer` nor Vision docs mention maths | none | — | — | medium (absence) |
| Math Notes evaluation / graphs | **No** | none | — | — | medium (absence) |
| Squeeze (Pencil Pro) | **Yes** | `UIPencilInteractionDelegate.pencilInteraction(_:didReceiveSqueeze:)`, SwiftUI `onPencilSqueeze(perform:)` | 17.5 | 17.5 (no Pencil on Mac) | high |
| User's preferred squeeze action | **Yes** (read-only) | `UIPencilInteraction.preferredSqueezeAction` | 17.5 | 17.5 | high |
| Double-tap | **Yes** | `pencilInteraction(_:didReceiveTap:)`, `onPencilDoubleTap(perform:)`, `preferredTapAction` | tap delegate: 17.5 (per Apple Pencil updates page). `preferredTapAction` 12.1 | yes | high |
| Squeeze contextual palette, the system one | **Yes, via PencilKit tool picker**. `UIPencilPreferredAction.showContextualPalette` is the user's setting; a visible-or-hidden `PKToolPicker` responds to squeeze | `PKToolPicker` + `PKResponderState.toolPickerVisibility` | `PKToolPicker` 13.0. `PKResponderState` 26.0 | 26.0 | high (docs + WWDC25 "Meet PaperKit": hidden picker "still responding to interactions like double-tap and squeeze") |
| Custom tools in the system picker (e.g. 3 pens + 2 highlighters) | **Yes** | `PKToolPicker` with tool items + `PKToolPickerCustomItem` | 18.0 | 18.0 | high |
| Barrel roll | **Yes** | `UITouch.rollAngle`; `UIPencilHoverPose.rollAngle`; PencilKit inks with roll need `PKContentVersion.version3` | 17.5 | 17.5 | high |
| Haptics on Pencil Pro (snap, path completion) | **Yes** | `UICanvasFeedbackGenerator` (`alignmentOccurred(at:)`, `pathCompleted(at:)`), SwiftUI `SensoryFeedback` | 17.5 | 17.5 | high |
| Hover (tool preview, hover distance) | **Yes** | `UIHoverGestureRecognizer.zOffset` (16.1), `UIPencilHoverPose` (17.5), `UIPencilInteraction.prefersHoverToolPreview` (17.5) | 16.1 / 17.5 | yes | high |
| Shape recognition (draw-and-hold snap) | **No public recognizer API found.** You get the haptic (`pathCompleted(at:)` is described as "path completion or shape recognition"), but you write the recogniser yourself | none | — | — | medium (absence) |
| Insert shapes / text boxes / images (markup layer) | **Yes**, via PaperKit | `PaperMarkupViewController`, `PaperMarkup`, `FeatureSet`, `ShapeMarkup` | 26.0 | **not listed** (iOS, iPadOS, macOS, visionOS only) | high |
| Ruler | **Yes** | `PKCanvasView.isRulerActive` | 13.0 | 13.1 | high |
| Stable stroke identity | **Yes (new)** | `PKStroke.id`, `PKStrokePath.id` | 27.0 | 27.0 | high |
| Read/set canvas selection + change callback | **Yes (new)** | `PKCanvasView.selection` (Set<UUID>), `PKCanvasViewDelegate.canvasViewSelectionDidChange(_:)` | 27.0 | 27.0 | high (selection page). Medium for the delegate's exact min OS (seen on the delegate page, availability not separately read) |
| Per-stroke affine transform (basis for reversible neatening) | **Yes** | `PKStroke.transform` | 14.0 | 14.0 | high |
| Bézier ↔ PencilKit conversion | **Yes (new)** | `PKStrokePath.bezierRepresentation`, `PKStrokePath.init(bezierPath:creationDate:pointProvider:)` | 27.0 | 27.0 | high |
| Substroke slicing / programmatic erase | **Yes (new)** | `PKStroke.substroke(range:)` (27.0). Programmatic erasing with a `PKStrokePath` as eraser is described in WWDC26-203, but I didn't find the symbol name | 27.0 | 27.0 | high (substroke) / medium (erase symbol) |
| Wet-ink render groups | **Yes (new)** | `PKStroke.renderGroupID` | 27.0 | 27.0 | high |
| Pencil-only drawing (finger scrolls) | **Yes** | `PKCanvasView.drawingPolicy` | 14.0 | 14.0 | high |
| Scribble (handwriting into text fields) | **Yes** (system), customisable | `UIScribbleInteraction` | 14.0 | 14.0 | high |
| Image OCR (scanned/imported PDFs) | **Yes** | Vision `RecognizeTextRequest` (18.0), `VNRecognizeTextRequest` (13.0), `RecognizeDocumentsRequest` (26.0) | 13 / 18 / 26 | yes | high (existence). The docs make no claim about handwriting or maths quality |
| Find UI over handwriting | **Yes** | `UIFindInteraction` + `PKStrokeRecognizer.search(_:fullWordsOnly:caseMatchingOnly:)` | 16.0 / 27.0 | yes | high (WWDC26-203 pairs them explicitly) |
| Spotlight search of notes | **Yes** | `CSSearchableIndex` + `PKStrokeRecognizer.indexableContent` | 9.0 / 27.0 | yes | high |
| iCloud Drive app container | **Not with a free account** | iCloud capability "iCloud documents" | — | — | high (Apple's capabilities table shows a check mark only for ADP and ADEP, none for the free "Apple Developer" tier) |
| User-chosen folder anywhere (incl. iCloud Drive), no entitlement | **Yes** | `UIDocumentPickerViewController` (folder) + security-scoped bookmark + `startAccessingSecurityScopedResource()` + `NSFileCoordinator` / `NSFileVersion` for conflicts | 8.0 / 5.0 | 13.1 | high (APIs exist). **Medium that this fully replaces a ubiquity container**: download-on-demand of evicted files and conflict behaviour need testing |

## Details and doc links

### Handwriting recognition: `PKStrokeRecognizer` (iOS/iPadOS/Mac Catalyst/macOS 27.0)
- Doc: https://developer.apple.com/documentation/pencilkit/pkstrokerecognizer
- Article: https://developer.apple.com/documentation/pencilkit/recognizing-handwriting-and-converting-to-text
- Sample: https://developer.apple.com/documentation/pencilkit/building-a-handwriting-recognition-experience-with-pencilkit
- WWDC26 session 203 "Read between the strokes with PencilKit": https://developer.apple.com/videos/play/wwdc2026/203/
- What it does (from the docs): it's a Swift `actor`, and everything is `async`. You push a `PKDrawing` with `updateDrawing(_:)`, because it doesn't observe the canvas. `recognizedText(strokeIDs:)` returns the single best string, for a subset or for all strokes. `search(_:fullWordsOnly:caseMatchingOnly:)` returns `SearchResult`s with stroke IDs and bounds. `indexableContent` gives multiple candidate readings concatenated, meant for Spotlight. `supportedLanguages`. `recognitionVersion` means you should store it and re-index when it increases.
- The session states it's on-device, with an offline model shipped with the OS, and that it "works on all devices supported by iOS 27". It supports 29 languages in iOS 27, and the Simulator only does Latin scripts.
- Apple's caveat: "Recognition works best when handwriting is scaled ... as if drawn on standard US Letter or A4 paper in points." Inkwell's iPad-shaped pages at 1:1 points should be fine, but deep zoom writing may hurt accuracy.
- The session says it's "the same powerful technology behind Apple apps like Freeform and Notes".
- **Maths:** the docs and transcript never mention maths, equations or formulae (I searched the transcript for "math", "equation", "refine", "straighten", "Smart Script" and all were absent). Treat maths recognition as **not provided**. Whether cursive English is handled well isn't stated anywhere, so test it on Luca's writing.
- **For Inkwell:** this one API covers search, Spotlight and copy-as-text on iPadOS 27+. To support iPadOS 26 you'd need a fallback, either rasterise a page and run Vision OCR, or simply require 27.

### Squeeze, double-tap, hover, barrel roll, haptics
- Apple Pencil updates (overview, May 2024): https://developer.apple.com/documentation/updates/applepencil
- `pencilInteraction(_:didReceiveSqueeze:)`, iOS/iPadOS/Catalyst 17.5: https://developer.apple.com/documentation/uikit/uipencilinteractiondelegate/pencilinteraction(_:didreceivesqueeze:)
- `UIPencilInteraction.Squeeze` (has `phase`, `timestamp`, `hoverPose`), 17.5: https://developer.apple.com/documentation/uikit/uipencilinteraction/squeeze
- `onPencilSqueeze(perform:)` (SwiftUI): https://developer.apple.com/documentation/swiftui/view/onpencilsqueeze(perform:)
- `preferredSqueezeAction`, 17.5: https://developer.apple.com/documentation/uikit/uipencilinteraction/preferredsqueezeaction
- `UIPencilPreferredAction` cases: ignore, switchEraser, switchPrevious, showColorPalette, showInkAttributes, showContextualPalette, runSystemShortcut: https://developer.apple.com/documentation/uikit/uipencilpreferredaction
- `UITouch.rollAngle`, 17.5 (0 on pencils without roll): https://developer.apple.com/documentation/uikit/uitouch/rollangle
- `UIPencilHoverPose`, 17.5: https://developer.apple.com/documentation/uikit/uipencilhoverpose
- `UIHoverGestureRecognizer.zOffset`, 16.1: https://developer.apple.com/documentation/uikit/uihovergesturerecognizer/zoffset
- `prefersHoverToolPreview`, 17.5: https://developer.apple.com/documentation/uikit/uipencilinteraction/prefershovertoolpreview
- `UICanvasFeedbackGenerator`, 17.5: https://developer.apple.com/documentation/uikit/uicanvasfeedbackgenerator. Also `alignmentOccurred(at:)` (https://developer.apple.com/documentation/uikit/uicanvasfeedbackgenerator/alignmentoccurred(at:)) and `pathCompleted(at:)`, "Triggers feedback to indicate path completion or shape recognition" (https://developer.apple.com/documentation/uikit/uicanvasfeedbackgenerator/pathcompleted(at:))
- `PKContentVersion.version3` ("supports barrel-roll angle data in inks"), 17.5: https://developer.apple.com/documentation/pencilkit/pkcontentversion/version3
- WWDC24 "Squeeze the most out of Apple Pencil" (10214): https://developer.apple.com/videos/play/wwdc2024/10214/
- **Implications for Inkwell's plan:**
  - *Squeeze = eraser.* You can implement it, but squeeze is a **system-level user preference**. Apple's guidance is to respect `preferredSqueezeAction` and offer the custom behaviour as an option. Hard-wiring squeeze to the eraser while the user's system setting is "Show tool palette" overrides the user's choice. Recommendation: on squeeze, if `preferredSqueezeAction == .switchEraser`, toggle the eraser; otherwise offer an in-app "Squeeze toggles eraser" setting, defaulting to on for Luca (personal app). Medium risk, so test that the system palette doesn't also appear when a hidden `PKToolPicker` is attached.
  - *Double-tap = palette.* The same applies. Note that `.showContextualPalette`/`.showColorPalette` already exist as user preferences.
  - *Barrel roll.* Users of Notes asked how to turn it **off** for ballpoint-style note-taking (see `fixes.md`), so make roll affect only the highlighter/fountain-pen, or nothing at all, by default.

### Tool picker
- `PKToolPicker`, 13.0: https://developer.apple.com/documentation/pencilkit/pktoolpicker
- `PKToolPickerCustomItem`, 18.0: https://developer.apple.com/documentation/pencilkit/pktoolpickercustomitem
- Article "Configuring the PencilKit tool picker", 18.0: https://developer.apple.com/documentation/pencilkit/configuring-the-pencilkit-tool-picker. Duplicate system tools need distinct `identifier`s or the picker shows only the first. That matters for "3 pens + 2 highlighters".
- `PKResponderState` / `toolPickerVisibility`, 26.0: https://developer.apple.com/documentation/pencilkit/pkresponderstate
- Inkwell plans a slim custom top toolbar. You can either hide the system picker (it stays active for squeeze/double-tap via `PKResponderState`, iPadOS 26+) and drive tools yourself, or use the system picker. Choosing a custom toolbar means rebuilding hover preview and the squeeze palette by hand.

### PaperKit (markup layer behind Notes, Freeform, Preview)
- Framework, iOS/iPadOS/macOS/visionOS 26.0. **Mac Catalyst isn't listed** in its availability: https://developer.apple.com/documentation/paperkit
- `FeatureSet.Feature`: images, stickers, loupes, links, shapeFills, shapeStrokes, shapeOpacity, text, drawing. `ShapeConfiguration.Shape`: rectangle, ellipse, line, chatBubble, roundedRectangle, regularPolygon, star, arrowShape.
- WWDC25 "Meet PaperKit": https://developer.apple.com/videos/play/wwdc2025/285/. It confirms PaperKit "powers Apple's unique markup experience system-wide. It's used in apps like Notes ...", and that Notes saves a thumbnail for forward-compatibility.
- WWDC26 "Unwrap PaperKit" (372): https://developer.apple.com/videos/play/wwdc2026/372. Its new data-model APIs to enumerate/modify markup elements were summarised from search results; I didn't read it in full.
- **For Inkwell:** PaperKit gives text boxes and shapes "for free" on iPad. Because Catalyst isn't listed, though, the Mac build would need a native macOS target or its own text-box layer. I didn't verify whether PaperKit compiles under Catalyst, so flag it to test.

### PencilKit model APIs that make reversible neatening feasible
- `PKStroke.transform`, 14.0: https://developer.apple.com/documentation/pencilkit/pkstroke-swift.struct/transform. Neatening can be expressed as per-stroke (or per-word group) affine transforms (translate, rotate, uniform scale) applied **on top of** untouched original points. You store the original drawing plus a separate "neaten layer" of transforms keyed by stroke ID; rendering applies them, and turning neatening off drops them. This never edits the original points.
- `PKStroke.id`, 27.0: https://developer.apple.com/documentation/pencilkit/pkstroke-swift.struct/id. The docs and session say it's stable across transforms, edits and undo, which makes the stroke-ID → transform map robust on 27+. On 26 you'd need your own identity (e.g. hash of creation date + first point).
- `PKCanvasView.selection`, 27.0: https://developer.apple.com/documentation/pencilkit/pkcanvasview/selection
- `PKStroke.substroke(range:)`, `renderGroupID`, `PKStrokePath.bezierRepresentation`, all 27.0.
- Article "Importing Bézier path data into PencilKit": https://developer.apple.com/documentation/pencilkit/importing-external-drawing-data-into-pencilkit. Its note: "Because the two formats represent curves differently, the conversion is an approximation", although the session says the round trip PK → Bézier → PK keeps control points. **Don't use Bézier conversion for the canonical storage of original ink.**

### iCloud / free account
- Capabilities table: https://developer.apple.com/help/account/reference/supported-capabilities-ios. "iCloud: iCloud documents" and "iCloud: CloudKit" have check marks for ADP and ADEP and **none** for "Apple Developer" (the free tier). The page footnote describes the free tier as "Apple Account holders who have agreed to the Apple Developer Agreement ... No cost ... can't distribute apps."
- Consequence: with a free account Inkwell **can't** have its own iCloud ubiquity container. The route that fits the "sync via an iCloud Drive folder" rule is to let Luca pick a folder in iCloud Drive once (`UIDocumentPickerViewController` in folder mode), persist a security-scoped bookmark, and read/write with `NSFileCoordinator`, checking `NSFileVersion.unresolvedConflictVersionsOfItem(at:)` for conflicts.
  - `UIDocumentPickerViewController`: https://developer.apple.com/documentation/uikit/uidocumentpickerviewcontroller
  - `startAccessingSecurityScopedResource()`: https://developer.apple.com/documentation/foundation/nsurl/startaccessingsecurityscopedresource()
  - `NSFileCoordinator`: https://developer.apple.com/documentation/foundation/nsfilecoordinator
  - `NSFileVersion.unresolvedConflictVersionsOfItem(at:)`: https://developer.apple.com/documentation/foundation/nsfileversion/unresolvedconflictversionsofitem(at:)
- **Not verified:** that free-account provisioning profiles expire after 7 days, requiring a re-install from Xcode. It's widely reported, but I didn't confirm it on an Apple page today. Check before relying on a free account for daily use.

### Vision (for imported PDFs / scans, and the maths question)
- `RecognizeTextRequest`, 18.0: https://developer.apple.com/documentation/vision/recognizetextrequest
- `VNRecognizeTextRequest`, 13.0: https://developer.apple.com/documentation/vision/vnrecognizetextrequest
- `RecognizeDocumentsRequest`, 26.0: https://developer.apple.com/documentation/vision/recognizedocumentsrequest
- I grepped all three doc pages for "handwrit", "math" and "equation" and got zero matches. Vision isn't documented as a maths recogniser. For Inkwell's "skip maths when neatening", you need a **heuristic classifier** (e.g. low recogniser confidence, symbols such as = + − × ÷ ∫ Σ √ ^, fraction bars, superscript-sized strokes, digits density, vertical stacking). One option is to use `PKStrokeRecognizer.recognizedText` returning `nil` or non-word output as a signal. That last idea is a design idea, not documented behaviour.

## What I couldn't verify
- Whether the **system** "Auto-refine Handwriting" toggle appears in third-party apps' `PKToolPicker` "More" menu and applies to their canvases. One MacRumors user (2024-06-16) wrote "I'm getting that message in 3rd party apps, but working in Apple Notes", and another hoped third-party apps would get it via "the new pencil kit API". There's no Apple doc on this. **Test on Luca's iPad:** add a `PKCanvasView` with a `PKToolPicker`, open "…", and look for the toggle. If it exists and is on, it would **alter Inkwell's ink**, which breaks the hard rule. Inkwell should detect it and tell Luca to keep it off (or find out if it can be suppressed).
- Exact symbol for programmatic erasing (WWDC26-203 describes it).
- Whether PaperKit can be linked under Mac Catalyst.
- `PKStrokeRecognizer` quality on cursive English and on mixed maths/text lines.
