# Xcode 12.2 Beta 2 Release Notes

Update your apps to use new features, and test your apps against API changes.

## Overview

Xcode 12.2 beta 2 includes SDKs for iOS 14.2, iPadOS 14.2, tvOS 14.2, watchOS 7.1, and macOS Big Sur 11. The Xcode 12.2 beta 2 release supports on-device debugging for iOS 9 and later, tvOS 9 and later, and watchOS 2 and later. Xcode 12.2 beta 2 requires a Mac with Apple silicon running macOS Big Sur 11 or later, or an Intel-based Mac running macOS Catalina 10.15.4 or later.

### General

#### Known Issues

*   Building or running an iOS app with a macOS destination may fail if you’re building the app with a newer iOS SDK than your version of macOS supports. (68261281, 68714781, 68948002)

    The failure may present in one of the following ways:

    *   The application crashes on launch

    *   Xcode displays an alert stating “The operation couldn’t be completed. (OSStatus error -10825.)”

    *   Xcode displays an alert stating “Unable To Install”

    **Workaround**: Change the iOS deployment target for the iOS app to a version supported by the version of macOS that you are using, or upgrade to a version of macOS that supports the iOS deployment target configured in the project. macOS 11.0 beta supports the iOS 14.0 deployment target, and macOS 10.15.6 supports the iOS 13.6 deployment target when running apps built using Mac Catalyst.

*   You can again upload an app for App Store submission or Developer ID notarization using an Xcode located at a path that contains a space. (69009477)

### Apple Clang Compiler

#### Resolved Issues

*   Fixed an issue that caused `strip`, `install_name_tool` and `vtool` to corrupt the ad-hoc code signatures generated by the linker for arm64 Mach-O files. (51911417)

### Devices

#### Resolved Issues

*   Fixed a hang in `rvictl` when running on macOS 11. (65205535)

### Playgrounds

#### Known Issues

*   Playgrounds may crash when presenting a live view on a Mac with Apple silicon. (68930351)

### Previews

#### New Features

*   Xcode provides previews for macOS Widget extensions. (57990060)

#### Known Issues

