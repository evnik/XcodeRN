# Xcode 12.2 Beta Release Notes

Update your apps to use new features, and test your apps against API changes.

## Overview

Xcode 12.2 beta includes SDKs for iOS 14.2, iPadOS 14.2, tvOS 14.2, watchOS 7.1, and macOS Big Sur 11. The Xcode 12.2 beta release supports on-device debugging for iOS 9 and later, tvOS 9 and later, and watchOS 2 and later. Xcode 12.2 beta requires a Mac with Apple silicon running macOS Big Sur 11 or later, or an Intel-based Mac running macOS Catalina 10.15.4 or later.

### Build System

#### Resolved Issues

*   `xcodebuild` no longer incorrectly double-escapes the output of `xcodebuild -showBuildSettings -json`. (63554669)

### Playgrounds

#### Known Issues

*   Xcode may show the text “No editor”, instead of opening the source editor of a Playground immediately after creating it. (56484197)

    **Workaround**: Use View > Navigators > Project to reveal the Project Navigator, then select the Playground manually.
