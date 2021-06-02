# Xcode 12.5 Beta 3 Release Notes

Update your apps to use new features, and test your apps against API changes.

## Overview

Xcode 12.5 Beta 3 includes SDKs for iOS 14.5, iPadOS 14.5, tvOS 14.5, watchOS 7.4, and macOS Big Sur 11.3. The Xcode 12.5 Beta 3 release supports on-device debugging for iOS 9 and later, tvOS 9 and later, and watchOS 2 and later. Xcode 12.5 Beta 3 requires a Mac running macOS Big Sur 11 or later.

### Code Completion

#### Resolved Issues

*   Code completion now returns suggestions more quickly inside large function bodies. (58687608)

### Debugging

#### Known Issues

*   Xcode fails to launch apps when Nightstand Mode is enabled on Apple Watch. (61351690)

    **Workaround**: Disable Nightstand Mode in Settings > General > Nightstand Mode on the Apple Watch.

*   On Macs with Apple silicon, apps crash when you build and run them using Rosetta translation on macOS Big Sur 11.3 Beta 2. (73456059)

    **Workaround**: Disable debugging using the scheme editor, or upgrade to macOS Big Sur 11.3 Beta 3.

### Devices

#### Known Issues

*   When running on a Mac with Apple silicon, Xcode may fail to connect to an Apple Watch device, presenting a message stating that the connection “is taking longer than expected.” While Xcode offers the option to continue to wait, the connection never completes. (74822495)

    **Workaround**: Develop with a simulated watchOS device, or using an Intel Mac.

### Signing and Distribution

#### Resolved Issues

*   Fixed an issue that caused OS X 10.11 and earlier to reject packages signed on OS X 10.11 and earlier. (71695608)

#### Known Issues

*   OS X 10.11 and earlier may reject code signatures added to universal binaries by Xcode 12.5. (70724583) (FB8830007)

    **Workaround**: Specify `--digest-algorithm=sha1,sha256` to the `codesign` utility at signing time. In Xcode, specify this using the `OTHER_CODE_SIGN_FLAGS` build setting.

### Simulator

#### Known Issues

*   When running a simulated device from a host app (such as Simulator, Xcode, or a CI server) running under Rosetta translation, spawning a new process in the simulated device fails with an “invalid device state” error. (71913373)

    **Workaround**: Launch Simulator or Xcode natively.

*   Siri may not respond to voice input on simulated devices. (74158392, 74297245)

*   Siri isn’t on by default in simulated iOS and iPadOS devices. (74261033)

    **Workaround**: Use the Settings app to enable Siri.

*   Siri isn’t available in simulated tvOS devices. (74261184)

*   You can’t log into iCloud on a simulated device running iOS 14.5, iPadOS 14.5, tvOS 14.5, or watchOS 7.4. (74295005)

### Swift

#### Resolved Issues

*   Fixed an issue where code signing of binary targets might fail with a “bundle format unrecognized, invalid, or unsuitable” error. (74570259) (FB9014663)

#### Known Issues

*   The compiler may generate incorrect code when you use an `enum` `case` with associated values to satisfy a protocol requirement. (72302307)

    For example:
    ```swift
    protocol FileHandlerAction {
      static func setFileURL(_ fileURL: NSURL) -> Self
    }

    enum AppAction : FileHandlerAction {
      case setFileURL(NSURL)
    }
    ```

    **Workaround**: Provide a static method to satisfy the requirement:
    ```swift
    enum AppAction : FileHandlerAction {
      case _setFileURL(NSURL)

      static func setFileURL(_ fileURL: NSURL) -> Self {
        return ._setFileURL(fileURL)
      }
    }
    ```

#### Deprecations