*   Using the device name “Mac Catalyst” in a [`PreviewDevice`](https://developer.apple.com/documentation/swiftui/previewdevice) modifier may cause the preview to fail. (65305155)

    **Workaround**: Remove the `previewDevice` modifier and switch to the “My Mac” run destination.

### Project Navigator

#### Resolved Issues

*   Fixed an issue where the Finish button was not enabled when adding Swift Packages to a project. (68731814)

### Signing and Distribution

#### Known Issues

*   Xcode can’t distribute an archive containing an App Clip if the parent app’s application identifier doesn’t begin with a Team ID. (67401115) (FB8461092)

### Simulator

#### Resolved Issues

*   SwiftUI projects using StoreKit can now build for simulated watchOS devices. (68931021, 68935233)

#### Known Issues

*   Simulators for iOS 13, tvOS 13, and watchOS 6 or earlier don’t run on the Developer Transition Kit, even though Xcode Preferences allows you to download these older runtimes. Future Macs with Apple silicon will support some older iOS and tvOS Simulators. (66115743) (FB8157217)

*   Shortcuts may not run in simulated devices. (69516795)

#### Deprecations

*   Simulators for watchOS 6 or earlier require 32-bit processes that aren’t supported on Macs with Apple silicon. (66352760)

### Source Editor

#### Resolved Issues

*   The source editor properly displays errors and warnings from Run Script build phases that use relative paths; clicking the issue in the Issues navigator takes you to the issue in the source editor. (43290386) (FB5420750)

### Swift

#### Resolved Issues

*   Fixed a compiler crash that could occur when a function builder body contains an empty switch statement. This issue could also cause a SourceKit crash while typing a switch statement in a SwiftUI view body. (65983237) (FB8111944)

### Swift Packages

#### Known Issues

*   Swift Packages may not respect the “Build Active Architecture Only” project build setting when you try to build universal binaries. (64344067)

    **Workaround**: Use the “Any Mac”, “Any iOS Device (arm64)”, “Any watchOS Device”, or “Any tvOS Device” destination to build for all applicable devices.

### Testing

#### Known Issues

*   Xcode can’t run UI tests for an iOS app on Apple silicon. If the active scheme or test plan includes both unit and UI tests, Xcode skips the UI tests, and logs a message that the UI tests were skipped in the test-activity log. (60059698)

*   Xcode doesn’t run iOS app tests in parallel on Apple silicon. The tests run sequentially instead. (60514529)

*   iOS unit tests fail to launch on Apple silicon if the test target’s host application is set to None. (65309328)

    **Workaround**: Set the host application to an iOS application target.

### Updates in Xcode 12.2 beta

### General

#### New Features

*   When bringing iPad apps to macOS, you can now enable the “Optimize Interface for Mac” target setting to use native Mac controls and resolution. (56344940)

*   Xcode’s run destination menu now shows an Any Mac destination for Mac schemes. This is a new build destination that builds each target in the scheme for all of their supported architectures, regardless of the native architecture of the local Mac. (62736613)

*   Xcode now supports iOS, tvOS, and watchOS development on Macs with Apple silicon. (64317985, 65077539, 65701094)

### Build System

#### Resolved Issues

*   `xcodebuild` no longer incorrectly double-escapes the output of `xcodebuild -showBuildSettings -json`. (63554669)

### Core ML

#### Resolved Issues

*   The Core ML editor’s Preview tab for sound classifier models now shows a classification result when you click on Listen. Also, when you add an audio file, clicking the Play button updates the timeline as the file plays. (67515312)

### Create ML

#### New Features

*   Training Control helps you explore and interact with models during training. The training process can be paused, saved, resumed, and extended. This feature requires macOS 11 or later. (45241965)

*   The new Style Transfer template lets you train deep neural networks to stylize photos and videos in real time. This template requires macOS 11 or later. (55848835)

*   The new Action Classification template lets you train neural networks to classify a single person’s actions in a video clip. This template requires macOS 11 or later. (56622350)

*   The Object Detection template’s new Transfer Learning option helps improve model accuracy when training data is limited. This feature requires macOS 11 or later. (58627183)

*   The Word Tagger template’s new Transfer Learning option uses dynamic word embeddings to help improve model accuracy when training data is limited. This feature requires macOS 11 or later. (59281335)

### Devices

#### Resolved Issues

*   You can debug a WatchKit App when an App Clip is added to its paired iOS App, even if that iOS App isn’t installed. (65784374) (FB8065876)

### Interface Builder

#### New Features

*   Added support for Inline and Compact [`UIDatePicker`](https://developer.apple.com/documentation/uikit/uidatepicker) styles. (65085323) (FB7847821)

#### Resolved Issues

*   Fixed the search field clipping on a navigation bar when first dragged from the object library. For existing navigation controllers in storyboards, you can correct clipping by selecting the navigation bar in the controller, and enable Size Inspector > Safe Area Relative Margins. (66566017) (FB8269384)

*   Fixed an issue that could cause an [`NSTableView`](https://developer.apple.com/documentation/appkit/nstableview) to lose its Source List style when deploying to macOS versions earlier than macOS 11. (67700315) (FB8525478)

### Organizer

#### Resolved Issues

*   Thinning for “all compatible device variants” no longer causes export of a watchOS application for Ad Hoc or Development distribution to fail. (66637482)

### Previews

#### New Features

*   The action menu has a new “Embed…” menu item that lets you specify the type of View container in which to embed the selected view hierarchy. (51152198)

*   The action menu has a new “Embed in ZStack” menu item. (56989502)

*   The previews canvas now automatically shows and hides based on the presence of a [`PreviewProvider`](https://developer.apple.com/documentation/swiftui/previewprovider) in the file being edited. (67083504, 67693254)

*   The Editor menu now includes Create Preview to create a [`PreviewProvider`](https://developer.apple.com/documentation/swiftui/previewprovider), and Create Library Item to create a [`LibraryContentProvider`](https://developer.apple.com/documentation/developertoolssupport/librarycontentprovider). (67110969)

#### Resolved Issues

*   Fixed an issue that prevented previews from loading in projects with non-ASCII characters in their names, or in symbols within the project. (57260388) (FB7451792)

*   Previews correctly display interpolated strings, including for localized strings. (64278576)

*   Fixed an issue that prevented previews from loading for code that contains multi-line string literals. (65735599)

*   On Intel-based Macs, previews now load for iOS, watchOS, or tvOS projects that depend on libraries without an arm64 slice. (65890022)

*   The canvas displays error details when a preview fails to launch due to the underlying app crashing, such as when the app doesn’t have an [`EnvironmentObject`](https://developer.apple.com/documentation/swiftui/environmentobject). (67955924)

#### Known Issues

*   Previews for macOS projects may not load if your Xcode is located outside the /Applications folder. (69442156)

### Signing and Distribution

#### New Features

*   Xcode can now sign iOS apps for development or distribution to Macs with Apple silicon. You must register your Mac with Apple silicon on the [Developer website](https://developer.apple.com) in order to run Mac, iPhone, or iPad apps. Registration requires your Mac’s hardware identifier, which you can find in Xcode’s error message or in the System Information app’s Hardware > Provisioning UDID field. Once you’ve registered your Mac, you can use Xcode’s automatic signing or manually sign apps to run on the device. (54476962, 65752056)

*   Xcode can sign and provision an archived iOS app to run on your Mac with Apple silicon. Find the archive in the Organizer window, click on Distribute App, select either “Ad Hoc” or “Development”, choose your distribution options, select “Automatically manage signing”, and proceed through the remainder of the distribution assistant to create an IPA. Once you’ve created the IPA, you can transfer it to your Mac with Apple silicon, and double-click on it to install. During the app’s first launch, you will be prompted to open the Security & Privacy preferences pane to enable the app. To see the launch button in the preferences pane, make sure your Mac is configured to only allow apps from the App Store and identified developers. (68513041, 68528315).

#### Resolved Issues

*   When distributing an iOS archive using the Ad Hoc or Development method, Xcode validates that Macs with Apple silicon are included in the provisioning profile generated by automatic signing. (66803918)

*   Xcode automatic signing includes your registered Macs with Apple silicon in your provisioning profile when exporting an archive. (66857321)

### Simulator

#### New Features

*   Simulated watchOS 7 devices support 64-bit processes. To verify watchOS projects are 64-bit clean in Simulator, make sure `ARCHS` is set to its default value. (54654060, 66352876)
    > ##### Note
    > Projects must be 64-bit clean to run in Simulator on Macs with Apple silicon, which don’t support 32-bit code.

### StoreKit

#### Resolved Issues

*   Fixed a crash that could occur when selecting “Subscription Options” in the StoreKit transaction manager. (68354368)
