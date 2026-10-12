# Inkwell

Personal handwritten notes app for iPad (Apple Pencil Pro) and Mac (Catalyst). Plan: `PLAN.md`. Manual steps for Luca: `NOTES.md`. Competitor research: `replica/research.md`.

## Layout
- `NoteCore/`: Swift package with no UI. Model, op log, merge, file store, neatening and search. Most logic and tests live here.
- `Inkwell/`: the app (SwiftUI shell, UIKit + PencilKit canvas, PDFKit). Keep it thin and push logic into NoteCore.

## Commands (fill in when issue #1 lands)
- Core tests: `swift test --package-path NoteCore`
- App tests: `xcodebuild test -scheme Inkwell -destination 'platform=iOS Simulator,name=<iPad>'`
- Lint: `swiftlint`

## Platform
Deployment target iPadOS 27 / macOS 27 (Catalyst). Search uses `PKStrokeRecognizer`. Don't use PaperKit, because it isn't available on Catalyst.

## Hard rules
- **Raw ink is immutable.** Neatening, snapping and erasing create new operations or variants and never mutate stored points. Every transform has tests showing the input is unchanged and that revert restores the exact original.
- **Each device writes only its own log** (`devices/<deviceID>/`). Merge is deterministic. Concurrent edits to the same object keep both versions and flag a conflict. Never last-writer-wins on user content.
- Predicted touches are never saved. Smoothing is applied when drawing, not baked into stored points.
- Maths is never neatened. Every smart behaviour has an off switch, and no UI ever pops up over the canvas.
- Everything stays on-device: no network calls, accounts or analytics.
- The free Personal Team means no iCloud entitlement. Sync goes through a user-picked iCloud Drive folder (security-scoped bookmark).
- Check current Apple APIs in the official docs before relying on them. Say so when something is uncertain.
- Never copy GoodNotes or other apps' names, icons, templates or copy.

## Workflow
- Driven by issues: `/process-issue <n>`. One branch per issue, small commits referencing `#n`, push after every commit, open a PR, CI job `ci` must pass.
- PR bodies end with: what was built, what was tested and how, what is untested, risks, and **manual iPad checks for Luca**.
- Never commit notes, samples, `replica/screens/`, signing files or secrets.
