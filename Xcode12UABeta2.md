# Xcode 12 for macOS Universal Apps Beta 2 Release Notes
Update your apps for Apple silicon, and test your apps against API changes.

## Overview

Xcode 12 for macOS Universal Apps beta 2 is a distribution of Xcode 12 beta 2 for creating Universal Mac apps that run on both Apple silicon and Intel-based Mac computers. Choose the “Any Mac” destination in the toolbar to build your Mac app as Universal, and to see any build errors your project may encounter. This is the same toolset included with the Universal Apps Quick Start Program and can be run on either an Intel-based Mac, or on the Developer Transition Kit.

Xcode 12 for macOS Universal Apps beta 2 includes SDKs for iOS 14, iPadOS 14, and macOS 11. The Xcode 12 for macOS Universal Apps beta 2 release supports on-device debugging for iOS 9 and later. Xcode 12 for macOS Universal Apps beta 2 requires a Mac running macOS 10.15.4 or later.

These notes are about the differences between Xcode 12 for macOS Universal Apps beta 2 and Xcode 12 beta 2. The primary Xcode 12 beta 2 product is recommended for development of apps not intended to run on macOS, and includes all platform SDKs. For additional information about Xcode 12 beta 2, see [Xcode 12 Beta 2 Release Notes](https://developer.apple.com/documentation/xcode-release-notes/xcode-12-beta-release-notes).

### General

#### Resolved in Xcode 12 for macOS Universal Apps Beta 2

*   Metal code compiles when using deployment target 11.0. (64344660)

#### Known Issues

*   SwiftUI code that uses SpriteKit may not compile. (63350569)

*   Xcode 12 for macOS Universal Apps beta 2 doesn’t support building for tvOS or watchOS. It only supports building for iOS or iPadOS on Intel-based Macs. (63733399)

*   Simulated iOS devices are not available when running Xcode 12 for macOS Universal Apps beta 2 on an Apple silicon Mac. (63749966)

*   Debugging a Rosetta process using LLDB from the command line can take a long time to launch. (63793175)

    **Workaround**: Open Xcode to prepare the cache used for debugging Rosetta processes.

*   Storyboards and XIBs may have rendering issues when working with large images. (64093939)

*   When you view the signing settings of an app that builds with Mac Catalyst, and you have a Mac run destination selected, then Xcode may display an error that indicates your Mac isn’t included in your iOS provisioning profile. This is a cosmetic issue and doesn’t affect building, running, or distributing your app. (64147483)

*   Xcode may crash when opening a debug gauge. (64181692)

*   iOS, iPadOS, and tvOS Playgrounds don’t work. (64264601)

    **Workaround**: Use the primary Xcode 12 beta to run these playgrounds.

*   Some macOS target templates include an older default Deployment Target. (64312117)

*   To build the Release configuration or run the Profile action on a simulated iOS device, set the Build Active Architecture Only build setting to Yes for both the Debug and Release configurations. (64317985)

*   Xcode may crash when continuing stepping out of a breakpoint. (64333652)

*   Swift Packages may not respect the “Build Active Architecture Only” project build setting when you try to build universal binaries. (64344067)

    **Workaround**: Use the “Any Mac” destination to build the project for both Apple silicon and Intel-based Mac computers.

*   SwiftUI code that uses SceneKit may not compile. (64344265)

*   A Mac Catalyst app signed to run locally on macOS may fail to run with the Mac (Rosetta) run destination. (64421496)

*   macOS 11 beta for Intel can’t run an executable built from a target created on a Mac Developer Transition Kit. (64792610)

    **Workaround**: Change the new target’s deployment target to macOS 10.16 or earlier.

*   Projects fail to build for simulated devices. (65077539)

    **Workaround**: Specify `x86_64` as the build architecture.

## Updates in Xcode 12 for macOS Universal Apps beta

### General

#### New Features in Xcode 12 for macOS Universal Apps beta

*   Xcode’s run destination menu now shows an Any Mac destination for Mac schemes. This is a new build destination that builds each target in the scheme for all of their supported architectures, regardless of the native architecture of the local Mac. (62736613)