*   The Swift compiler emits a warning for the use of the `await` keyword as an unqualified identifier. Wrap `await` with back-ticks so Swift always treats it as an identifier, or fully qualify declarations named await (for example, by adding `self` if it is a reference to an instance member named `await` from within the instance). ([SE-0296](https://github.com/apple/swift-evolution/blob/main/proposals/0296-async-await.md), 67000350)

### Testing

#### Resolved Issues

*   Xcode no longer incorrectly reports a name that starts with “<unknown>” for tests that the test code dynamically generates at runtime. (73767460)

#### Deprecations

*   Xcode no longer includes XCTest’s legacy Swift overlay library (`libswiftXCTest.dylib`). Use the library’s replacement, `libXCTestSwiftSupport.dylib`, instead. For frameworks that encounter build issues because of the removal of the legacy library, delete the framework and library search paths for `libswiftXCTest.dylib` and add the `ENABLE_TESTING_SEARCH_PATHS=YES` build setting. This setting automatically sets the target’s search paths so that it can locate the replacement XCTest library. (70365050)

## Updates in Xcode 12.5 Beta 2

### General

#### New Features

*   You can create macOS File Provider extensions using the new File Provider Extension target template. (54054417)

### Build System

#### Resolved Issues

*   Builds with Parallelize Build disabled no longer hit a new dependency cycle if a hosted test target with a defined `TEST_HOST` build setting depends on targets other than the one that produces the host bundle. (73210420)

### Instruments

#### Resolved Issues

*   Launching an extension via Product > Profile in Xcode no longer causes Instruments to wait indefinitely for the process to start. (62275419) (FB7674284)

*   Fixed a crash that sometimes occurred when transferring a Metal app from Xcode to Instruments and starting recording. (70655385) (FB8824932)

*   Revised the `xctrace export` XML schema for Run Information. You may need to adjust code that parsed the output from earlier beta releases of Xcode 12.5. (73204384)

*   Fixed a crash that occurred when recording a trace with the Game Performance template. (73265950)

### Signing and Distribution

#### Resolved Issues

*   Resolved an issue that prevented exporting distribution certificates from Xcode due to a keyboard focus issue in the authentication window. (71011727) (FB8880845)

### Simulator

#### Resolved Issues

*   Fixed an issue that caused apps using [`WKWebView`](https://developer.apple.com/documentation/webkit/wkwebview) to crash on simulated devices running iOS 13.7 or earlier on a Mac with Apple silicon. (73375522)

*   Simulated devices running iOS 14.5 and iPadOS 14.5 no longer ignore the Shift key on attached keyboard devices. (73929715) (FB8988913)

### Swift

#### New Features

*   Property wrappers now work in local contexts. (74192307)

    For example, this code is now valid:
    ```swift
    @propertyWrapper
    struct Wrapper<T> {
      var wrappedValue: T
    }

    func test() {
      @Wrapper var value = 10
    }
    ```

### Swift Packages

#### New Features

*   The Swift Package Manager now builds package products and targets as dynamic frameworks automatically, if doing so avoids duplication of library code at runtime. (59931771) (FB7608638)

### Testing

#### New Features

*   The code coverage report now shows the number of executable lines per file. (68808019)

#### Resolved Issues

*   Fixed an issue where methods on [`XCTOSSignpostMetric`](https://developer.apple.com/documentation/xctest/xctossignpostmetric) threw an exception on watchOS. (72552791)

*   Fixed an issue where the [`adjust(toNormalizedSliderPosition:)`](https://developer.apple.com/documentation/xctest/xcuielement/1501022-adjust) method on [`XCUIElement`](https://developer.apple.com/documentation/xctest/xcuielement) would adjust to the wrong value for sliders in Watch apps. (73100059)

*   `xcodebuild test-without-building` no longer runs a test plan or scheme’s tests twice when you have disabled the test target’s “Automatically include new tests” run option. (73230328)

*   Fixed an issue where UI tests running on iOS devices using the arm64e architecture (including iPhone XS and later) failed to launch, with a `Symbol not found` error. (73263692)

*   Test methods and classes written in Swift and that don’t explicitly customize their Objective-C name using `@objc(...)` now work when using the `xctest` or `swift test` command line tools on Apple platforms. (73267118)

*   Fixed an issue where unit tests for a Watch app failed to start after the app launched. (73478326)

## Updates in Xcode 12.5 Beta

### General

#### New Features

*   The Reveal Build Products Folder item in the Product menu reveals the build products directory in Finder. (72248847)

#### Resolved Issues

*   Fixed an issue where code completion, live issues, and other code-analysis features could produce incorrect results after a user moves a source file while an Xcode project is open. (57054858)

*   Large workspaces now open faster. (70276306)

### Apple Clang Compiler

#### New Features

*   The `_LIBCPP_RAW_ITERATORS` macro has been removed from libc++ in favor of using wrapped iterators. (63088925)

### Build System

#### New Features

*   The build system no longer re-signs the hosting app target when building app-hosted test targets; instead it builds test targets before the app target’s sign task runs. This eliminates an extra `codesign` task, which speeds up builds for large apps with such test targets. (47322098)

*   `xcodebuild` now supports the `-archive` flag when creating an XCFramework, providing a shorthand method for creating an XCFramework from one or more archives. (64725832)

    For example:
    ```
    xcodebuild -archive <archive_path1> -framework MyFramework.framework -archive <archive_path2> -framework MyFramework.framework -o <output_xcframework_path>
    ```

#### Resolved Issues

*   The copy files build phase now properly signs code for embedded frameworks with a framework version that isn’t “A”. (55701162) (FB7323980)

*   You can now manually reorder schemes. (61456142)

*   `xcodebuild` no longer double-escapes the output of `xcodebuild -showBuildSettings -json`. (63554669)

*   Preprocess and Assemble single-file actions now work correctly when analyze-while-building is enabled, and no longer display an empty property list in the source editor. (70811963)

### Code Completion

#### New Features

*   Code completion is more reliable in expressions that contain errors, and in expressions that are ambiguous without additional context. (71378252)

    For example, given:
    ```swift
    func test(a: Int, b: String) -> Int { ... }
    func test(a: Int, b: Int) -> String { ... }
    func test(a: (Int, Int) -> Int) -> Int { ... }
    ```

    Invoking code completion after `test().prefix(3).` suggests members of String. Invoking code completion after `test(a: 2).` suggests members of Int and String. Invoking code completion after `$0.` in the following block suggests members of Int:
    ```swift
    test {
      $0.
    }
    ```

### Debugging

#### New Features

*   When debugging C++ programs using libc++, LLDB now offers improved expression evaluation support for STL containers and algorithms.

    *   You can call member functions of STL containers, even if they are never called in the target program.

    *   LLDB can instantiate templated functions from the standard library. This includes algorithms such as `std::sort`, `std::count`, `std::count_if`, etc. (19866497)

### Instruments

#### New Features

*   `<(start|end)-pattern>` elements in os-signpost-interval schema are now optional. This allows Custom Instruments to match signposts by name and other properties without needing to specify the expected message format. (43850670)

*   Profiling XCTest with Instruments now automatically starts the recording, without a click on the record button. (50260328)

*   Instruments can now import `os_log` and `os_signpost` data from the ktrace files that include logging-level data. (56037733)

*   Custom Instruments can now specify statically defined sub-tracks without needing to be driven by table column data. (61367995)

*   `xctrace export` now produces output in time-sorted order. (69804348)

*   Table of Contents query for `xctrace` now exposes metadata information about the run. (71320853)

#### Resolved Issues

*   Fixed an issue where `xctrace` wouldn’t pass a standard input to the launched process. (17842765)

*   Fixed an issue where plot elements wouldn’t draw using the color column specified in a point schema. (71680467) (FB8913696)

### Interface Builder

#### New Features

*   You can now configure a Module for custom classes in the inspector for [`NSObjectController`](https://developer.apple.com/documentation/appkit/nsobjectcontroller) and similar objects. (35971498)

#### Resolved Issues

*   [`NSButton`](https://developer.apple.com/documentation/appkit/nsbutton)’s “Image Only” Position setting now properly displays an image without a title at runtime. (16200971)

*   Fixed an issue where the assistant editor wouldn’t display source code for a selected object’s custom Swift class if the class was annotated with `@objc`. (19623315)

*   Fixed an issue where connect-to-source wouldn’t properly escape Swift keywords in Outlet and Action names. (22527929)

*   Fixed an issue where Editor > Debug Selected Views failed to attach to `@IBDesignable` views for debugging. (45217745) (FB5645911)

*   Added Dark Mode support for the connect-to-source bindings popover. (47583413) (FB5701084)

*   Fixed iOS canvas appearance issues when importing project images with an unexpected scale. (63789933) (FB7719276)

*   Fixed an issue where the assistant editor could open the wrong source file for a selected object’s custom class if duplicate class names existed in the project. (67362709)

*   Fixed the canvas drifting when resizing the document outline. (67505701)

*   Fixed an issue where selecting the custom color item from an inspector’s color popup menu wouldn’t open the system colors picker window. (69365980) (FB8727901)

*   Selecting a view in the canvas and performing Select All (CMD+A) no longer selects the view’s layout guides. (69518746)

*   Fixed an issue where certain connect-to-source popover labels didn’t show up in Dark Mode. (69713404)

*   Fixed an issue where the custom colors swatch in an inspector’s color properties displayed an incorrectly offset focus indicator. (72370447)

### Localization

#### New Features

*   You can now use Xcode to localize applications into all ISO 639 languages. (46806165) (FB5359472)

*   You can now use workspaces to export a collection of projects for localization, generating a single localization catalog for all projects in the workspace. As part of this change, options to import and export for localization are now in the Product menu instead of the Editor menu. You can also use `xcodebuild -importLocalizations` and `xcodebuild -exportLocalizations` with the `-workspace` option to export or import a workspace. (48548375)

*   The new Localization Export Supported build setting lets you disable localization export for a specific target or project that doesn’t require localization. (66606145)

#### Resolved Issues

*   Fixed an issue where the Application Language menu in the scheme editor doesn’t show all languages for which a project is localized. (28872507)

*   `*-InfoPlist.strings` files are now renamed to `InfoPlist.strings` at build-time for bundles that require `Info.plist` localization. This is consistent with existing behavior that renames `Info.plist` files at build-time. (38686398)

*   Exporting and importing for localization now produces an error if two files (ex: Main.strings and Main.storyboard) write translations to the same path. (39917359, 52412470) (FB6384066)

*   Fixed an issue where exporting color sets for localization caused Xcode to crash. (63934393)

*   Fixed an issue where new-style multiline Swift string literals weren’t properly extracted for localization. (64652467) (FB7742731)

*   Localizable keys in `Info.plist` files are now only automatically extracted on localization export for Application and App Extension targets. (66871236)

*   Fixed an issue where strings were replaced with their keys at localization export if the `.strings` file was outside the directory hierarchy of the Xcode project. (69835864) (FB8761502)

### Playgrounds

#### New Features

*   A Playground in an app’s project can now access symbols from the app target. New playgrounds you create have this option on by default. To enable this functionality in existing playground documents, turn on the Import App Types option in the File Inspector. (66357893)

*   Inline results for deeply nested Swift arrays and structs now display more information in Xcode Playgrounds. (67344623)

#### Resolved Issues

*   Fixed an issue that could cause Xcode to show “No editor” when opening a Playground. (56484197)

### Simulator

#### New Features

*   Simulator now supports recording video from within the app. Hold Option when clicking on the screenshot button in the toolbar (or press Command+R) to record a video. Click the red button to stop video recording. (63041314)

*   Simulator can create animated GIFs from video recordings using the new Record Video feature. After recording a video, right-click on the video preview, then select Save as Animated GIF. To keep both the video file and the animated GIF, press and hold Option and select Save Copy as Animated GIF. You can adjust the dimensions and size of the generated GIFs in Simulator Preferences. (65089299)

### Source Control

#### Resolved Issues

*   Fixed an issue where some workspaces could fail to notice project file changes from source control operations until you quit and relaunched Xcode. (3920347)

### StoreKit

#### New Features

*   StoreKit Testing in Xcode now supports testing of non-renewing subscriptions. (59478394)

*   The [StoreKit Test](https://developer.apple.com/documentation/storekittest) framework is now availabe on watchOS. (68152552)

### Swift

#### New Features

*   Incremental compilation is faster in many cases. When you change code within the body of a struct, class, enum, protocol, or extension, Swift now recompiles far fewer files in that module than before. (51230617)

*   Implicit member expressions now support chains of member accesses. (57295228)

    For example, this code is now valid:
    ```swift
    let milky: UIColor = .white.withAlphaComponent(0.5)
    let milky2: UIColor = .init(named: "white")!.withAlphaComponent(0.5)
    let milkyChance: UIColor? = .init(named: "white")?.withAlphaComponent(0.5)
    ```

    As is the case with the existing implicit member expression syntax, the resulting type of the chain must be the same as the (implicit) base, so it isn’t well-formed to write `let cgMilky: CGColor = .white.withAlphaComponent(0.5).cgColor` (unless appropriate white and withAlphaComponent members were defined on CGColor.).

    Members of a “chain” can be properties, method calls, subscript accesses, force unwraps, or optional chaining question marks. Furthermore, the type of each member along the chain is permitted to differ (again, as long as the base of the chain matches the resulting type) meaning the following successfully typechecks:
    ```swift
    struct Foo {
      static var foo = Foo()
      static var bar = Bar()

      var anotherFoo: Foo { Foo() }
      func getFoo() -> Foo { Foo() }
      var optionalFoo: Foo? { Foo() }
      subscript() -> Foo { Foo() }
    }

    struct Bar {
      var anotherFoo = Foo()
    }

    let _: Foo? = .bar.anotherFoo.getFoo().optionalFoo?.optionalFoo![]
    ```

*   Swift includes more checks when bridging data from Objective-C. In particular, the runtime library aborts your program with a suitable error message if it detects a non-nullable pointer that contains a null value. (58650899)

*   Property wrappers are now supported on local variables. (73377111)

*   Functions, subscripts, and initializers may now have more than one variadic parameter, as long as all parameters that follow variadic parameters are labeled. (73676506)

    This makes declarations like the following valid:
    ```swift
    func foo(_ a: Int..., b: Double...) { }

    struct Bar {
      subscript(a: Int..., b b: Int...) -> [Int] { a + b }

      init(a: String..., b: Float...) { }
    }
    ```

#### Resolved Issues

*   Function overloading now works in local contexts, making the following valid:
    ```swift
    func outer(x: Int, y: String) {
      func doIt(_: Int) {}
      func doIt(_: String) {}

      doIt(x)
      doIt(y)
    }
    ```

    In this code, the first `doIt(_:)` calls with an Int value, and the second with a String value. (29312676)

*   The runtime and compiler support for Swift’s `is`, `as?`, and `as!` operators has been overhauled, providing more consistent and predictable behavior. (58991956)

*   If your app (including loaded OS binaries) contains multiple redundant protocol conformances, Swift now uses the first one it finds in the first binary loaded (including in OS binaries). (72049977)

### Swift Packages

#### New Features

*   Swift packages that specify a 5.4 tools version can now explicitly declare targets as executable, which allows the use of the `@main` keyword in package code. ([SE-0294](https://forums.swift.org/t/se-0294-declaring-executable-targets-in-package-manifests/42404), 47691185)

*   Swift Package Manager caches package dependencies on a per-user basis, which reduces the amount of network traffic and increases performance of dependency resolution for subsequent uses of the same package. If needed, you can disable cache use in `xcodebuild` by using the new `-disablePackageRepositoryCache` flag. (72204929)

### Testing

#### New Features

*   XCTest now supports marking test failures as “expected”. Expected test failures don’t impact the overall pass/fail result of the suite containing the test. Xcode displays expected failures differently in the Test Navigator and Test Report, and highlights the line of code where the expected failure occurred along with an optional user description. Expected test failures provide a low-overhead tool for preserving the overall “green” state of a project’s test suite when there are failures which can’t be immediately resolved, ensuring that any new failures are clearly visible. In contrast to skipping a test with [`XCTSkip`](https://developer.apple.com/documentation/xctest/xctskip), a test with an expected failure still runs, reporting any unexpected changes. (13408632)

    To mark a failure as expected, call the new [`XCTExpectFailure`](https://developer.apple.com/documentation/xctest/3726077-xctexpectfailure) API in a test before the code which produces the test failure, for example:
    ```swift
    XCTExpectFailure("…")
    // Perform test which currently fails
    ```

    Additionally, the scope of the expected failure can be limited by enclosing the failing code in a closure:
    ```swift
    // Arrange and act on the test subject

    XCTExpectFailure("…") {
        XCTAssert(…) // Failing assertion
    }

    // Continue test with further assertions etc.
    ```

    By default, if `XCTExpectFailure` is called but the test doesn’t record a failure, XCTest marks the test as having failed due to an “unmatched expected failure”. This can be suppressed for failures which occur non-deterministically, by passing `XCTExpectFailure` an `XCTExpectedFailure.Options` object as a parameter, with its `isStrict` property set to `false`:
    ```swift
    let options = XCTExpectedFailure.Options()
    options.isStrict = false
    XCTExpectFailure("…", options: options)
    // Perform test which sometimes fails
    ```

*   Xcode now allows you to clean test results without having to re-open your workspace by selecting Clean Test Results from Xcode’s Product menu. (16527161)

*   Xcode now supports XCTest unit and UI tests for watchOS apps. When creating a new watchOS app, check the Include tests checkbox to add a unit and UI test target to the newly created project. For an existing project, add a unit or UI test target via File > New > Target, and then add the test target to the Test action of the WatchKit App scheme. To run the tests, select a watch simulator or device from the run destinations menu in the toolbar, and then choose Product > Test. Note that testing is supported on watchOS 7.4 or later. (21395998)

*   XCTest now automatically includes specialized subclasses of Swift generic test classes when running tests on macOS 11.3, iOS 14.5, tvOS 14.5, watchOS 7.4, or later OS versions. This allows you to use generics to improve reusability of test classes. (23493200)

*   XCTest now includes [`XCTAssertIdentical(_:_:_:file:line:)`](https://developer.apple.com/documentation/xctest/3727243-xctassertidentical) and [`XCTAssertNotIdentical(_:_:_:file:line:)`](https://developer.apple.com/documentation/xctest/3727244-xctassertnotidentical) APIs to assert whether two object instances are identical (the same instance) and are stricter than [`XCTAssertEqual`](https://developer.apple.com/documentation/xctest/xctassertequal) by using the `===` operator instead of `==` in Swift. (46137782)

#### Resolved Issues

*   The `message` String parameter of `XCTSkip.init(_:file:line:)` no longer includes `@autoclosure` incorrectly. Unlike its conditional variants [`XCTSkipIf`](https://developer.apple.com/documentation/xctest/xctskipif) and [`XCTSkipUnless`](https://developer.apple.com/documentation/xctest/xctskipunless), XCTSkip’s initializer unconditionally evaluates its message string. (63827685)

*   If a test times out (due to having Test Timeouts enabled in the active Test Plan), any content that the test emitted to standard out or standard error prior to the timeout is now included in the test log. (64591225)

*   Xcode and xcodebuild now prevent the computer from sleeping while executing tests. (67493488)

*   If code under test crashes, and Xcode is able to collect a crash report, the error message that Xcode generates in the Test Report and Test Log includes the crashing symbol, as well as the Application Specific Information field from the crash report. (69755517)
