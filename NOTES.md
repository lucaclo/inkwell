# NOTES — what Luca must do by hand

## One-time setup (before issue #1)
0. **Update both devices to version 27:** the Mac to macOS 27 (System Settings → General → Software Update) and the iPad to iPadOS 27. Inkwell targets 27 for Apple's handwriting recogniser.
1. **Install Xcode** from the Mac App Store. Open it once, accept the licence, and install the iOS/iPadOS platform when it asks. Then run in Terminal:
   `sudo xcode-select -s /Applications/Xcode.app`
2. **Add your Apple ID to Xcode:** Xcode → Settings → Accounts → **+**. This creates your free "Personal Team". No $99 fee is needed.
3. **Prepare the iPad:**
   - Connect it to the Mac with USB-C and tap **Trust**.
   - Turn on Settings → Privacy & Security → **Developer Mode**, then restart the iPad.
   - After the first install, go to Settings → General → **VPN & Device Management**, tap your Apple ID, then **Trust**.
4. **iCloud:**
   - In iCloud Drive, create a folder called `Inkwell` (Files app or Finder).
   - On the Mac, right-click that folder → **Keep Downloaded**.
   - Recommended: turn on **Advanced Data Protection** (Settings → [your name] → iCloud → Advanced Data Protection). This end-to-end encrypts your iCloud Drive.

## Every week
- Free signing expires after **7 days**. Plug the iPad in, open the project in Xcode, choose your iPad as the run target and press **Run (⌘R)**. It takes about a minute.
- **Never delete Inkwell from the iPad.** Deleting it erases the iPad's local copy. Your notes are also in iCloud Drive, but don't rely on that alone.

## GitHub (once CI exists, after issue #2 is merged)
Protect `main` so a PR can only be merged when CI passes:
1. github.com/lucaclo/inkwell → **Settings** → **Branches** → **Add branch protection rule**.
2. In "Branch name pattern", type `main`.
3. Tick **Require status checks to pass before merging**.
4. Search for `ci` and select it. The search only finds it once CI has run at least once.
5. Click **Save changes**.

GitHub won't let you approve your own PR. Your workflow's "approve" step means: check that CI is green, then press **Merge**.

## The issue loop
`/process-issue <n>` → a PR is opened → CI goes green → you test on the iPad if the PR lists manual checks → merge → `/clear` → next issue.

## Manual test checklists
Each PR lists the device checks it needs. The standing checks are:
- **Writing feel:** latency, pressure and palm rejection, writing a full page of cursive.
- **Pencil Pro:** squeeze tap (eraser toggle), squeeze hold (temporary eraser), double-tap (palette), hover preview, haptics.
- **Two-device offline test:**
  1. Put the iPad and the Mac in airplane mode.
  2. Write on the same page on both.
  3. Reconnect and wait 2 minutes.
  4. Check that every stroke is present on both devices, and that any conflict shows a badge.
- **7-day reinstall:** after re-running from Xcode, all notebooks open unchanged.
- **Large PDF:** import a 300-page PDF. Check that scrolling stays smooth and the iPad doesn't get hot.

## Never commit
Your notebooks (`*.inkbook`), handwriting samples (`samples/`), GoodNotes screenshots (`replica/screens/`) and signing files. `.gitignore` already covers these.
