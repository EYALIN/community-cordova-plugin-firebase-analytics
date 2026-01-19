# Changelog

All notable changes to this project will be documented in this file.

## [1.1.0] - 2026-01-18

### Changed
- Updated default `ANDROID_FIREBASE_BOM_VERSION` from `33.8.0` to `34.7.0`
- Updated default `IOS_FIREBASE_POD_VERSION` from `11.12.0` to `12.7.0`

### Note
- Android Firebase BOM v34+ removes all Kotlin extensions (KTX) modules - they are now included in main modules
- iOS Firebase SDK 12.x requires Xcode 16.2 and CocoaPods 1.12.0 or higher

## [1.0.0] - 2025-01-18

### Changed
- Forked from [cordova-plugin-firebase-analytics](https://github.com/chemerisuk/cordova-plugin-firebase-analytics) v8.0.8
- Renamed plugin to `community-cordova-plugin-firebase-analytics`
- Updated default `ANDROID_FIREBASE_BOM_VERSION` to `33.8.0`
- Updated default `IOS_FIREBASE_POD_VERSION` to `11.12.0`
- Updated repository URLs to EYALIN organization
- Updated package.json to follow community plugin conventions
- Updated README with new installation instructions
