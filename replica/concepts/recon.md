# Recon map: Concepts by TopHatch (iPad; Mac status unverified, see below)

Scope: the drawing and diagram tools only. That means precision tools (shape guides, snap, shape recognition, measure, grids), the tool selection UI (tool wheel and tool bar), the vector stroke model (select, nudge, slice, mask), undo and history, layers, gallery and folders, import and export (including PDF), sync, Apple Pencil features, and the Mac question. Not a clone: Luca's note-taking app Inkwell will borrow patterns from it.
For: Luca's Inkwell. Personal, iPad Pro M4/M5 with Pencil Pro, plus Mac Catalyst. Cursive English notes with maths and economics diagrams.
Date: 2026-10-12

Out of this study, as briefed: the object library and marketplace, collaboration and business plans, and subscription detail beyond context. No screenshots were saved. No binaries, source code or private APIs were used. Nothing below copies Concepts names, icons, assets or marketing copy into Inkwell. Where a Concepts feature name appears (for example "Nudge" or "Slice"), it only identifies that feature for this research. Inkwell must use its own names.

## Sources

| # | source | URL | notes |
| --- | --- | --- | --- |
| 1 | Manual, index | https://concepts.app/en/ios/manual/ | 17 sections |
| 2 | Manual, Precision Tools | https://concepts.app/en/manual/precision-tools | grids, snap, measure, shape guides, shape recognition |
| 3 | Manual, Workspace | https://concepts.app/en/manual/workspace | tool wheel and tool bar, UI modes, undo gestures |
| 4 | Manual, Selection | https://concepts.app/en/manual/selection | lasso, item picker, popup, transforms |
| 5 | Manual, Brushes and Tools | https://concepts.app/en/manual/brushes-and-tools | brushes, Nudge, Slice, masks, text, smoothing |
| 6 | Manual, Layers | https://concepts.app/en/manual/layers | auto sorting, focus mode, 5-layer free limit |
| 7 | Manual, Infinite Canvas | https://concepts.app/en/manual/infinite-canvas | navigation, artboard, stylus |
| 8 | Manual, Settings | https://concepts.app/en/manual/settings | gestures, tap-and-hold, draw-and-hold, stylus |
| 9 | Manual, Gallery | https://concepts.app/en/manual/gallery | folders, file storage, iCloud sync |
| 10 | Manual, Export / Import / PDF | https://concepts.app/en/manual/export , /import , /pdf | formats, regions, PDF placement |
| 11 | Pencil Pro page | https://concepts.app/en/apple-pencil-pro-squeeze-roll/ | squeeze, double-tap, barrel roll (6.14+) |
| 12 | iOS roadmap / changelog | https://concepts.app/en/ios/roadmap/ | 6.12 iCloud Drive (Apr 2024), 6.14 Pencil Pro, 6.23 shape recognition (Mar 2025), 6.31 recognition snapping fixes, 6.36 (Sep 2026) |
| 13 | App Store lookup API | https://itunes.apple.com/lookup?id=560586497 | v6.36.1 (5 Oct 2026), 4.74 stars from 26,556 ratings, 280 MB, iOS 15+ |
| 14 | Google Play listing | https://play.google.com/store/apps/details?id=com.tophatch.concepts | feature list, free versus paid split |
| 15 | User reviews | see reviews.csv / feedback.md | 916 rows |

## Core loop

Open a drawing (an infinite canvas), pick a tool from the wheel, draw strokes. Every stroke stays a vector object that can be reselected, nudged, sliced, recoloured, resized or moved. Optional precision aids (guides, snap, recognition) constrain strokes as they are drawn.

## Screens

