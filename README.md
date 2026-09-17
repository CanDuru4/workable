[![Swift Version][swift-image]][swift-url]

# Workable
<br />
<p align="center">
  <a href="https://canduru.net">
    <img src="https://i.ibb.co/rHFr92y/Original-resized.png" alt="Logo" width="221" height="90">
    <img src="https://i.ibb.co/mXqZ5fd/The-Workable-Logo-1.png" alt="Logo" width="221" height="90">
  </a>
    <p align="center">
    This app is created with Swift to iOS platform using Firebase. Users can sign up as a company or employee, see available opportunities, and apply for them.
  </p>
</p>

## Status

This application is currently in the development stage.

## Features

- [x] Sign Up with Different User Profiles
- [x] See Available Options for Hiring or Applying
- [x] Search for Suitable Options

## Requirements

- iOS 15.0+
- Xcode 27

## Installation

Open the `.xcodeproj` directly in Xcode 27 or later. Swift Package Manager resolves the pinned dependencies automatically; CocoaPods is no longer required. Firebase 12.19.1 requires iOS 15 or later (SponsorApp retains iOS 16). Test targets require iOS 17 or later.

Supply the app's existing `GoogleService-Info.plist` through the app target before using Firebase services. Missing configuration shows a setup screen without accessing Firebase.

## Photos from the Application

<p align="center">
<img src= "https://i.ibb.co/7nH3ZMG/Simulator-Screenshot-i-Phone-14-2023-07-25-at-22-50-31.png" width="400" >
<img src= "https://i.ibb.co/54qwzVd/Simulator-Screenshot-i-Phone-14-2023-07-25-at-22-50-33.png" width="400" >
</p>

<p align="center">
<img src= "https://i.ibb.co/PxPdmgb/Simulator-Screenshot-i-Phone-14-2023-07-25-at-22-50-36.png" width="400" >
<img src= "https://i.ibb.co/Ld9536f/Simulator-Screenshot-i-Phone-14-2023-07-25-at-22-50-20.png" width="400" >
</p>

<p align="center">
<img src= "https://i.ibb.co/znZTZxj/Simulator-Screenshot-i-Phone-14-2023-07-25-at-22-50-22.png" width="400" >
<img src= "https://i.ibb.co/b6myxkR/Simulator-Screenshot-i-Phone-14-2023-07-25-at-22-50-24.png" width="400" >
</p>

## Meta

Can Duru , canduru2004@gmail.com, support@canduru.net


[https://github.com/CanDuru4](https://github.com/CanDuru4)

[swift-image]:https://img.shields.io/badge/swift-5.0-orange.svg
[swift-url]: https://swift.org/

For signed Release archives using a custom package checkout directory, set the `FIREBASE_SOURCE_PACKAGES_DIR` build setting to the same absolute directory passed to `-clonedSourcePackagesDirPath`. Without an override, the Crashlytics phase uses Xcode's standard DerivedData package directory. Missing scripts fail with a setup instruction. Unsigned builds and simulator builds do not upload symbols.
