# Xcode 12.1 Release Notes

Update your apps to use new features, and test your apps against API changes.

## Overview

Xcode 12.1 includes SDKs for iOS 14.1, iPadOS 14.1, tvOS 14, watchOS 7, and macOS Catalina 10.15.6. The Xcode 12.1 release supports on-device debugging for iOS 9 and later, tvOS 9 and later, and watchOS 2 and later. Xcode 12.1 requires an Intel-based Mac running macOS Catalina 10.15.4 or later.

### General

#### Resolved

*   Fixed a bitcode issue that could cause App Store processing to fail, resulting in an “ITMS-90562: Invalid Bundle” error in App Store Connect. (69121373) (FB8708120)

### Metal

#### Resolved

*   Fixed an issue that could cause Metal Debugger to show empty Summary and Memory reports when debugging. (68599136)