| ID | screen | how to reach | purpose | key components | states seen |
| --- | --- | --- | --- | --- | --- |
| S01 | Gallery | app launch | browse drawings and folders | sidebar (top-level folders, iCloud location, Recents (6.33), Recently Deleted), grid of thumbnails, "+" create menu, group/sort controls, folder notes field | empty, filled, nested folder, iCloud folder |
| S02 | Create menu | "+" in S01 | new drawing, folder, import (Files, Photos, clipboard, camera, recently imported) | popover list | n/a |
| S03 | Canvas (workspace) | open drawing | draw | status bar, tool wheel or tool bar, precision panel, layers panel, edge pointers to off-screen strokes | normal, compact, hidden UI; left-handed mirror |
| S04 | Tool wheel | on S03, floating | tool and preset switching | outer ring of up to 8 tool slots; inner ring with size, opacity, smoothing; centre colour; undo/redo at the side | normal, docked in a corner (compact), scaled by pinch |
| S05 | Brushes menu | tap the active tool, or double-tap an inactive slot | pick a brush or tool for a slot | brush list, presets, My Brushes, brush packs | free versus locked |
| S06 | Size / opacity / smoothing slider | tap an inner-ring control | adjust the value | 4 size presets, slider, tap-and-hold to type a value | open while sliding |
| S07 | Colour wheel and colours menu | tap or hold the wheel centre | colour pick | HSL, RGB and COPIC wheels, palettes, vector colour picker | n/a |
| S08 | Precision panel | status bar Precision toggle | toggle Grid, Snap, Measure, Guide, Recognition | checkbox rows, each with settings on the other side | minimised, expanded |
| S09 | Shape guide on canvas | Precision > Guide | constrain strokes to a line, arc, angle, ellipse or rectangle | grey template, handles, centre crosshairs, measurement labels | active, measured |
| S10 | Snap options | Precision > Snap > Options | snap and align behaviour | Snap to Grid, Align to Grid, Allow Traceback, Allow Turns, Auto-complete, Active Layer Only, Snap While Editing (to grid or key points) | n/a |
| S11 | Grid settings | Precision > Grid name, or Settings > Workspace | grid type and look | 5 basic and 3 perspective grids, spacing, divisions, weight, colour, orientation, confine to artboard | grid layer edit mode |
| S12 | Selection menu and popup | tap-and-hold the canvas, or the Selection tool | select and act on strokes | bottom filters (type, partial, lock, layers); popup with copy, duplicate, group, lock, delete, flip; transform toggles (rotate, scale/stretch/off) | lasso, item picker, colour picker; nudge ghost |
| S13 | Layers panel | status bar Layers | layer management | list, new layer, Automatic/Manual sorting toggle, eye icons, options menu (select all, lock, duplicate, delete, merge down, rename, opacity) | focus mode |
| S14 | Measurement popup | tap the measurement field in the status bar | exact length, size and rotation | editable values, ratio lock chain | single stroke, multiple, fill |
| S15 | Export sheet | status bar Export | export | format (JPG, PNG, PSD, PDF flattened or vector, SVG, DXF, .concept), region (screen, entire drawing, artboard, PDF bounds, selection), ppi, options | progress, preview (6.30) |
| S16 | PDF page tray | import a multi-page PDF | place pages | scrollable side tray of pages, dragged onto the canvas | hidden or shown |
| S17 | Settings | status bar | Workspace and Interaction tabs | backgrounds, grid, artboard, units, tool setup; touch input (finger action, 2/3/4-finger taps, tap-and-hold, draw-and-hold), stylus (pressure, tilt, barrel roll, hover, squeeze/double-tap action) | n/a |
| S18 | Pro store | status bar or gallery | purchase | plans | out of scope |

## Flows (happy-path tap counts, inferred from the manual; not timed on a device)

