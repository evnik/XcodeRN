# Xcode 12 Beta 4 Release Notes
Update your apps to use new features, and test your apps against API changes.

## Overview

Xcode 12 beta 4 includes SDKs for iOS 14, iPadOS 14, tvOS 14, watchOS 7, and macOS 11. The Xcode 12 beta 4 release supports on-device debugging for iOS 9 and later, tvOS 9 and later, and watchOS 2 and later. Xcode 12 beta 4 requires Apple silicon running macOS Big Sur 11 beta or later, or an Intel-based Mac running macOS Catalina 10.15.4 or later.

### Apple Clang Compiler

#### Deprecations

*   The stand-alone system assemblers for i386, x86_64, and arm are deprecated and may be removed in a future Xcode release. Using the `as` command with the `-Q` flag shows a warning that instructs you to transition to Clang’s integrated assembler and the `-q` flag. The `as(1)` driver will remain, as a standard way to invoke Clang’s integrated assembler, as well as any assemblers installed by the developer. (61299833)

### Build System

#### Deprecations

*   The Build Settings editor no longer includes the Valid Architectures build setting (`VALID_ARCHS`), and its use is discouraged. Instead, there is a new Excluded Architectures build setting (`EXCLUDED_ARCHS`). If a project includes `VALID_ARCHS`, the setting is displayed in the User-Defined section of the Build Settings editor. (15145028)

*   The legacy build system is deprecated, and will be removed in a future release. (62742902)

### Core ML

#### Deprecations

*   The default initializer on an auto-generated model interface in Xcode is deprecated in favor of `init(configuration:)`. Use `init(configuration:)` or the newly introduced `.load()` method instead, and handle model load errors appropriately. (62875309)

### Debugging

#### Known Issues

*   iPad and iPhone Apps on Mac may not have access to On-Demand Resources when built and run from Xcode. (62074124)

*   The Memory Graph Debugger may incorrectly classify the origin of types defined in SwiftUI apps in the current Xcode workspace. The Debug navigator may list these types in the wrong sections, and incorrectly filter them out when you select “Show only content from workspace”. (63899779)

    **Workaround**: Deselect “Show only content from workspace” to discover objects of all types.

*   On Apple silicon, debugging a tvOS app on a simulated device fails with an error “Could not attach to pid”. (65375566)

    **Workaround**: Run the app on an Apple TV, or in a simulated tvOS device on an Intel Mac. Alternatively, edit the Run scheme and deselect “Debug executable”.

*   Debugging, testing, and profiling on devices running iOS 14, iPadOS 14, watchOS 7, or tvOS 14 beta 4 and later requires Xcode 12 beta 3 or later. Older versions of Xcode may display an error of “Failed to start remote service” when attempting to develop on unsupported operating system versions. (60850305)

*   Xcode may crash when opening a debug gauge. (64181692)

### Instruments

#### Known Issues

*   The Animation Hitches template doesn’t show hitch intervals when instrumenting macOS apps. (61082729)

*   iOS 14, iPadOS 14, tvOS 14, and watchOS 7 simulated devices have reduced performance and higher memory consumption compared to simulated devices running earlier OS versions. (65037128)

#### Deprecations

*   The `instruments` command is now deprecated in favor of its replacement: `xctrace`. `xctrace` records, imports, and exports data from Instruments `.trace` files. (36641078)

### Interface Builder

#### Known Issues

