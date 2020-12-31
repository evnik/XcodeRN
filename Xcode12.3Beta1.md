# Xcode 12.3 Beta Release Notes

Update your apps to use new features, and test your apps against API changes.

## Overview

Xcode 12.3 beta includes SDKs for iOS 14.3, iPadOS 14.3, tvOS 14.3, watchOS 7.2, and macOS Big Sur 11.1. The Xcode 12.3 beta release supports on-device debugging for iOS 9 and later, tvOS 9 and later, and watchOS 2 and later. Xcode 12.3 beta requires a Mac with Apple silicon running macOS Big Sur 11 or later, or an Intel-based Mac running macOS Catalina 10.15.4 or later.

### Build System

#### Resolved Issues

*   Fixed an issue where `xcodebuild` sometimes logged unexpected output about failed event streams. (33401512)

### Devices

#### Resolved Issues

*   Fixed an issue that caused Xcode to spontaneously lose device configuration information for an Apple Watch. This data loss caused Xcode to either crash or display an error stating that your app “cannot be installed on (null)”. (54768855)

*   Fixed an issue where Xcode could fail to prepare a wirelessly connected iOS device for debugging with the error “Failed _shouldMakeReadyForDevelopment check”. (61227501) (FB7649607)

*   Fixed an issue that could cause Xcode to get interrupted when copying symbols from iOS devices, and never finish preparing iOS devices for debugging. The failure mainly occurred on Xcode installations used to debug multiple iOS devices which are running the same version of iOS. This bug impacted the performance of launching executables on iOS devices and attaching the debugger to them. (68221778) (FB8611135)

### Documentation Viewer

#### Resolved Issues

*   Fixed a crash that could happen when opening the Documentation Window if you installed Xcode outside of `/Applications`. (70631583)

### Interface Builder

#### Resolved Issues

*   Fixed iOS storyboard rendering issues when using [`UISplitViewController`](https://developer.apple.com/documentation/uikit/uisplitviewcontroller) simulated metric sizes with [`UITabBarController`](https://developer.apple.com/documentation/uikit/uitabbarcontroller). (69054879) (FB8704013)

*   Fixed an issue that caused Xcode to warn about multiple deprecated system color references in saved documents. (69667149) (FB8749086)

*   Fixed an issue where the background color of a [`UITextField`](https://developer.apple.com/documentation/uikit/uitextfield) could appear transparent in your app instead of the default color. (70559650)

### Simulator

#### New Features

*   `simctl` now prints “Recording started” to `stderr` when it has enqueued the first frame of a video recording. Scripts or other automation can wait for that message before proceeding, to ensure the first part of the operation is captured in the resulting video. (57915463)

#### Resolved Issues

*   `simctl` video recordings no longer cut off the end of the video when no screen updates are happening. The recording timeline now holds the last frame and extends until you terminate the recording with Control-C (SIGINT). (67952344) (FB8565355)

*   CoreSimulator now excludes its caches directory from Time Machine backups by default. (68782191)

### Swift

#### Resolved Issues

*   Fixed a failure that could occur when compiling a project with Mac Catalyst that imports [OSLog](https://developer.apple.com/documentation/oslog) from Swift. (68597591)