```
F01 Draw a straight line with a guide
    S03 -> S08 Precision -> tick Guide (Line default?) -> drag handles -> draw along -> untick Guide
    happy path taps: 3 to turn on and position, plus the stroke, plus 1 to turn off = about 5
    edge: guide handles grabbed by accident while drawing (2014 review); guide
          stays on screen until manually toggled off
```
```
F02 Draw a perfect circle by shape recognition
    S03: draw roughly, hold the Pencil still at the end (default about 0.5 s) -> shape snaps -> keep moving the Pencil to scale/rotate -> lift
    happy path taps: 0 extra (hold-to-trigger)
    edge: natural pauses trigger it (1-star review); unwanted arrowheads/odd
          shapes (3-star review, 2026); manual does not say how to revert to the raw stroke (likely undo)
```
```
F03 Fix one stroke after drawing (vector edit)
    S03: tap-and-hold the canvas -> lasso the stroke -> drag / pinch / rotate -> tap away
    happy path taps: 2 plus the gesture
    Nudge: pick the Nudge tool in a wheel slot -> push the stroke like string
    edge: lasso picks up hidden or masked strokes (several reviews)
```
```
F04 Switch pen to highlighter-equivalent and back
    S04: tap the other wheel slot (1 tap) ... tap back (1 tap)
    happy path taps: 2
```
```
F05 Change pen size
    S04: tap the size ring -> tap preset (2), or tap-hold-slide on the size ring (1 gesture)
```
```
F06 Undo
    two-finger tap (gesture, configurable) or the wheel's undo button: 1
    no documented multi-step history scrubber in the current manual (see the data model)
```
```
F07 Erase part of a stroke
    pick Slice (destructive vector cut) or Hard/Soft Mask (non-destructive) in a wheel slot, then rub
    happy path taps: 1 plus the gesture
    edge: masks move separately from strokes and confuse users (4+ reviews)
```
```
F08 New drawing in a nested folder
    S01 -> open folder -> open subfolder -> "+ New Drawing"
    happy path taps: 3 (folders) + 1 = about 4; no paper picker on creation (grid/background is set in S17/S11 after)
```
```
F09 Annotate a PDF and export it
    S03 Import -> Files -> pick PDF -> drag pages from tray S16 -> annotate -> Export -> PDF -> region "PDF Bounds" + "Original Pages" -> share
    happy path taps: about 10
    edge: multi-page export only via PDF Bounds; vector export loses width and texture; paid feature
```
```
F10 Sync to another device
    S01: drag drawings into the iCloud sidebar location (iOS only, since 6.12)
    edge: no cross-platform format (.concept vs .concepts); no Mac app found; conflict handling is not documented
```

## Components

| component | variants | states | used on |
| --- | --- | --- | --- |
| Radial tool wheel | full, docked/compact, scaled; left or right side | slot active, slot locked (paid), slider open | S03, S04 |
| Linear tool bar | normal, compact | same | S03 (alternative to the wheel) |
| Precision panel row | checkbox plus settings | on/off, minimised | S08 |
| On-canvas guide | line, arc, angle, ellipse, rectangle | active, handle-drag, crosshair double-tap "perfect" mode, measured | S09 |
| Selection bottom bar | filter toggles; transform toggles | lasso, picker, colour picker | S12 |
| Contextual popup | selection actions | n/a | S12, PDF |
| Layer row | normal, active, focus, locked, hidden | auto vs manual sorting | S13 |
| Status bar fields | zoom/angle/measure | tap = popup, hold = inline edit, double-tap zoom = recentre | S03 |
| Toast | "Editing Grid" with Done | n/a | S11 |
| Gallery thumbnail | drawing, folder | hold menu (rename, duplicate, delete, share) | S01 |

## Inferred data model (guesses unless stated)

```
Drawing       id, name, folder_id, created_at, updated_at, background (paper/colour),
              grid (type, spacing, divisions, weight, colour, orientation, confine),
              artboard (w, h, units) | null, drawing_scale (1:n), units,
              layers[], measurements_layer, notes
              evidence: S01, S11, S17, Gallery + Precision manual pages
              confidence: high (fields), medium (structure)
              file: .concept package on iOS (.concepts on Windows/Android, incompatible)
              stored in "On My iPad/Concepts" visible in Files; iCloud location is a separate root

Folder        id, name, parent_id, description(notes -> Notes.txt per folder, roadmap 6.0)
              confidence: high (nesting is stated; the Notes.txt detail is from the roadmap)

Layer         id, name, order, visible, locked, opacity (default 100), is_auto (keyed by tool family)
              auto rule: new layer per tool family the first time it is used; pens share one, pencils share one
              special layers: Grid layer, Measurement layer, Image layer (bottom)
              confidence: high

Stroke        id, layer_id, brush_id, colour (rgba), size, opacity, smoothing (0..100%),
              raw_points[] (x, y, pressure?, tilt?, azimuth?, velocity?, t),
              rendered_path (smoothed), group_id | null, locked, kind (stroke | fill | mask_hard | mask_soft | text | image | pdf_page)
              evidence: brushes respond to pressure/tilt/velocity; 100% smoothing collapses to a
                start-end line, so smoothing is applied to stored input on render, not baked into
                the points; Nudge "has fewer points to edit" on 100%-smoothed strokes;
                masks stay editable (non-destructive); Slice is destructive (splits strokes);
                properties are "adjustable after drawing"
              confidence: medium. Whether raw points are kept separately from smoothed output after a
                smoothing change is a GUESS, but very likely given that smoothing is described as
                adjustable per stroke after the fact.
              raster add-ons: Dynamic Pen, Dotted, many market brushes carry a raster layer
                over the vector (bigger files, pixelation).

Mask          stroke with kind=mask_*; hides strokes under it on the same layer; does not move with
              selected strokes (user complaints) -> masks are separate objects, not stroke edits
              confidence: medium-high

ShapeGuide    type (line|arc|angle|ellipse|rect), handles[], centre, rotation, constrained(bool via
              crosshair double-tap), measure label; one active guide per drawing (guess)
              confidence: medium

Measurement   id, target_stroke_id | null (static), value, units, position along stroke
              confidence: high

Brush         id, family, type (stamp|reveal), stamps[], grain, size/opacity/smoothing presets,
              pressure/tilt/velocity curves, spacing/scatter/rotation, target_layer
              confidence: high (custom brush editor)

ToolSlot      wheel_index (0..7), brush_id, preset values (size, opacity, smoothing, colour)
              confidence: high

UndoStack     linear per drawing, gesture driven (2-finger undo / 3-finger redo default).
              History: reviews from 2013–2014 describe an undo facility letting one "move through
              the entire creative process" and layers that "reach back in time". The current manual
              documents no history slider. Status of a history slider today: UNVERIFIED (likely
              removed in the v5/v6 redesigns).
```