*   Interface Builder doesn’t allow creating a classic style [`UISplitViewController`](https://developer.apple.com/documentation/uikit/uisplitviewcontroller). (65966010) (FB8107534)

#### Deprecations

*   Interface Builder no longer provides access to the Can Draw Concurrently property. You may still configure this behavior in code with [`canDrawConcurrently`](https://developer.apple.com/documentation/appkit/nsview/1483425-candrawconcurrently). (42437767)

*   QTCaptureView and QTMovieView are deprecated and no longer supported. Remove these views from storyboards and `.xib` files. (64263402)

### Playgrounds

#### Known Issues

*   Xcode may show the text “No Editor” instead of opening the source editor of a Playground immediately after creating it. (56484197)

    **Workaround**: Use View > Navigators > Project to reveal the Project Navigator, then select the Playground manually.

### Previews

#### Known Issues

*   Live SwiftUI previews for macOS aren’t interactive when the containing [`PreviewProvider`](https://developer.apple.com/documentation/swiftui/previewprovider) has more than one preview. (62156572)

*   SwiftUI previews may fail when a file is part of a framework that is linked by both an app and a widget. (63785700)

*   Live previews for Mac Catalyst may fail when run on macOS 11. (63998976)

*   Live SwiftUI previews for Mac Catalyst exit when brought forward or made visible. (64151326)

*   Xcode doesn’t provide previews for macOS widget extensions. (57990060)

*   You can’t select views in Widgets in the Previews canvas. (62517078)

*   Animations may not work in live SwiftUI previews. (63333795)

*   Live SwiftUI previews for macOS may not appear when making changes until you click the Bring Forward button on the canvas. (63865018)

*   Previewing a widget extension for iPad devices may show an excess blank bar at the top. (64277772)

*   A widget extension preview doesn’t adapt to the dark appearance when you apply a `.preferredColorScheme(.dark)` appearance modifier. (64277915)

### Project Navigator

#### Known Issues

*   The Find panel may stop responding to mouse events after you resize the window. (66256586)

    **Workaround**: Switch to a different document and then back to the one you’d like to edit.

*   App Clip schemes offer “My Mac (Designed for iPad)” or “My Mac (Designed for iPhone)” run destinations, even though App Clips aren’t supported on macOS. (65702469)

### Reality Composer

#### Deprecations

*   Reality files created by Xcode 12 can only be loaded in macOS 10.15.4 or later, iOS and iPadOS 13.4 or later, and Reality Composer 1.4 or later. (58825031)

### Signing and Distribution

#### Known Issues

*   A Mac Catalyst app signed to run locally on macOS may fail to run with the Mac (Rosetta) run destination. (64421496)

*   App Clips can no longer access Wallet passes with the Pass Type IDs Entitlement. However, App Clips can determine whether a specific pass is already present in Wallet and prompt the user to add a pass if necessary. If you’ve already added the Wallet capability to an App Clip target, you may not be able to build or submit your app to App Store Connect. Remove the Wallet capability in the target editor’s Signing & Capabilities pane and disable or delete any code that makes use of this removed feature. (65244156)

### Simulator

#### Known Issues

*   When simulating a push notification in Simulator with the `content-available` key set, the system calls [`application(_:performFetchWithCompletionHandler:)`](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1623125-application) instead of [`application(_:didReceiveRemoteNotification:fetchCompletionHandler:)`](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1623013-application). (60426170, 60974170) (FB7625283)

*   Simulators for iOS 13, tvOS 13, and watchOS 6 or earlier don’t run on the Developer Transition Kit, even though Xcode Preferences allows you to download these older runtimes. Future Macs with Apple silicon will support some older iOS and tvOS Simulators. (66115743)

#### Deprecations

*   When running in macOS 11, Simulator supports iOS 11.4 or later. (59938106)

*   Simulators for watchOS 6 or earlier require 32-bit processes that are not supported on Macs with Apple silicon. (66352760)

### Source Editor

#### Known Issues

*   An Xcode extension may cause Xcode to hang on launch, or upon enabling the extension. (61952790)

    **Workaround**: Disable the Xcode extension in the Extensions pane in System Preferences.

*   A new Xcode Source Editor Extension target doesn’t automatically set up embedding `XcodeKit.framework` in the extension. (59274389)

    **Workaround**: Embed `XcodeKit.framework` in the extension manually.

#### Deprecations

*   For compatibility with new security features in macOS 11, Xcode extensions must be built using Xcode 12 and must embed `XcodeKit.framework`. An Xcode extension rebuilt with these tools remains compatible with older versions of Xcode and macOS. (51822755)

### Swift

#### Known Issues

*   Widgets may crash when built for release. (65862827)

    **Workaround**: Set `DEAD_CODE_STRIPPING` to `NO` in the extension target’s build settings. When you upload the application to App Store Connect, also unset “Include bitcode for iOS content” in the App Store Connect distribution options.

### Swift Packages

#### Known Issues

*   A package resolution error with the message “database is locked” may occur when opening a workspace that contains package references. (61113361)

    **Workaround**: Close and reopen the workspace.

*   Swift Packages may not respect the “Build Active Architecture Only” project build setting. (64344067)

    **Workaround**: Use the “Any Mac”, “Any iOS Device (arm64)”, “Any watchOS Device”, or “Any tvOS Device” destination to build for all applicable devices.

### Testing

#### Known Issues

*   Screenshot capture may cause a “Lost connection to `testmanagerd`” test failure when running UI tests on certain iOS devices. (63946264)

    **Workaround**: Disable automatic screenshots in your scheme or test plan.

*   Building Mac Catalyst apps for Macs with Apple silicon fails when Code Coverage is enabled. (65003639)

*   [`XCTAssert`](https://developer.apple.com/documentation/xctest/xctassert) and related assertion macros in Objective-C and Objective-C++ no longer include a reference to `self` to access the current test case. The compiler may now emit new warnings when building code with `-Wunused-variable` or `-Wunused-lambda-capture`, which declares an explicit variable or lambda capture for `self`. (60017011)

    **Workaround**: Remove the `self` variable or lambda capture because it’s no longer required by [`XCTAssert`](https://developer.apple.com/documentation/xctest/xctassert).

*   Xcode can’t run UI tests for an iOS or iPadOS application on Apple silicon. If the active scheme/test plan includes both unit and UI tests, Xcode skips the UI tests, and logs a message that the UI tests were skipped in the test activity log. (60059698)

*   Xcode doesn’t support running tests in parallel for an iOS or iPadOS application on Apple silicon. The tests run sequentially instead. (60514529)

*   Animation performance metrics (total number of hitches, hitches total duration, hitch time ratio, frame rate, and frame count) when using an animation `os_signpost` coupled with the [`XCTOSSignpostMetric`](https://developer.apple.com/documentation/xctest/xctossignpostmetric) are unavailable for simulated devices. (63766090)

    **Workaround**: Use [`XCTSkip`](https://developer.apple.com/documentation/xctest/xctskip) to skip over performance tests on simulated devices.

*   iOS unit tests fail to launch on Apple silicon if the test target’s Host Application setting is set to None. (65309328)

    **Workaround**: Set the host application to an iOS application target.

#### Deprecations

*   Xcode now supports debugging apps and running tests on iOS devices running iOS 9.0 and above. (59561001)

## Updates in Xcode 12 Beta 4

### Asset Catalogs

#### Resolved

*   When you select Optimize Interface for Mac for apps built with Mac Catalyst and there is no Mac asset, Xcode now uses the Universal asset only if you don’t provide a Mac Scaled or iPad asset. (63368950)

### Interface Builder

#### New Features

*   In AppKit apps, you can now edit the Render Mode and Symbol Scale of SF Symbols for storyboard and `.xib` files. When you select an SF Symbol in the image picker, two additional properties expand below the image name. To display SF Symbols that support full color, set the Render Mode to Original. (61844681)

*   Added support for new UISwitch properties, [`preferredStyle`](https://developer.apple.com/documentation/uikit/uiswitch/3621874-preferredstyle) and [`title`](https://developer.apple.com/documentation/uikit/uiswitch/3621876-title). (62320185)

### Previews

#### Resolved

*   Previews now work correctly when you select the universal “Any Mac” run destination. (64513915)

*   Fixed an issue where previews fail in packages with non-root source files. (64628934) (FB7751511)

### Reality Composer

#### Resolved

*   Fixed a crash that could occur in Reality Composer when adding a CSV file to a chart asset. (63782093)

### Simulator

#### New Features

*   Simulator now supports 64-bit processes on watchOS 7. Make sure your project uses `$(STANDARD_ARCHS)` to build for x86_64 on Intel Macs, and for arm64 on Macs with Apple silicon. This configuration allows you to check your code is 64-bit clean, and makes it possible to simulate a watchOS device on Apple silicon, which doesn’t support 32-bit processes. (66352876)

#### Resolved

*   `simctl` status bar overrides now work on simulated devices running iOS or iPadOS 13.6 or earlier. (63958080)

### Source Control

#### Known Issues

*   If you create a Git repository before setting Git’s author information, Xcode won’t be able to rename files, and every file in the repository will be untracked. (64260085)

    **Workaround**: Set up Git author information via Xcode Preferences or the command-line `git` before creating a new project. Alternatively, create an initial commit after you set up Git author information.

### Testing

#### Resolved

*   `xcodebuild` now respects the `-parallel-testing-worker-count` option when running tests in parallel. (64495567)

## Updates in Xcode 12 Beta 3

### General

#### Resolved

*   Fixed an issue that prevented compilation of SwiftUI code that uses SpriteKit. (63350569)

*   Compilable code completions for SwiftUI APIs now correctly handle overloaded methods. (64037686)

*   Fixed a crash that sometimes occurred when adding an Apple ID account to Xcode’s Accounts preferences pane. (64806671) (FB7798083)

*   Xcode 12 beta 3 supports iOS, tvOS, and watchOS device and simulated device development on Apple silicon. (64317985, 65077539, 65701094)

### Build System

#### New Features

*   XCFrameworks can now include `.dSYM` and `.bcsymbolmap` debugging symbol files in your library bundle with the `-debug-symbols` flag. Run the command `xcodebuild -create-xcframework -help` for additional usage information. (64910707)

#### Resolved

*   Fixed an issue where Xcode didn’t properly copy headers while processing an XCFramework. (64754387) (FB7786076)

### Debugging

#### Resolved

*   Fixed a crash that could occur when you selected the memory browser in the Debug Navigator. (54767689)

*   When debugging with `lldb`, `po self` now displays the address of a pointer in Swift code on a simulated tvOS device. (58477904, 65150335)

*   Debugging a Rosetta process using `lldb` from the command line launches more quickly. (63793175)

*   Fixed a crash that could occur when selecting the FPS Debug Gauge while debugging a game project on macOS. (64213691)

*   Fixed a crash that could occur after capturing a view hierarchy. (64334442)

*   Debugging iOS WidgetKit extensions run on macOS 11 fails with an error. (65698467)

### Documentation Viewer

#### Resolved

*   SwiftUI, DeveloperToolsSupport, WidgetKit, SwiftSystem, and Combine now include beta indicators in Xcode’s documentation viewer. (64380885)

*   SwiftUI, DeveloperToolsSupport, WidgetKit, SwiftSystem, and Combine now have correct Mac Catalyst availability in Xcode’s documentation viewer. (64386417, 64526330)

### Interface Builder

#### New Features

*   Interface Builder now supports the two-column and three-column styles for [`UISplitViewController`](https://developer.apple.com/documentation/uikit/uisplitviewcontroller) introduced in iOS 14. (57025285)

*   You can now show and hide the Minimap with the Minimap command in the Editor menu. (63831585)

#### Resolved

*   Fixed an issue that would sometimes omit iOS text styles from the inspectors. (51854358) (FB6169763)

*   Fixed performance issues with [`NSTabView`](https://developer.apple.com/documentation/appkit/nstabview) and hidden views in a storyboard or `.xib` canvas. (63008369, 64314634)

*   Fixed rendering issues when with large images and [`SCNView`](https://developer.apple.com/documentation/scenekit/scnview) for storyboards and `.xib` canvases on Apple silicon. (64093939)

*   Fixed content rendering issues for some destination view controllers from a show or push segue in the Mac Catalyst view of a storyboard. (64320758)

### Previews

#### Resolved

*   On-device SwiftUI previews for watchOS complications are now supported. (64097600)

*   Resolved a timeout that could occur in SwiftUI previews for Mac Catalyst. (64098969)

*   Fixed a bug that could result in blank previews for widgets that pass `nil` to the [`widgetURL(_:)`](https://developer.apple.com/documentation/swiftui/view/widgeturl(_:)) modifier. (64315456)

*   Xcode now supports SwiftUI Previews for iOS when running on Apple silicon. (65101322)

### Project Navigator

#### Resolved

*   Fixed an issue where the Show in Finder contextual menu item was disabled for some items in the Project Navigator. (63934092)

*   Fixed a crash that could occur when renaming the root project node in the Project navigator. (63998499)

*   Selecting items in the navigation sidebar no longer shows a black highlight rather than the macOS accent color. (64139237)

*   Fixed a crash that could occur while validating menu items. (64409911

*   Fixed an issue where double-clicking a group in the Project Navigator didn’t expand or collapse the group. (64622953) (FB7749742)

*   Fixed an issue where using a keyboard shortcut to show a navigator didn’t focus the navigator outline. (64627462) (FB7751100)

*   Fixed an issue where the Filter in Navigator menu item didn’t function. (64647545) (FB7758103)

*   Fixed a crash which could occur when performing the Reveal in Project Navigator command. (65235467)

*   Fixed an issue where Xcode didn’t allow you to drag a storyboard to a new location in its parent group. (65241585)

### Reality Composer

#### Resolved

*   Reality Composer 1.4.1 restores compatibility with beta releases of iOS 14 and iPadOS 14. (64509815)

### Sanitizers

#### Resolved

*   Xcode now supports Thread Sanitizer when debugging on simulated watchOS devices. (64421085)

### Signing and Distribution

#### New Features

*   Xcode now supports automatic and manual signing for development and distribution of iPhone and iPad apps on Macs with Apple silicon. You must register your Mac with Apple silicon on the [Developer website](https://developer.apple.com) in order to run Mac, Mac Catalyst, iPhone, or iPad apps. Registration requires your Mac’s hardware identifier, which you can find in Xcode’s error message or in the System Information app’s Hardware > Provisioning UDID field. (54476962, 65752056)

#### Resolved

*   Automatic signing can now enable the Sign in with Apple capability for App Clip targets. (64452719)

*   App Clips can now use the [Network Extension](https://developer.apple.com/documentation/networkextension) framework and [`Hotspot Configuration Entitlement`](https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_developer_networking_hotspotconfiguration) to configure Wi-Fi networks. (64966949)

### Simulator

#### Resolved

*   Improved app launch times in simulated devices under heavy load. (63348920)

*   When Simulator is open in a full-screen split with Xcode and you start another simulated device, the new device window no longer attempts to start in full-screen. (64005856)

*   Fixed a bug where Launching apps in Simulator while Simulator is already running sometimes failed with an error of “Timed out waiting for Simulator.app to become ready”. (64508635)

*   Simulator no longer triggers the hot corner action if you start pointer capture mode with an upper-left hot corner enabled. (64805156) (FB7797684)

### Swift

#### Resolved

*   Reduced the compiler’s memory use. (59908962)

*   Xcode 12 beta 3 includes support for using `@main` in place of `@UIApplicationMain` or `@NSApplicationMain` in UIKit- or AppKit-based apps. (60502727, 60502804, 63291088)

*   Swift infers attributes for Swift function builders from protocol requirements. (63629316)

*   Adding a member to a type that is used in both the file that defines it and another file no longer causes a miscompilation in incremental compiles. (64074744)

### Testing

#### Resolved

*   UI target queries can now better target cells in the iOS Share Sheet. (49961747)

*   iOS app unit tests for Swift code execute more reliably on Apple silicon. (65308436)

## Updates in Xcode 12 Beta 2

### General

#### New Features

*   Code completions have a new, focused user interface, making it easier to find a completion. Completions are also more accurate and up to 15 times faster in Xcode 12. (56087948, 58010475)

#### Resolved

*   Running a developer command-line tool without the command-line tools installed or invoking `xcode-select --install` directly will trigger installation of the command-line tools. (63881429)

### Core ML

#### Resolved

*   Xcode now correctly encrypts a model archive for Core ML model deployment when Encrypt Model is enabled. (64331416)

### Devices

#### Resolved

*   Devices running beta releases of iOS or iPadOS 13.6 can be used for development with Xcode 12 beta 2. (64220694)

### Metal

#### Resolved

*   Metal code compiles when using deployment target 11.0. (64344660)

### Organizer

#### Resolved

*   The Organizer window no longer clips text in the sidebar. (64281631)

### Previews

#### Resolved

*   Packages that contain previews can now update without fully rebuilding the active scheme. (51030302)

### Project Navigator

#### Resolved

*   Selecting a file in the Project navigator using VoiceOver now opens the selected file in the editor. (64461629)

*   Deleting a Core Data model from the Project navigator no longer causes Xcode to crash. (64606064)

## Updates in Xcode 12 Beta

### General

#### New Features

*   Documents can now be opened in their own tab, making it easy to quickly switch between files while maintaining the rest of Xcode’s configuration. Option-click or double-click to open a document in a tab. The tab bar appears when you have more than one document open, or you choose View > Always Show Tab Bar. (7954451)

*   Xcode now supports previewing widgets, App Clips, and content in Swift packages. For more seamless live previewing on device, Xcode installs the new Xcode Previews app for iOS 14 and iPadOS 14. (56388008)

*   The new [`LibraryContentProvider`](https://developer.apple.com/documentation/developertoolssupport/librarycontentprovider) protocol gives you the ability to show your views and modifiers in Xcode’s library. (56423420)

*   When bringing iPad apps to macOS, you can now use the Optimize Interface for Mac target setting to use native macOS controls and Mac resolution. (56344940)

*   Xcode’s run destination menu now shows an Any Mac destination for Mac schemes. This is a new build destination that builds each target in the scheme for all of their supported architectures, regardless of the native architecture of the local Mac. (62736613)

### Apple Clang Compiler

#### New Features

*   Clang now warns about incorrect format strings that are specified in an [`NSLocalizedString`](https://developer.apple.com/documentation/foundation/nslocalizedstring) macro. (23622446) (FB5412403)

*   The `std::is_scalar` trait is now true for Block types. This allows using blocks in new places like `std::optional`. (57892832)

#### Resolved

*   `@dynamic` on a property is ignored if the property is redeclared in a protocol that inherits from another protocol. (45503561)

*   Clang now reports an error when you use a function without an explicit declaration when building C or Objective-C code for macOS (`-Werror=implicit-function-declaration` flag is on). This additional error detection unifies Clang’s behavior for iOS/tvOS and macOS 64-bit targets for this diagnostic. (49917738)

*   Fixed type checking for block parameters using `id` with protocols. The compiler now emits an error for method calls with a block that uses parameters more specific than arguments with which it will be called. (57980961)

### Asset Catalogs

#### New Features

*   Added support for Scalable Vector Graphic (SVG) image assets. These preserve their vector representation with deployment targets of macOS 10.15 or later, iOS 13 or later, and iPadOS 13 or later. (18389814)

*   The required pixel size is now shown for complication placeholder images. (21135944)

*   Adding a new color now includes a Dark Appearance variant by default. If you leave this empty, Xcode will use the Any Appearance color value for both Light Appearance and Dark Appearance. You can use the asset’s Attribute inspector to hide the unused variant. (55720623)

*   The “Mac Catalyst” asset variant has been renamed to “Mac Scaled”. Xcode will use this asset in targets that build with Mac Catalyst when “Scale Interface to Match iPad” is selected (including on macOS 10.15). When “Optimize Interface for Mac” is selected, Xcode will prefer the Mac asset variant. (58883008)

*   The “New Asset” menu has been changed to organize asset types by platform. (59233882)

#### Resolved

*   Resolved an issue where hidden folders inside an Asset Catalog could cause Xcode to repeatedly reload the catalog. (35275782) (FB5390092)

*   Asset Catalog `Contents.json` files will be normalized upon editing for better stability and compatibility with future edits. Keys are written in alphabetical order, and a newline character is present at the end of the file. (53886564)

### Build System

#### New Features

*   CoreData code generation can now be invoked on the command line using the `momc` tool. (58713955)

#### Resolved

*   Fixed a bug where a regenerated dSYM file isn’t copied with the product in an incremental build if `DWARF_DSYM_FILE_SHOULD_ACCOMPANY_PRODUCT` is enabled. (44696736)

*   Restored support for `PRODUCT_DEFINITION_PLIST` in the new build system. (45800765) (FB5711777)

*   Fixed a race condition where multiple targets using the same XCFramework could result in non-deterministic build failures. (53911952) (FB6878988)

*   When using `USE_RECURSIVE_SCRIPT_INPUTS_IN_SCRIPT_PHASES` with `XCFileLists`, the items within are now properly treated as recursive inputs. (54635196) (FB7109342)

*   Fixed a bug that could cause tagged On-Demand Resources to be included in both an asset pack and the product. These resources are now only included in the asset pack. (59008757)

*   Input files for Run Script Phases are now tracked as inputs to code-signing tasks, allowing modifications to those files to properly trigger code signing on incremental builds. (59353913)

*   Fixed an issue that caused [`LSMinimumSystemVersion`](https://developer.apple.com/documentation/bundleresources/information_property_list/lsminimumsystemversion) in a macOS application’s `Info.plist` and [`MinimumOSVersion`](https://developer.apple.com/documentation/bundleresources/information_property_list/minimumosversion) on other platforms to be set to an earlier value than the deployment target of the build target. (62617478) (FB7681463)

### Create ML

#### New Features

*   Training Control helps you explore and interact with models during training. The training process can be paused, saved, resumed, and extended. This feature requires macOS 11 or later. (45241965)

*   The new Style Transfer template lets you train deep neural networks to stylize photos and videos in real time. This template requires macOS 11 or later. (55848835)

*   The new Action Classification template lets you train neural networks to classify a single person’s actions in a video clip. This template requires macOS 11 or later. (56622350)

*   The Object Detection template’s new Transfer Learning option helps improve model accuracy when training data is limited. This feature requires macOS 11 or later. (58627183)

*   The Word Tagger template’s new Transfer Learning option uses dynamic word embeddings to help improve model accuracy when training data is limited. This feature requires macOS 11 or later. (59281335)

### Debugging

#### New Features

*   When a process pauses at a breakpoint, Xcode displays the hit count for that particular breakpoint location as part of the breakpoint’s annotation in the editor. An example is “Breakpoint 2.1 (7)”, where 7 means that location 2.1 has been hit 7 times. (3836838)

*   When a process crashes under the debugger, Xcode prints the crash messages in the Console. These messages are similar to the ones displayed in CrashReporter. (8931901)

*   Reorder breakpoint actions by dragging and dropping them into a different position in the Breakpoint Editor. (9777468)

*   The new Enable Breakpoint at Current Line and Disable Breakpoint at Current Line menu item lets you toggle an existing breakpoint in your code. In addition, you can bind a keyboard shortcut to that menu item to toggle the breakpoint quickly. (17924697)

*   You can now name a breakpoint, and reference it by name from another breakpoint’s action. For example, to enable a previously disabled breakpoint called “MyBreakpoint”, type `break enable MyBreakpoint` in an action’s Debugger Command field. (25739693)

*   When paused in the debugger, stepping out of a block will unwind and land in a frame with debug symbol.

    To land in disassembly, hold the control key while clicking on the Step Over or Step Out control. (29482033)

*   Besides showing you the paused line in the editor, Xcode indicates the column where the process is paused. This is helpful in knowing when to step in, analyzing crash reports, and locating yourself in code with multiple closures. (31197308)

*   You can now specify a path for the LLDB init file to use in a Run and Test action. Configure this path in the Info tab of a scheme’s Run or Test action. The path can contain a build settings macro such as `${SRCROOT}`, so the file can be part of a project. (38677796) (FB5425738)

*   Xcode debugger annotations will highlight source code with greater opacity to improve visibility in several Xcode themes. (53463745)

*   The view debugger will identify runtime issues and present optimization opportunities to improve the efficiency and responsiveness of the UI. The suggestions will be presented in the debug navigator when debugging the view hierarchy of the application. (56552710)

*   To debug a Widget Extension, run the extension’s scheme. Setting environment variables in the Arguments pane of the widget extension’s scheme lets you configure options for the debugging session. Widgets support one or more families, or sizes. To select the family to use when debugging, set the `_XCWidgetFamily` environment variable to `small`, `medium`, or `large`. If the extension uses [`WidgetBundle`](https://developer.apple.com/documentation/swiftui/widgetbundle) to support multiple widgets, you can choose which one to debug by setting the `_XCWidgetKind` environment variable to match the `kind` property of the widget’s configuration. On macOS, you can specify the default view shown in the WidgetKit Simulator by setting the `_XCWidgetDefaultView` environment variable to `timeline`, `snapshot`, `placeholder`, or `info` (57059772, 63777618)

*   The view debugger now supports saving and reopening view hierarchy snapshots. After you capture a view hierarchy with the Debug View Hierarchy button in the debug bar, you can choose File > Export View Hierarchy to save it as a `.viewhierarchy` file. You can reopen the saved `.viewhierarchy` in Xcode to inspect the state of the view hierarchy as captured. (57933113)

*   When a [`CALayer`](https://developer.apple.com/documentation/quartzcore/calayer) is selected in the view debugger, the Object inspector now displays explanatory tooltips on Offscreen Flags and Group Flags. (58647887)

*   If you have disabled breakpoints in the Breakpoint Navigator, you can use the contextual menu to delete all the disabled breakpoints. (59164503)

*   Debug App Clips using the scheme created for the App Clip. In the scheme the environment variable `_XCAppClipURL` can be used to set the App Clip experience URL for the debugging session. (59404002)

*   The view debugger now generates runtime issues for performance Optimization Opportunities for [`CALayer`](https://developer.apple.com/documentation/quartzcore/calayer). Choose Editor > Show Layers to view CALayers in the view debugger. Choose Editor > Show Optimization Opportunities to show or hide performance runtime issues. (60103476)

*   Debug > Attach to Process and Debug > Detach are now in the middle of the menu, closer to the rest of the debug menu items. (60390611)

*   View hierarchies captured with Xcode can now be exported to `.viewhierarchy` files. (61065771)

*   The ClockKit framework generates Runtime Issues in Xcode, to help you analyze runtime bugs. (61346475)

#### Resolved

*   Resolved an issue where clicked buttons in the debug bar didn’t suitably change their appearance in Dark Mode. (46294176)

*   Xcode persists the Malloc Stack Logging choice in the Scheme Editor’s Diagnostics tab in a more timely manner. (59154142)

*   Xcode now launches applications with Launch Services to better reflect a real application running environment. (59478437)

*   Resolved an issue which caused the view debugger to show no content when the user selects “Focus on View” in the view hierarchy of the debugged process. (60255111)

### Devices

#### New Features

*   The “Add Device” sheet in the Devices and Simulators window is now resizable. (59611308)

*   The Devices and Simulators window permits selecting multiple devices in the navigator, so they can be unpaired together. This eases the removal of old records for devices that are no longer in use. (63290367)

### Documentation Viewer

#### New Features

*   The Developer Documentation window has a new Featured page with an overview of Apple’s latest developer documentation. (59319966)

### Instruments

#### New Features

*   You can now export Analysis Core Tables from existing Instruments `.trace` files using the `xctrace` command. See the `xctrace` man page for more details. (12491801)

*   Instruments now supports better expansion of inlined functions in call trees and event backtraces when a dSYM is present. (16252965)

*   Instruments now annotates applicable CPUs as Efficient or Performance. Selecting a CPU will show relevant details, including call trees with data constrained to that CPU. (38031506)

*   Instruments can now import data from `.logarchive` files. Instruments imports these files using the new Logging template that contains the `os_signpost` and `os_log` tools. To customize which template to use during import, use File > Import To Template… (38422518)

*   The `xctrace` command can now attach to an existing process by name using the `--attach` flag. (47649439) (FB5645940)

*   The File Activity template now provides aggregate statistics for logical reads and writes, in addition to individual detail views for Disk Reads and Disk Writes. (52148749)

*   The System Trace template is significantly more performant on new recordings and imported files. (55037273)

*   Files with symbol-heavy recordings are now 80-90% smaller, because of optimized `.trace` symbol storage. (56048324)

*   Instruments includes a new Animation Hitches template for detecting scrolling and animation issues, to help you visualize and investigate an application’s graphics pipeline. (56553023)

*   Double-clicking events in the track view will now switch to a detail view that shows the underlying data at the inspected time so you can further investigate. (59173526)

#### Resolved

*   Fixed an issue where double-clicking on a Call Tree node to move to source failed for any track without an instrument. (32751506)

*   Thread names in Instruments now reflect values set by developers utilizing thread-naming APIs. (51279758)

*   Significantly improved trace saving and loading performance. Saves are now up to 40% faster. Opening trace files is up to 80% faster. (51597633)

*   Fixed an issue where the `<slice>` attribute for a `<calltree>` detail was ignored on Custom instruments. (61944832)

### Interface Builder

#### New Features

*   Added support for the new [`safeAreaLayoutGuide`](https://developer.apple.com/documentation/appkit/nsview/3553228-safearealayoutguide) on [`NSView`](https://developer.apple.com/documentation/appkit/nsview) introduced in macOS 11. (16915977)

*   Introduced a new minimap for the Interface Builder canvas. You can show and hide the minimap with Editor > Canvas > Minimap. Drag the minimap to any corner of the canvas. You can also double-click or command-click in the minimap to focus on a specific scene. (19218249) (FB5891904)

*   Find and Replace now includes matches in attributed string literals. (21508424)

*   Interface Builder now has a Current Date option for [`NSDatePicker`](https://developer.apple.com/documentation/appkit/nsdatepicker). (56048031)

*   Standard spacing constraints are now created by default when items are positioned a standard distance from each other. (57057604)

*   Added support for SF Symbols in macOS 11 (58480276)

*   Added support for [`UIButton.ButtonType.close`](https://developer.apple.com/documentation/uikit/uibutton/buttontype/close). (59211094)

*   Added support for [`NSTextView`](https://developer.apple.com/documentation/appkit/nstextview) and [`NSTextField`](https://developer.apple.com/documentation/appkit/nstextfield) new content type property in macOS 11. (59273897)

*   Added support for the new [`toolbarStyle`](https://developer.apple.com/documentation/appkit/nswindow/3608199-toolbarstyle) in macOS 11. (59274307)

*   Added support for the new [`subtitle`](https://developer.apple.com/documentation/appkit/nswindow/3608198-subtitle) property in macOS 11. (59274358)

*   Added support for the new [`NSSearchToolbarItem`](https://developer.apple.com/documentation/appkit/nssearchtoolbaritem) in macOS 11. (59277905)

*   Added support for selecting text styles in macOS 11. (59297807)

*   Added support for the new [`NSTableViewStyle`](https://developer.apple.com/documentation/appkit/nstableviewstyle) with Automatic, Full Width, Inset, and Source List options. (61958249)

*   Added support for the new [`NSView`](https://developer.apple.com/documentation/appkit/nsview) Layout Margins Guide. (62908200)

*   The Objects library contains a new Window Controller with Sidebar object, composed of a window controller and split view controller configured to provide a toolbar, sidebar, and full-size content view with safe area layout guides enabled. (63045604)

*   The rendering mode and symbol scale properties of SF Symbols for iOS are now editable. Once an SF Symbol is selected in the image picker, the additional properties will expand below the image name. (63280118)

#### Resolved

*   Fixed a bug where `IBDesignable` views weren’t using the intrinsic content size the first time Interface Builder displays the storyboard or `.xib`. (23234553) (FB5797024)

*   When an `IBDesignable` view fails to build, there is now an error directly on the view in canvas. Clicking the error icon on the IBDesignable property in the Identity inspector, now provides a popup that displays the error for easier debugging. (56408987)

*   Storyboards and `.xib` files will now use the intrinsic content size provided by an `IBDesignable` view when overriding [`intrinsicContentSize`](https://developer.apple.com/documentation/appkit/nsview/1526996-intrinsiccontentsize) on an `NSView`. (56419405)

*   Fixed a bug where the Spell Checking property was ignored on [`UITextView`](https://developer.apple.com/documentation/uikit/uitextview). (60750116) (FB7636246)

*   Fixed an issue where images with Preserves Vector Representation enabled wouldn’t correctly display light or dark variants in the canvas. (61243894) (FB7649981)

*   The options on the Layout property of a view (in the Size inspector) have been renamed for greater clarity. The Automatic option is now named Inferred, and indicates whether the view is using constraints or an autoresizing mask.

    A view whose Layout is Inferred uses `Translates Autoresizing Mask Into Constraints = false` when the view is using constraints or is in an Auto Layout container, such as an [`NSStackView`](https://developer.apple.com/documentation/appkit/nsstackview) or [`UIStackView`](https://developer.apple.com/documentation/uikit/uistackview). Otherwise, it uses autoresizing masks and `Translates Auto Resizing Mask Into Constraints = true`.

    For a view whose Layout is Autoresizing Masks, Translates Auto Resizing Mask Into Constraints is always true. (61561405)

*   Fixed a crash that could happen when using Image Stacks in tvOS storyboards. (62113733) (FB7671430)

### Linking

#### New Features

*   The linker now supports `@filename` response files. The contents of the file are substituted into the argument list in place of the file name. The linker is typically invoked through Clang, which already supports response files. To have the linker parse a response file instead of Clang, use `-Wl,@filename`. (54356464) (FB7037642)

*   When the deployment target is iOS 14 or higher, the linker now converts Objective-C method lists into a new, smaller, read-only relative methods list in `__TEXT`. These binaries won’t work on older versions of iOS. (56880461)

*   The linker now reports a warning if you link with a dylib but don’t use any symbols from it. If you really mean to do this, you can either suppress all such warnings with `-Wl,-warn_unused_dylibs` or mark unused frameworks individually as needed, using `-needed_framework Foo` instead of `-framework Foo`. For example, in Other Linker Flags, add `-Wl,-needed_framework,Foo`. (60936600)

#### Resolved

*   When using the `-map file` option, functions and data from `.o` files built for Link Time Optimization are now tracked more accurately. (50031245)

*   When encountering an error about misaligned pointers, the linker now shows all such pointers, instead of just the first. (61019996)

### Metal

#### New Features

*   The new Summary Page in Metal Debugger provides an overview of captured command buffers, performance metrics, and memory usage. Xcode analyzes the commands and provides a list of insights that describe potential issues you may want to investigate. From the summary screen, you can navigate to more detailed information about each topic area. (53887141)

*   When capturing data on a device with A11 or newer GPUs, Metal System Trace tracks start and end times for individual shaders, which provides more granular insights into how the GPU executes your code. (54615187)

*   In Instruments, GPU Counters are now available for macOS in addition to iOS. Use GPU Counters to get more information about how the GPU runs your shader code, such as whether the shader code is underutilizing the GPU or bottlenecked in a particular part of the GPU. (55966447)

*   Shader Validation detects common shader bugs. Turn on Shader Validation when debugging your app to look for illegal memory access and other problems that can otherwise be difficult to debug. (56194992)

*   The GPU Counter view in Metal Debugger has a new user interface, making it easier to filter and sort through the GPU counter data. Create your own counter sets to see the exact data you need to diagnose your app’s performance. (56792744)

### Organizer

#### New Features

*   Metrics Charts in Xcode Organizer are now interactive, allowing developers to compare and contrast metrics associated with different versions of their applications. (49305896)

*   Xcode Organizer now displays scroll-hitch metrics. Use these metrics to help identify perceptible animation delays you encounter while scrolling in your application. To view the Scroll Hitch bar graph, click on the Scrolling section in the Metrics Organizer window. (53514128)

*   Xcode Organizer now provides Disk Writes diagnostic reports. Use these reports to optimize the disk-write performance of your apps. To view the reports, click on the Disk Writes item in the Reports section of the Organizer. (53514182)

*   Metrics in the Xcode Organizer now include data from app versions with limited field usage. App versions that don’t meet the previous year’s usage threshold are badged with a gauge icon next to the version number, and display a margin of error. As customer usage increases, the margin of error decreases until it is low enough that it can be omitted from the UI. (53514245)

### Playgrounds

#### New Features

*   Xcode Playgrounds can now import and use Swift packages and frameworks. Select the Build Active Scheme checkbox in the playground’s File inspector and ensure that the active scheme builds the package or framework target. (60612584)

*   Xcode’s Report Navigator now includes Playground build logs. (56351128)

*   Xcode Playgrounds now build the active scheme’s targets and make them importable when Build Active Scheme is enabled in the File inspector. (60089627)

#### Resolved

*   Live views are now accessible to VoiceOver. (40548790)

*   Resolved an issue causing the LLDB RPC server to crash while using Xcode Playgrounds. (59271354)

*   Live views in iOS and tvOS Playgrounds now use the view’s intrinsic content size if the view receives a zero size. (61068790)

*   Playgrounds now support asset catalogs. (61110861)

*   The live view of a macOS Playground falls back to a sensible default size, if the view has no inherent size. (62065321) (FB7670503)

*   If a Playground live view has a size of zero, a banner now indicates why the live view isn’t visible. (63033441)

*   An Xcode Playground now automatically compiles Core ML models in its Resources folder and Playground code can access the generated ML model interface. (63109576)

### Previews

#### New Features

*   Xcode now considers edited files and open previews when selecting which app renders previews. Files contained in an application-linked framework now preview inside of the application, picking up any resources and entitlements provided by the application. (46057388)

*   Each preview now has buttons to start Live Preview, Preview on Device, Inspect Preview, and Duplicate Preview. (47472549)

*   The canvas has a new integrated experience for adding modifiers. Click the Inspect Preview button to see modifier recommendations for the selected view and search for the modifier you want to apply. (51696163)

*   Code completion now inserts a compilable completion and example for SwiftUI views and modifiers. (55455037)

*   Xcode supports previewing widgets. For an example of how to configure a widget preview, see [`WidgetPreviewContext`](https://developer.apple.com/documentation/widgetkit/widgetpreviewcontext). (56390347)

*   The Attributes inspector now offers quick actions for editing the name, device, layout, preferred color scheme, and accessibility text size of a selected preview. (56413241)

*   Xcode Previews now supports previewing views in frameworks on-device if the framework is linked by an app in the selected scheme. (57025579)

*   Xcode now supports previewing SwiftUI watchOS complications by adding the [`previewContext(_:)`](https://developer.apple.com/documentation/swiftui/view/previewcontext(_:)) modifier to a watchOS complication. (57848297)

*   Xcode now supports previews for App Clips. (59227941)

*   Xcode now connects with the new Xcode Previews app for iOS 14 and iPadOS 14 for greatly improved on-device previews. The Xcode Previews app seamlessly displays changes from Xcode Previews on devices. The first time you use on-device previews, the Xcode Previews app appears on your device’s homescreen. Launching Xcode Previews on a device after disconnecting from Xcode restores the last-displayed preview. (59631753)

*   Double-clicking a view in a preview now selects the corresponding code and moves keyboard focus to the source editor, allowing for quick editing of a view’s contents. (60171349)

*   The bottom bar of the canvas now contains a button for quickly inspecting the selected view. (62990297)

*   Add custom SwiftUI views and modifiers to the Xcode library using the new [`LibraryContentProvider`](https://developer.apple.com/documentation/developertoolssupport/librarycontentprovider) protocol. (63154504)

#### Resolved

*   Rebuilding against the iOS 14, macOS 11, watchOS 7, and tvOS 14 SDKs changes uses of [`GeometryReader`](https://developer.apple.com/documentation/swiftui/geometryreader) to reliably top-leading align the views inside the [`GeometryReader`](https://developer.apple.com/documentation/swiftui/geometryreader). This was the previous behavior, _except_ when it wasn’t possible to detect a single static view inside the [`GeometryReader`](https://developer.apple.com/documentation/swiftui/geometryreader). (59722992) (FB7597816)

### Project Editor

#### New Features

*   The Document Types, Exported Type Identifiers, and Imported Type Identifiers panes support the new templated document icons in macOS 11. (59314567)

### Project Navigator

#### New Features

*   The selection in the Project navigator, Source Control navigator, Debug navigator (for View Debugger and Memory Graph) and Reports navigator now tracks the contents of the active editor. (9546415) (FB5634395)

*   Xcode’s navigators now respect the System “sidebar icon size” and also allow it to be changed independently of that setting. (11619444)

*   File results in the Find navigator are now adorned with a path showing their workspace location. (47196462)

*   The Project navigator now allows control over text-matching style (“contains”, “does not contain”, “begins with”, or “ends with”) when typing a filter term and pressing enter. (56474089)

*   Open Quickly matches are now more targeted and focused. Open Quickly is better at finding discontiguous word matches. Typing “resetDownload” matches “resetDocumentDownload” as you’d expect. The improved accuracy focuses on the best matches, and excludes the worst. (59065704)

*   Text filtering in the jump bar, scheme menu, and run destination chooser is significantly improved. It shows the best matches, and suppresses the worst. Filtering for frequently occurring characters like `init` will show just init methods, instead of every symbol that contains i, n, i, t. (59597035)

#### Resolved

*   Resolved crashes when adding and moving items in the project structure. (48644008, 57752303)

*   Improved performance of Project navigator, in particular “Reveal in Project Navigator” and recursive expand / collapse operations on groups. (49189414, 60245991, 6092575)

*   Improved stability and accuracy of results when filtering the project structure for text and SCM status. Note that results now require all filter terms to match, instead of any term. (57708582, 58099589, 62128435)

### Refactoring

#### New Features

*   Editor > Refactor > Rename now handles renaming symbols with a definition or references that are escaped with backticks. (46409010)

### Server

#### Resolved

*   You can select which branch to use for integrations on the Repositories tab of an Xcode Server bot. (59068222, 58615215)

### Simulator

#### New Features

*   Simulator can display a simulated device in full-screen mode, or tile its window alongside Xcode. (32866357)

*   Simulator now supports 64-bit and 32-bit processes for watchOS 7. To verify watchOS projects are 64-bit clean in Simulator, make sure `ARCHS` is set to its default value. (54654060)

*   Window > Stay On Top keeps device windows in front of other application windows. (57060945) (FB7439463)

*   When a device window loses focus, it pauses capturing input events from Send Pointer to Device and Send Keyboard Input to Device until Simulator regains focus. (57351155)

*   Simulator defaults to the internal microphone unless you explicitly choose a different audio source. This avoids triggering phone call mode on Bluetooth headsets which degrades audio quality while listening to music. (59338925, 59803381)

*   Simulator supports simulating Nearby Interaction for devices that support the feature. Dragging the device window around on the screen will update the simulated distance between the two devices. The farther apart the windows are on screen the greater the reported distance. (62227375)

#### Resolved

*   The Download Components preferences pane now prompts once for authentication to download and install legacy simulators, rather than prompting for authentication on each install. (22993731)

*   CoreSimulatorService doesn’t use as much CPU when clients rapidly connect and disconnect. (53220616)

*   Simulator now allows selecting the Physical Size, Point Accurate, and Pixel Accurate size options, even if the chosen option causes part of the window to be off-screen. (56163353) (FB7366108)

*   Simulator runtimes now persist when updating Xcode from the app store, moving Xcode, or renaming Xcode. (58100481)

*   When entering keyboard- or pointer-capture mode with keys held down Simulator no longer leaves those keys stuck in macOS. When exiting capture mode the correct left or right key-up event is delivered to the guest to prevent it from thinking a modifier key is stuck. (60174685)

*   Simulator no longer creates default devices in custom device sets, restoring the behavior of Xcode 11.3. (63750578) (FB7717786)

### Source Editor

#### New Features

*   Repeated code completion invocations inside Swift function bodies are now up to 15 times faster compared to Xcode 11.5. (59830963)

#### Resolved

*   Fixed a crash that could occur with large amounts of log output in the debug console. (49261867)

*   The editor now preserves the relative indentation of pasted text, rather than re-indenting the text. This can be controlled in Preferences > Text Editing > Indentation. (52348424)

*   Fixed an issue where the `com.apple.dt.SKAgent` process would consume a lot of memory in large projects with mostly flat hierarchies of source files. (53835770)

*   Fixed an issue where code completion sometimes suggests a class name rather than a variable name. (56887185)

*   Fixed a problem where incorrect content would show up in the jump bar for system headers. (57509269)

*   Fixed a problem where pasting into multiple insertions points would reset the selection to a single insertion point. (57572639)

*   Fixed an issue where code completion suggests a case-insensitive match candidate in the most recently used list, instead of a lowercase, case-sensitive match candidate. (57962108) (FB7495633)

*   Fixed an issue where typing a backtick in documentation, with the Text Editing preference Enable type-over completions unchecked, would insert an extra backtick. (58011556)

*   Fixed an issue where editing a file outside of Xcode would cause Xcode to crash on launch. (58272739)

*   Fixed issues where Xcode wouldn’t properly save edits to `Date` and `Data` values in property list files. (58836269)

*   Improved the display order in code completion to prioritize symbols matching parameter types. (59066628)

*   [Callable values of user-defined nominal types](https://github.com/apple/swift-evolution/blob/master/proposals/0253-callable.md) is now supported in Swift code completion. Code completion shows the calling signature after a base expression followed by an opening parenthesis. (59302416)

*   A breakpoint hidden within multiple code folds now correctly expands the folded code when the debugger hits it or when it’s selected in the Breakpoint navigator. (59445409)

*   Fixed an issue where folding code would sometimes cause a crash. (60170676)

*   Fixed an issue where Xcode would hang after multiple large refactors. (61749114)

*   Fixed an issue where editing an Objective-C category name would sometimes cause a crash. (61860583)

*   Fixed an issue where folding code with trailing whitespace would sometimes cause a crash. (62218489) (FB7673070)

### StoreKit

#### New Features

*   Xcode 12 supports testing in-app purchases directly in Simulator or on a connected device, using a new local [StoreKit](https://developer.apple.com/documentation/storekit) test environment.

    Configure in-app purchase information locally for testing, before setting it up in App Store Connect and without a connection to App Store servers. For more information on getting started, see [Testing In-App Purchases in Xcode](https://developer.apple.com/documentation/storekit/in-app_purchase/testing_in-app_purchases_in_xcode) and [Setting Up StoreKit Testing in Xcode](https://developer.apple.com/documentation/xcode/setting_up_storekit_testing_in_xcode). The test environment supports early development, unit testing, and debugging in-app purchases, as described in [Testing at All Stages of Development with Xcode and Sandbox](https://developer.apple.com/documentation/storekit/in-app_purchase/testing_at_all_stages_of_development_with_xcode_and_sandbox).

    Use the [StoreKit Test](https://developer.apple.com/documentation/storekittest) framework to create and automate tests for handling in-app purchase transactions. [StoreKit Test](https://developer.apple.com/documentation/storekittest) supports comprehensive testing of in-app purchase scenarios, including changes in subscription status, subscription offers, restore purchases, ask to buy, interrupted purchases, and more.

    Control the test environment, including clearing purchase history, resetting offer eligibility, and speeding up the renewal rate of time for testing subscriptions. (56504988)

### Swift

#### New Features

*   Swift indentation has been overhauled, greatly improving the indentation of chained methods calls, especially those that involve nested or trailing closures. (25519439) (FB5472851)

*   Improved the error message when using SwiftUI’s [`List`](https://developer.apple.com/documentation/swiftui/list) initializer that takes a collection of identifiable data with an element type that doesn’t conform to [`Identifiable`](https://developer.apple.com/documentation/swift/identifiable). (51519565) (FB6130940)

    For example, the following code:
    ```swift
    import SwiftUI

    struct NotIdentifiable {}

    let data: [NotIdentifiable] = []

    List(data) { _ in
        Text("Row")
    }
    ```
    now produces the error message:
    ```
    error: initializer 'init(_:rowContent:)' requires 'NotIdentifiable' conform to 'Identifiable'
    List(data) { _ in
    ^
    ```

*   Swift indentation now column-aligns conditions in `guard` and `if` statements. (53131527) (FB6688335)

    For example:
    ```swift
    guard let x = someOptional,
          let y = anotherOptional else {
      // ...
    }
    ```

*   The compiler now diagnoses exclusivity violations within code that computes the `default` argument during [`Dictionary`](https://developer.apple.com/documentation/swift/dictionary) access. ([SR-11700](https://bugs.swift.org/browse/SR-11700), 56378713)
    ```swift
    struct Container {
      static let defaultKey = 0

      var dictionary = [defaultKey:0]

      mutating func incrementValue(at key: Int) {
        dictionary[key, default: dictionary[Container.defaultKey]!] += 1
      }
    }
    // error: overlapping accesses to 'self.dictionary', but modification requires exclusive
    // access; consider copying to a local variable
    //     dictionary[key, default: dictionary[Container.defaultKey]!] += 1
    //     ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    // note: conflicting access is here
    //     dictionary[key, default: dictionary[Container.defaultKey]!] += 1
    //                              ~~~~~~~~~~^~~~~~~~~~~~~~~~~~~~~~
    ```

    The exclusivity violation can be avoided by precomputing the `default` argument using a local variable.
    ```swift
    struct Container {
      static let defaultKey = 0

      var dictionary = [defaultKey:0]

      mutating func incrementValue(at key: Int) {
        let defaultValue = dictionary[Container.defaultKey]!
        dictionary[key, default: defaultValue] += 1
      }
    }
    // No error.
    ```

*   Swift now allows the implicit use of `self` in `@escaping` closures when reference cycles are unlikely to occur. ([SE-0269](https://github.com/apple/swift-evolution/blob/master/proposals/0269-implicit-self-explicit-capture.md), 56408426)

    First, implicit use of `self` in `@escaping` closures is now allowed if the user has explicitly captured `self` in the closure’s capture list, so the following code is now valid:
    ```swift
    class Test {
      var x = 0
      func execute(_ work: @escaping () -> Void) {
        work()
      }
      func method() {
        execute { [self] in
          x += 1
        }
      }
    }
    ```

    Second, implicit `self` is available in `@escaping` closures when `self` is a value type, making the following code valid:
    ```swift
    struct Test {
      var x = 0
      func execute(_ work: @escaping () -> Void) {
        work()
      }
      func method() {
        execute {
          x += 1
        }
      }
    }
    ```

*   A property with an attached property wrapper can now rely on type inference to infer the wrapped value type when using default initialization without empty parentheses on the wrapper attribute. For example:
    ```swift
    @propertyWrapper
    struct IntWrapper {
      var wrappedValue: Int { 0 }
    }

    struct UseWrapper {
      @IntWrapper var value
    }
    ```

    The wrapped property `UseWrapper.value` uses default initialization of `IntWrapper`, and relies on type inference to deduce the type-wrapped value type to be `Int`. (59471019)

*   In order to shorten incremental compilations, Swift now keeps separate fingerprints for each type- (and protocol-) body. These _type-body fingerprints_ mean that if you change the body of a `struct`, `enum`, `class`, or `protocol` in a file that also defines other `struct`, `enum`, `class`, `protocols`, only the changed entity will be counted as “dirty” for the purpose of recompiling other files. For example, suppose you have a file that defines two `structs`:
    ```swift
    struct A {
    }
    struct B {
    }
    ```

    and you add a member to `A`:
    ```swift
    struct A {
      var x = 17
    }
    struct B {
    }
    ```

    Before this change, the compiler would have recompiled any file using either `A` or `B`. Now, the compiler doesn’t recompile files that use only `B`.

    If you experience problems with this feature, disable it by passing `-disable-type-fingerprints` into the Swift compiler via the `Other Swift Flags` build setting. If you still experience problems, disable the new dependency infrastructure by passing `-disable-fine-grained-dependencies` into the Swift compiler via the `Other Swift Flags` build setting. (59954707)

*   Declarations inside generic contexts can now have `where` clauses even when the declaration itself doesn’t have additional generic parameters. ([SE-0267](https://github.com/apple/swift-evolution/blob/master/proposals/0267-where-on-contextually-generic.md), 64228492)

    For example:
    ```swift
    struct Box<Wrapped> {
        func boxes() -> [Box<Wrapped.Element>] where Wrapped: Sequence { ... }
    }
    ```

*   `lazy` properties may now have `didSet` and/or `willSet` observers. (64229062)

#### Resolved

*   Swift now supports unapplied references to protocol methods. Previously this only worked for methods defined in structs, enums, and classes. (21289579) (FB5819096)

    For example:
    ```swift
    protocol Cat {
        func play(catToy: Toy)
    }

    let fn = Cat.play(catToy:)
    fn(myCat)(myToy)
    ```

*   Swift indentation no longer under-indents multi-line expressions that appear within call arguments, parameter lists, array and dictionary literals, or tuples when their elements are column-aligned. (48934744)

*   The experimental function builder feature is now correctly applied to a single-expression closure. For example:
    ```swift
    @_functionBuilder
    struct ArrayBuilder<T> {
        static func buildBlock(_ values: T…) -> [T] {
            values
        }
    }

    func array(@ArrayBuilder<Int> builder: () -> [Int]) -> [Int] {
        builder()
    }

    array { 0 }
    ```

    These closures already worked in SwiftUI because they were just returning a single [`View`](https://developer.apple.com/documentation/swiftui/view), which is all that applying the [`ViewBuilder`](https://developer.apple.com/documentation/swiftui/viewbuilder) transform to them would have made them do. However, not all function builder transforms have this property, and now they should work in general. (56340587)

*   Fixed a compiler crash that happened when using a property wrapper whose wrapped value has a mutating getter and non-mutating setter. (56467140)

*   The Swift compiler no longer prints imports in the compatibility header for empty extensions or extensions with only private members and no public conformances.

    Objective-C/C source files relying on those transitive imports may raise errors about missing declarations and need to be updated with an explicit importation to compile as expected. (57133517)

*   Fixed a crash caused by importing Objective-C interfaces that use the `objc_runtime_name` into Swift. (59306590) (FB7571694)

*   Fixed a compiler crash that happened when overriding a property with an attached property wrapper in a subclass to implement property observers. (60093232) (FB7615016)

*   Fixed an issue where initializing a property wrapper could invoke property observers before all of `self` is initialized. (60832285)

*   Fixed an issue where global rename could alter SDK headers (62607314) (FB7681195)

### Swift Packages

#### New Features

*   You can now declare conditions for a Swift package’s target dependencies, such as limiting the dependencies by platform. This gives you more flexibility to describe complex target dependencies that support multiple platforms. (40237402)

*   Swift packages can now contain resources such as images, asset catalogs, storyboards, and other files. When Xcode builds an app that depends on a package, it adds the package’s code and resources to the app bundle for use at runtime. For more information see [Bundling Resources with a Swift Package](https://developer.apple.com/documentation/swift_packages/bundling_resources_with_a_swift_package). (54361843)

*   Swift packages can now vend prebuilt libraries distributed as XCFrameworks, allowing dependencies on libraries that can’t be distributed as source code. When Xcode builds an app that uses such a package, it embeds the libraries into the app bundle. For more information see [Distributing Binary Frameworks as Swift Packages](https://developer.apple.com/documentation/swift_packages/distributing_binary_frameworks_as_swift_packages). (56592977)

*   Swift packages can now contain localized content for any resource in the package. In addition to localized content in asset catalogs, Xcode supports separate localization files in `.lproj` folders. For more information see [Localizing Package Resources](https://developer.apple.com/documentation/swift_packages/localizing_package_resources). (56925255)

### Testing

#### New Features

*   [`XCTAssert`](https://developer.apple.com/documentation/xctest/xctassert) and related assertion macros in Objective-C can now be used in contexts other than instance methods of [`XCTestCase`](https://developer.apple.com/documentation/xctest/xctestcase) subclasses. (4176422)

*   Xcode now captures backtraces for test failures which occur outside of test methods and lists the failure callstack frames in the Issue navigator, the source editor, and the test report. (9955893)

*   UI Tests will now implictly handle banner notifications on iOS that block the navigation bar during UI testing. (24920246)

*   [XCTest](https://developer.apple.com/documentation/xctest) now provides an [`XCTIssue`](https://developer.apple.com/documentation/xctest/xctissue) type for richer modeling of test failures and other issues, along with associated APIs for working with these issues, including a new [`recordIssue:`](https://developer.apple.com/documentation/xctest/xctestcase/3546549-recordissue) method on [`XCTestCase`](https://developer.apple.com/documentation/xctest/xctestcase) which supersedes [`recordFailureWithDescription:inFile:atLine:expected:`](https://developer.apple.com/documentation/xctest/xctestcase/1496269-recordfailurewithdescription). (28547702)

*   If the test process fails to launch or load the test bundle, for example if dynamic linking fails, or some other system failure prevents testing from starting, the error is presented in the test report under a section titled “System Failures”. (36926043)

*   The number of passing, failing, and skipped tests is now surfaced in the test report UI. (49672520)

*   When building for testing in a test plan-enabled scheme, Xcode now only builds test targets which are referenced by the active test plan. If the scheme references multiple test plans, then test targets which aren’t referenced by the currently-active test plan aren’t built. This change doesn’t affect `xcodebuild`: it builds all test targets referenced by all of the scheme’s test plans, unless one or more `-testPlan <name>` arguments are specified. (49737598)

*   [`XCTApplicationLaunchMetric`](https://developer.apple.com/documentation/xctest/xctapplicationlaunchmetric) can now measure application launch to first frame. This new metric measures the time it takes for an application to launch and be ready to respond to a touch event. The following shows an example of using [`XCTApplicationLaunchMetric`](https://developer.apple.com/documentation/xctest/xctapplicationlaunchmetric) to measure how long it takes for an application to become responsive. (54721394)
    ```swift
    func testAppLaunchToResponsive() throws {
        measure(metrics: [XCTApplicationLaunchMetric(waitUntilResponsive: true)]) {
            app.launch()
        }
    }
    ```

*   Xcode now excludes static library targets when computing the list of built product directories to include in the DYLD_FRAMEWORK_PATH and DYLD_LIBRARY_PATH environment variables when running tests. (55254152) (FB7249507)

*   Performance XCTests now support animation performance testing when using [`XCTOSSignpostMetric`](https://developer.apple.com/documentation/xctest/xctossignpostmetric) coupled with an animation `os_signpost` interval. The performance measurements returned include duration, three hitch-related metrics, and frame rate. To create an animation `os_signpost` interval, create a custom interval or use one of the provided UIKit intervals. The following shows an example performance test that measures the animation performance of scrolling an application. (55644042)
    ```swift
    func testScrollingAnimationPerformance() throws {
      let table = app.tables.firstMatch
      measure(metrics: [XCTOSSignpostMetric.scrollDecelerationMetric]) {
        table.swipeUp(velocity: .fast)
      }
    }
    ```

*   If the test process stalls while waiting on an expectation, such as during [`waitForExpectations(timeout:handler:)`](https://developer.apple.com/documentation/xctest/xctestcase/1500748-waitforexpectations) or a similar [`XCTWaiter`](https://developer.apple.com/documentation/xctest/xctwaiter) method, Xcode captures a spindump of the test process and attaches it to the test report. Previously, Xcode killed the test process and restarted execution with the next test. To continue to protect against stalled tests, enable the Test Timeouts setting in the test plan. (57163494)

*   Xcode 12 expands on the ability to reset the authorization status of protected resources, introduced in Xcode 11.4. Health resources can be reset using the new constant [`XCUIProtectedResource.health`](https://developer.apple.com/documentation/xctest/xcuiprotectedresource/health) which is available in iOS 14.0 and later. (57852954)

*   [`XCUIElement`](https://developer.apple.com/documentation/xctest/xcuielement) and [`XCUICoordinate`](https://developer.apple.com/documentation/xctest/xcuicoordinate) now allow specifying a velocity when performing swipe and drag interactions. (58059937)

*   Screenshots taken during UI tests are now encoded as HEIC files instead of JPEGs where possible. This can considerably reduce the file size of result bundles. (58468642)

*   [`XCTAssertEqual(_:_:accuracy:_:file:line:)`](https://developer.apple.com/documentation/xctest/3551607-xctassertequal) and [`XCTAssertNotEqual(_:_:accuracy:_:file:line:)`](https://developer.apple.com/documentation/xctest/3551608-xctassertnotequal) now accept any [`Numeric`](https://developer.apple.com/documentation/swift/numeric) value instead of requiring a [`FloatingPoint`](https://developer.apple.com/documentation/swift/floatingpoint) value. This allows passing non-floating point numeric types such as [`Int`](https://developer.apple.com/documentation/swift/int), either as expression values or as the `accuracy` parameter. (58481784)

*   Running an individual test in a test-plan-enabled scheme now skips configurations in that test plan which are disabled. Option- or Control-clicking a test diamond now denotes any configurations in the active test plan are disabled, and includes a “Run in All Enabled Configurations” option if some are disabled. (58547265)

*   If you click the diamond next to a test or test class in the source editor, and that test is outside of the active scheme or test plan, Xcode will present a sheet allowing you to select the specific scheme or test plan that contains the test you want to run. (59223004)

*   The Failed and Skipped scope bar buttons in the Test Report now show tests where any runs failed or were skipped, instead of only showing tests where all runs failed or were skipped. (59401757)

*   The Test navigator now supports filtering skipped tests, in addition to failed tests and tests only contained in the active scheme. (59519058)

*   When running tests in a test-plan-enabled scheme, Xcode now honors the “Debug XPC services” setting from the Options tab of the scheme’s Run action. (60439063)

*   It is now possible to customize Default Execution Time Allowance and Maximum Execution Time Allowance in the Test Plan Editor. These settings apply when Test Timeouts is enabled. (61607966)

*   XCTest now attaches a spindump diagnostic during UI testing when a UI query times out or the target app doesn’t become idle promptly. (62076023)

#### Resolved

*   The Test navigator now correctly remembers its selection state and scroll offset when switching to and from other navigators, as well as when changing filters and schemes. (16308307, 24918098)

*   Resolved a bug which prevented diamonds from appearing next to test methods and classes in the source editor when the Test navigator isn’t open. (54216504)

*   When a test failure is recorded without any source code location, Xcode now displays a failure annotation in the source editor and a link to jump to that test method from the Issue navigator. (58118593)

*   Resolved an issue that could cause keyboard modifiers to persist after a call to [`performWithKeyModifiers:block:`](https://developer.apple.com/documentation/xctest/xcuielement/1500563-performwithkeymodifiers) if the block threw an unhandled exception. (58376575)

*   XCTest APIs which include a `file: StaticString = #file` parameter now use the `#filePath` literal introduced in Swift 5.3 as the default parameter value. XCTest requires complete file paths to source files for error reporting and jumping to failures within Xcode. For more information, see notes on [SE–0274](https://github.com/apple/swift-evolution/blob/master/proposals/0274-magic-file.md) and `#filePath` in the Swift section. (58496553)

*   Moving test plan files between directory levels in the Project navigator now updates references to those files in schemes properly. (59171975)

*   Xcode will reinstall the app under test if it was deleted in a UI test. (60159203) (FB7616398)

*   XCTest now supports using [`XCTSkip`](https://developer.apple.com/documentation/xctest/xctskip) in [`tearDown()`](https://developer.apple.com/documentation/xctest/xctest/1500463-teardown) and [`tearDownWithError()`](https://developer.apple.com/documentation/xctest/xctest/3521151-teardownwitherror) to mark a test as skipped. Although the test method may already have run to completion by the time the teardown methods are invoked, this may be useful to “retroactively” mark that a test wasn’t eligible to run or that its results may be invalid. (60634152)

*   Resolved an issue where `xcodebuild` wouldn’t respect the `-enableCodeCoverage` option if the scheme uses a test plan. (62605817)
