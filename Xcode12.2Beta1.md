# Xcode 12 Release Notes

Update your apps to use new features, and test your apps against API changes.

## Overview

Xcode 12 includes SDKs for iOS 14, iPadOS 14, tvOS 14, watchOS 7, and macOS Catalina 10.15.6. The Xcode 12 release supports on-device debugging for iOS 9 and later, tvOS 9 and later, and watchOS 2 and later. Xcode 12 requires an Intel-based Mac running macOS Catalina 10.15.4 or later.

### General

#### New Features

### Core ML

#### Known Issues

*   The Core ML editor’s Preview tab for sound classifier models doesn’t show a classification result when you click on ‘Listen’. Also, when you add an audio file, clicking the Play button doesn’t update the timeline as the file plays. This issue also occurs in the Create ML app. (67515312)

### Devices

#### Known Issues

*   You can’t debug a WatchKit App when an App Clip is added to its paired iOS App, if that iOS App isn’t installed. (65784374) (FB8065876)

    **Workaround**: Set “Supports Running Without iOS App Installation” in the General settings for the WatchKit App Extension’s build target.

### Organizer

#### Known Issues

*   Exporting a watchOS application for ad-hoc or development distribution may fail when using Xcode 12 and thinning for “all compatible device variants.” (66637482)

    **Workaround**: Don’t thin, or choose a specific target device.

### Signing and Distribution

#### New Features

*   Xcode 12 lets you build your iOS app for running on Macs with Apple silicon. Make sure you’ve registered your Mac with Apple silicon’s hardware identifier (available in the System Information app’s Hardware > Provisioning UDID field) in your account on [https://developer.apple.com/account](https://developer.apple.com/account), find the archive in the Organizer window, click on Distribute App, select either “Ad Hoc” or “Development,” choose your distribution options, select “Automatically manage signing,” and proceed through the remainder of the distribution assistant to create an IPA. Once you’ve created the IPA, you can transfer it to your Mac with Apple silicon, and double-click on it to install. During the app’s first launch, you will be prompted to open the Security & Privacy preferences pane to enable the app. To see the launch button in the preferences pane, make sure your Mac is configured to only allow apps from the App Store and identified developers. (68513041, 68528315).

#### Known Issues

*   Xcode automatic signing may not automatically include Macs with Apple silicon in your provisioning profile when exporting an archive. (66857321)

    **Workaround**: If Xcode produces an IPA that doesn’t install on your registered Macs, remove any Ad Hoc Distribution or Development provisioning profiles from the ~/Library/MobileDevice/Provisioning Profiles directory before exporting your archive.

### Simulator

#### New Features

*   Simulated watchOS 7 devices support 64-bit processes. To verify watchOS projects are 64-bit clean in Simulator, make sure `ARCHS` is set to its default value. (54654060, 66352876)
    > ##### Note
    > Projects must be 64-bit clean to run in Simulator on Macs with Apple silicon, which don’t support 32-bit code.

### StoreKit

#### Known Issues

*   Xcode crashes when selecting “Subscription Options” in the [StoreKit](https://developer.apple.com/documentation/storekit) transaction manager. (68354368)

    **Workaround**: Use the [StoreKit Test](https://developer.apple.com/documentation/storekittest) framework to test downgrading, cross-grading, or upgrading a subscription.

### Swift

#### Known Issues

*   The compiler may crash when a function builder body contains an empty switch statement. This issue can also cause a SourceKit crash while typing a switch statement in a SwiftUI view body. (65983237) (FB8111944)