Relationships: Folder 1-n Folder, Folder 1-n Drawing, Drawing 1-n Layer, Layer 1-n Stroke (incl. masks, text, images), Drawing 0-1 ShapeGuide active, Stroke 0-1 Measurement, ToolSlot n-1 Brush.

## Pencil and input facts (from the manual and the Pencil Pro page)

- Squeeze and double-tap (6.14+): configurable action. The examples given are switching tools and colours, activating nudge or selection, and canvas navigation. 6.15 lets squeeze open the tool wheel at the Pencil. Most options are shared with double-tap. A 2025 user still asked for "double tap or squeeze ... to undo", so undo may not be offered, or may be hard to find (unverified).
- Barrel roll: rotates the brush stamp, for example marker chisel or graphite. It has an on/off toggle only.
- Hover: shows a brush-stamp preview (M2 and later).
- Finger action (with a stylus attached): Do Nothing, Use Active Tool, Pan, Select, Nudge, Slice, or Configured Tool.
- 2-, 3- and 4-finger taps: each can be mapped to any of 13 actions.
- Tap-and-hold (finger): selection, with an adjustable hold time.
- Draw-and-hold: shape recognition. The activation time has a slider, about 0.5 s in the manual screenshot. It recognises lines, curves, arrows, triangles, squares, rectangles, circles and ellipses, from 1 to 4 strokes. After it fires, you keep moving the Pencil to scale or rotate the shape.
- Smoothing: per tool preset, from 0% (raw) to 100% (a straight line from start to end). One HN user writes maths and handwriting at 8–12% smoothing.

## Mac version

No Concepts app turned up in a Mac App Store search through the iTunes Search API (entity=macSoftware). The roadmap and download pages list iOS, Android, Windows, ChromeOS and Samsung only. Recent reviews from 2026-05-09 and 2026-05-30 say there is no usable Mac app. One 2025 review mentions the "iPad and Mac" file. That may mean the iPad app running on Apple Silicon ("Designed for iPad"), which could not be verified. Treat it as: no native Mac app.

## Feature matrix

See `features.csv`. Must: 21, should: 15, could: 10, skip: 11 (57 rows).

## Out of scope (cannot or should not be cloned)

- The object library, its marketplace and Pexels stock: licensed or partner content.
- COPIC colour system: trademarked, licensed.
- Brush market packs and their artwork.
- Accounts, cross-platform purchases, business deployment, collaboration.
- Windows, Android and ChromeOS versions.
- CAD exports (DXF) and perspective grids: not needed for notes.

## Size (Inkwell borrowing only the diagram slice)

Screens of interest: 8 (S03, S04, S08, S09, S10, S12, S13, S15). Flows: 10. Entities: 9.
Hard parts:
1. A stroke model that keeps the raw input immutable and applies smoothing and snapping as a reversible transform.
2. Shape recognition that never fires by accident and always lets you go back to the raw ink.
3. Snapping endpoints to other strokes, axes and the grid at an angle, with clear feedback.
4. Vector selection hit-testing on large documents.
5. iCloud Drive folder sync without conflicts.

Size for Inkwell's diagram subset: M (a few weeks).
