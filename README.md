# Workable

[![Swift](https://img.shields.io/badge/Swift-5.0-F05138?style=flat&logo=swift&logoColor=white)](https://swift.org/)
[![UIKit](https://img.shields.io/badge/UIKit-iOS-2396F3?style=flat&logo=apple&logoColor=white)](https://developer.apple.com/documentation/uikit)
[![iOS](https://img.shields.io/badge/iOS-15.0%2B-000000?style=flat&logo=apple&logoColor=white)](https://developer.apple.com/ios/)
[![Firebase](https://img.shields.io/badge/Firebase-12.19.1-FFCA28?style=flat&logo=firebase&logoColor=black)](https://firebase.google.com/docs/ios/setup)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue?style=flat)](LICENSE)

Workable is a UIKit iOS app that works as a two-sided directory for ESG-related hiring. A person signs up as an employee or as a company, fills in a short profile, and browses the other side of the market from a searchable, auto-refreshing list. It is aimed at early-stage companies hiring for ESG roles and at candidates looking for them. The app was last worked on in 2023, is still at the development stage, and is not on the App Store.

> **Context:** LaunchX summer entrepreneurship program project, 2023. The app was built for FutureGorge, the venture developed in the program.

<p align="center">
  <img src="docs/assets/workable-logo.png" alt="Workable logo" width="180">
</p>

The Xcode project, target and bundle identifier still carry the product's earlier name, ESG Connect (`ESG Connect.xcodeproj`, source in `ESGConnect/`, bundle id `com.CanDuru.ESG-Connect`).

## Features

- Sign up as a company or as an employee, each with its own profile
- Email/password sign-up and log-in, with the session restored on launch
- List of available companies or candidates, filterable by type and searchable by name or location
- Automatic list refresh every 60 seconds
- Profile tab with a personalized greeting, editable personal details, email and password change, and log out
- In-app FAQ, privacy policy and Stripe pre-payment pages, opened in a web view from links stored in Firebase
- Push notification registration through Firebase Cloud Messaging
- Firebase App Check with App Attest

## Tech stack

| Layer | What is used |
| --- | --- |
| Language / UI | Swift 5.0, UIKit, programmatic Auto Layout (only `LaunchScreen.storyboard`) |
| Backend | Firebase Auth, Cloud Firestore (`users` collection), Realtime Database (web links), Cloud Messaging, App Check (App Attest), Analytics, Crashlytics, Performance, In-App Messaging |
| Web content | WebKit (`WKWebView`) for the FAQ, privacy policy and payment pages |
| Dependencies | Swift Package Manager (Firebase 12.19.1) |

## Getting started

### Prerequisites

- macOS with Xcode 27 or later
- iOS 15.0 or later on a simulator or device (test targets require iOS 17 or later)
- A Firebase project with Auth, Cloud Firestore and Realtime Database enabled

### Installation

1. Clone the repository.

   ```bash
   git clone https://github.com/CanDuru4/workable.git
   ```

2. Open `ESG Connect.xcodeproj` in Xcode. Swift Package Manager resolves the pinned Firebase packages automatically.
3. Add your own `GoogleService-Info.plist` (see [Configuration](#configuration)).
4. Build and run the shared `ESG Connect` scheme on an iOS 15.0+ simulator or device. App Attest needs a real device; on the simulator, register a debug App Check token in the Firebase console.

### Configuration

The app has no `.env` file. Everything outside the source lives in Firebase:

| Where | Key / path | Used for |
| --- | --- | --- |
| `ESGConnect/GoogleService-Info.plist` | whole file | Firebase project credentials (git-ignored, never commit it) |
| Realtime Database (child object) | `faq` | URL opened by the FAQ screen |
| Realtime Database (child object) | `privacy_policy` | URL opened from the sign-up screen |
| Realtime Database (child object) | `payment` | Stripe pre-payment URL opened by the Subscription tab |
| Cloud Firestore | `users/{uid}` | Profile documents backing the home list and profile tab |

Without `GoogleService-Info.plist` the app shows a setup screen instead of calling Firebase. The Realtime Database URL is hard-coded in the view controllers that read it, so point those at your own instance if you fork the project.

For signed Release archives that use a custom package checkout directory, set the `FIREBASE_SOURCE_PACKAGES_DIR` build setting to the same absolute directory passed to `-clonedSourcePackagesDirPath`. Without an override, the Crashlytics symbol-upload phase uses Xcode's standard DerivedData package directory. Unsigned and simulator builds do not upload symbols.

## Project structure

```
ESG Connect.xcodeproj/          Xcode project to open
ESG Connect.entitlements        Push notification entitlement
ESGConnect/
├── AppDelegate.swift           Firebase, App Check and push notification setup
├── SceneDelegate.swift         Root view controller selection
├── TabBarViewController.swift  Home / Subscription / Profile tabs
├── Credentials/                Welcome, log in and sign up screens
├── Home/                       Searchable, auto-refreshing list and its cell
├── Profile/                    Profile, personal info, FAQ and settings cell
├── Subscription/               Stripe pre-payment web view
├── Helper/AppCheck.swift       App Attest provider factory
├── Assets.xcassets/            Colors, app icon and logos
└── Info.plist
docs/assets/                    README images
CHANGELOG.md                    Version history
```

## Screenshots

<p align="center">
  <img src="docs/assets/screenshot-1.png" alt="Workable screenshot 1" width="260">
  <img src="docs/assets/screenshot-2.png" alt="Workable screenshot 2" width="260">
  <img src="docs/assets/screenshot-3.png" alt="Workable screenshot 3" width="260">
</p>

<p align="center">
  <img src="docs/assets/screenshot-4.png" alt="Workable screenshot 4" width="260">
  <img src="docs/assets/screenshot-5.png" alt="Workable screenshot 5" width="260">
  <img src="docs/assets/screenshot-6.png" alt="Workable screenshot 6" width="260">
</p>

## License

MIT. See [LICENSE](LICENSE).

## Author

Can Duru — [canduru.net](https://canduru.net)
