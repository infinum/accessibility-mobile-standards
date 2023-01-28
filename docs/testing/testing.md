# Testing accessibility features

When working with accessibility, it is important to have tools that will give you the ability to test current accessibility features.

Based on the currently available tools, we can define them as;

* Testing tools
* Verification tools

Testing tools are tools that can be used in standard testing like; UI testing. On the other hand, verification tools give us information about the current accessibility implementation status.

## Testing on iOS

On iOS, we can support both testing and verification tools. When talking about testing tools, we will cover tools that can be used as a part of UI testing; while talking about verification tools, we will cover tool which is a part of the Xcode to verify the current status of the application (or screen of the application).

### Testing tools

#### Testing with XCUI tests

To test the accessibility features of our application, UI tests need to be written. Apple didn’t provide a specific framework or tool to test accessibility features by default.

Still, with well-written UI tests, we can test some of the accessibility features like labels, touch area, element size, etc.

Most of those checks are not just accessibility-related, but they can give us information if we provide or create an interface as defined by design.

```swift
final class LoginAccessibilityTests: XCTest {

    let applicatioon = XCUIApplication()

    override func setUp() {
        // ... navigate to the login page
    }

    func testSubmitButton() {
        let submitButton = application.buttons["Submit"]

        XCTAssert(button.frame.size.height == 50)
        ...
    }
}
```

#### GTXiLib

To make XCUI tests a bit better, Google provides its framework, which can help get more information about the accessibility state of the particular screen.

They developed the framework called [GTXiLib](https://github.com/google/GTXiLib). GTXiLib provides many helper methods and feedback about current elements on the screen. Also, based on the accessibility status of the component, the test can fail.

Great thing about GTXiLib is that it will provide additional feedback if some component does not have an accessibility label, if the touch target size is too small, etc.

### Verification tools

#### Accessibility Inspector

While two previous tools were testing tools where some implementation was needed to get feedback about the accessibility state of the application, Accessibility Inspector does not require any implementation.

Accessibility Inspector is a tool already included in Xcode, and when used, it can inspect the currently active screen and components. We can get much information about accessibility implementation and other accessibility features like contrast, hit area, unsupported dynamic font size, and others.

Xcode inspector is available in the Xcode by _Xcode > Open Developer Tools... > Accessibility Inspector_.

## Additional notes

In this document, usage of component identifiers like `accessibilityIdentifier` or `resourceId` is not defined, because they are not used for accessibility features, but rather for automation testing.

⎯

[← Accessibility principles and examples](../guidelines/principles/accessibility_principles_and_examples.md "Accessibility principles and examples")
│
[Conclusion →](../general/conclusion.md "Conclusion")
