# Xcode 12.2 Release Notes

Update your apps to use new features, and test your apps against API changes.

## Overview

Xcode 12.2 includes SDKs for iOS 14.2, iPadOS 14.2, tvOS 14.2, watchOS 7.1, and macOS Big Sur 11. The Xcode 12.2 release supports on-device debugging for iOS 9 and later, tvOS 9 and later, and watchOS 2 and later. Xcode 12.2 requires a Mac with Apple silicon running macOS Big Sur 11 or later, or an Intel-based Mac running macOS Catalina 10.15.4 or later.

### Devices

#### Known Issues

*   Xcode may spontaneously lose device configuration information for an Apple Watch. This data loss may cause Xcode to either crash or display an error stating that your app “cannot be installed on (null)”. (54768855)

*   Xcode 11 and 12 may fail to prepare a wirelessly connected iOS device for debugging with the error “Failed _shouldMakeReadyForDevelopment check”. Even if Xcode prepares the device successfully, the Devices and Simulators window may continue to display stale errors for the device’s status. (61227501) (FB7649607)

*   Xcode may fail to copy symbols from iOS devices, and fail to prepare the devices for debugging, then take several minutes to attach to the debugger and reach breakpoints that would normally be reached immediately on launch. (68221778) (FB8611135)

### Documentation Viewer

#### Known Issues

*   Xcode may crash when opening the Documentation Window if you installed Xcode outside of `/Applications`. (70631583)

### Swift

#### Known Issues

*   Compiling a project with Mac Catalyst that imports [OSLog](https://developer.apple.com/documentation/oslog) from Swift may fail. (68597591)
