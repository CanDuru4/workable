# Workable (ESG Connect)

UIKit iOS app: a two-sided ESG hiring directory (companies and employees browse each other) backed by Firebase. LaunchX summer program project from 2023, built for the FutureGorge venture. Dormant portfolio repo: last feature work was 2023, with a 2026 modernization pass (SPM, current Xcode). Not on the App Store. Public repo, MIT.

Stack: Swift 5.0, UIKit with programmatic Auto Layout, Firebase 12.19.1 via Swift Package Manager.

## Naming

The product is "Workable" (`CFBundleDisplayName`), but the project, target, scheme and bundle id still use the earlier name: `ESG Connect.xcodeproj`, scheme `ESG Connect`, sources in `ESGConnect/`, bundle id `com.CanDuru.ESG-Connect`. Do not rename them; the README documents the split.

## Repo map

- `ESG Connect.xcodeproj/` — the project to open. Shared scheme in `xcshareddata/xcschemes/ESG Connect.xcscheme`; pinned packages in `project.xcworkspace/xcshareddata/swiftpm/Package.resolved`.
- `ESGConnect/AppDelegate.swift` — App Check, Firebase configure, FCM push registration.
- `ESGConnect/SceneDelegate.swift` — root VC: `CredentialsViewController` in a nav controller, or a "Firebase setup required" screen when Firebase is not configured.
- `ESGConnect/TabBarViewController.swift` — Home / Subscription / Profile tabs.
- `ESGConnect/Credentials/` — welcome, `LogIn/`, `SignUp/` screens.
- `ESGConnect/Home/` — searchable list of the other side of the market, refreshed by a 60 s `Timer`.
- `ESGConnect/Profile/` — profile, personal info editing (name, email, password), FAQ web view.
- `ESGConnect/Subscription/` — Stripe pre-payment page in a `WKWebView`.
- `ESGConnect/Helper/AppCheck.swift` — App Attest provider factory.
- `ESG Connect.entitlements` — push notifications (`aps-environment` = development).
- `README.md`: features, setup, Configuration table. `CHANGELOG.md`: 0.0.0 and 1.0.0 notes (2023). `design-assets/`: logo, banner and README screenshots only.

## Commands

No CI, no Makefile, no scripts. Everything goes through Xcode (Xcode 27 per README).

- Open: `open "ESG Connect.xcodeproj"` and run the `ESG Connect` scheme on an iOS 15.0+ simulator or device.
- CLI build (simulator, unsigned):
  `xcodebuild -project "ESG Connect.xcodeproj" -scheme "ESG Connect" -destination 'generic/platform=iOS Simulator' CODE_SIGNING_ALLOWED=NO build`
- Tests: the `ESG ConnectTests` and `ESG ConnectUITests` targets exist (iOS 17.0 deployment target) but contain no source files, so there is nothing to run. A clean build is the only verification.
- Deploy: none. No App Store / TestFlight pipeline.

## Firebase and configuration

- `ESGConnect/GoogleService-Info.plist` is git-ignored and must never be committed (it is not in git history). A local copy may exist; never print or copy its contents.
- Without the plist, or with launch argument `-FirebaseSetupPreview`, the app skips Firebase and shows the setup screen. Keep that guard working.
- Firestore: `users/{uid}` with `userprofile` = `"employee"` or `"company"`. Field names differ by profile: employees use `educationstatus` / `social`, companies use `employeenumber` / `website`; both have `name`, `uid`, `location`. Sign-up and personal-info editing write the matching set, and Home filters on `userprofile`.
- Realtime Database holds the web links read at runtime: `faq`, `privacy_policy`, `payment`. The database URL is hard-coded in `SignUpViewController`, `FAQViewController` and `SubscriptionViewController`.
- App Check uses App Attest, which needs a real device. On the simulator, use a debug App Check token registered in the Firebase console.
- Crashlytics dSYM upload is a Run Script build phase that only runs for signed Release `install` builds on `iphoneos`. For custom package checkout dirs, set the `FIREBASE_SOURCE_PACKAGES_DIR` build setting (see README "Configuration").

## Conventions observed

- One view controller per screen, grouped by feature folder. No storyboards except `LaunchScreen.storyboard`; UI is built in code.
- Firebase calls happen directly inside view controllers (no service layer). Follow that pattern for small fixes rather than refactoring.
- Files use Xcode header comments and `//MARK:` section markers.
- Colors and logos come from `Assets.xcassets` (`AppBlue`, `AppBlueDarker`, `AppYellow`, `Logo`, `Logo2`).
- Deployment targets: app 15.0, test targets 17.0. The project-level setting is still 14.0; the target setting wins.

## Validation placement and reuse (owner update 2026-10-26)

- Follow the global Claude/Codex test policy and `~/Developer/personal/mac-mini/validation-economy/README.md` and `COVERAGE.md`. Focus first; full coverage only when the changed inputs require it. Docs-only policy edits need no application suite or deploy.
- Use `~/Developer/personal/mac-mini/validation-economy/remote-run.py` as the first choice for compatible heavy committed-source Python/Node checks. It defaults to `gaming-pc` and handles connection and bounded Wake-on-LAN automatically; call it directly without a separate online check or asking the owner each time. Match the pinned runtime and locked dependencies, bound actual workers, and preserve repo data-export restrictions. Never export credentials, production data, signing keys or uncommitted work.
- The PC pool shares eight CPU slots and 24 GiB across isolated jobs with zero test swap; retain automatic job cleanup, the 8 GiB package-cache budget and 128 GiB virtual-disk cap. Brain is an explicit secondary route (`--runner brain`) when compatible, capped at two CPUs and 4 GiB together. If the PC remains unavailable after bounded wake/connect, report the blocker; never silently start the same work on the Mini or replay an uncertain submitted job.
- Xcode, Swift, simulator, signing and device checks stay on the Mini. The PC Linux runner has no Apple toolchain; only compatible ancillary Python/Node checks are eligible.
- For work that must run on the Mini: manual heavy commands use `repo-run.py --repo <absolute checkout> --profile <profile> -- <command>` from the shared helper; choose from native for the actual tool. Tiny syntax checks need no reservation. Bound tool workers and reserve separate heavy phases.
- Reuse only supported receipts with matching source, coverage, dependencies, runtime/platform and relevant environment. Preserve passed unaffected batches; count remote results only when the owning gate aggregates them. Receipts do not replace required build artifacts or OS/device/browser proof. Split or offload an impossible reservation instead of waiting indefinitely; only stop your own obsolete jobs. Existing gates need explicit remote routing and matching-result aggregation; this instruction does not automatically move unintegrated commands.
