[⬅️ Features per mobile platform](../features_per_mobile_platform.md)

# Accessibility features on iOS

## The fundamentals

This chapter will provide information about the accessibility components used for user interaction on the user interface. That includes the accessibility tree, accessibility element, its label, value, hint, and traits. After that, we will describe essential component properties for better accessibility usage and user experience.

### Accessibility tree

The accessibility tree represents a list of elements on the screen in a specific order. This order on iOS is from the top left to the bottom right. Every element in the accessibility tree contains information about itself – in this case, it is essential to have accessibility information about every element in that tree. Information used to describe accessibility elements is; label, value, hint, traits, and actions.

Try to think about the accessibility tree as a DOM used on the web to make this more descriptive.

### Accessibility element

As mentioned before, the essential thing when talking about accessibility is the accessibility tree. The accessibility tree creates its inner elements from those defined as accessible elements. For example, Apple defined some UI elements accessible by default, like `UILabel`, `UITextField`, `UIProgressView`, and all subclasses of `UIControl`. Still, some elements like `UIView` are not accessible by default.

To define if an element on the UI is accessible, there is a property called `isAccessibilityElement` of type `Bool`. Still, when talking about SwiftUI, the method used for the same behavior is `accessibility(hidden:)`. The value can be changed via code or in the interface builder.

When discussing custom accessibility elements, it is essential to check if they are accessible. Custom control can be created by subclassing `UIView` and `UIControl`. Still, the first one will not be accessible by default; the second will. Both approaches have pros and cons, but try to test accessibility elements when creating custom components.

### Accessibility label

The Accessibility label represents the text that VoiceOver will read to the users. It is one of the most important components of the accessibility tree because it gives users the UI context. It is used to identify every component on the UI, but it does not need to provide the content of the component.

In most scenarios, the accessibility label will be read as the value of that element, e.g., the element’s text. Still, some components don’t have a value to provide, like buttons with an image only. In that case, values like “Start”, “Play,” or “Delete” should be provided via the accessibility label. Also, in some cases, the label should give more information with an included default value, which can be done by changing the property.

There are different ways of changing the accessibility label of the element; via code with property `accessibilityLabel` or in SwiftUI as `accessibility(label:)`. Another way is changing the value in the interface builder.

```swift
// UIKit
editButton.accessibilityLabel = "Edit"

// SwiftUI
Button("Edit") { ... }
    .accessibility(label: "Edit")
```

### Accessibility value

The accessibility value represents the current value of the element. The value can represent a different state based on the component and even a different value type. E.g., the text field accessibility value is a value inside the text field (as a text), while a slider provides a value as a number.

The important thing here is understanding how to create custom components and define the accessibility value and its type for that component. Also, when talking about VoiceOver, it is important to know that VoiceOver reads the accessibility value after the accessibility label.
The value can be provided (or changed) via the`accessibilityValue` property in SwiftUI with modifier `accessibility(value:)` or via interface builder.

```swift
// UIKit
firstDepositButton.accessibilityValue = "10"

// SwiftUI
Button("First deposit") { ... }
    .accessibility(value: "10")
```

### Accessibility hint

The accessibility hint is the latest thing VoiceOver reads. It is used to describe or help users to use our app and interact with its components.
Based on the Apple recommendations, an excellent example of an accessibility hint would be; “Deletes your photo.” or “Adds a reaction to the message.”.

Still, there is one caveat, the accessibility hint can be disabled, and because of that, the recommendation is not to define essential information as an accessibility hint. With that in mind, try to think about accessibility hints as additional information when using the application.

Accessibility hint can be defined via property `accessibilityHint`, in SwiftUI with modifier `accessibility(hint:)` and via interface builder.

```swift
// UIKit
playButton.accessibilityHint = "Plays selected song."

// SwiftUI
Button("Play") { ... }
    .accessibility(hint: "Plays selected song.")
```

### Accessibility traits

Accessibility traits add additional information to UI elements and define how every element should be treated. That describes how every user can interact with every element on the UI when using accessibility features.

For example, creating a custom component that should work as a slider could use the `adjustable` accessibility trait with increment and decrement functionality.

Apple did a fantastic job with this; every `UIView` element supports `UIAccessibilityTraits`. Many accessibility traits are supported by iOS, and at this moment, those are:

* Button
* Image
* Link
* Header
* Selected
* Static text
* Search field
* Play sound
* Keyboard key
* Summary element
* User interaction enabled
* Updates frequently
* Starts media session
* Adjustable
* Allows direct interaction
* Causes page turn

Each of those traits has its functionality. You can check this [link](https://developer.apple.com/documentation/uikit/uiaccessibility/uiaccessibilitytraits) for more information.

## Accessibility features on iOS

When talking about accessibility on iOS devices, Apple defined four main categories to satisfy the accessibility needs of their users. Those categories are:

* Cognitive
* Motor
* Vision
* Hearing

The main idea is to create assistive technologies to help users with disabilities use our apps with support and accessibility implementation. This chapter will cover some of the most important accessibility features available on iOS devices and give information about using them in iOS applications.

### Voice Control

VoiceOver is a built-in screen reader that works on the iOS platform. It is not just a screen reader per se but is also used for navigation inside the application or the whole iOS system.

VoiceOver changes how users interact with the application, where the most used operation will be a swipe-navigation operation.

Understanding how VoiceOver goes through the accessibility tree and which data is read to the user is important. The order of reading data for every accessibility element goes in the following order: **Accessibility label** > **Accessibility value** > **Accessibility traits** > **Accessibility hint**. It is important to configure UI components to have the required values so the user can easily navigate and use our app.

To get the information if the VoiceOver is used, there is a property `UIAccessibility.isVoiceOverRunning`, which returns a `Bool` value. If there is a need to get the information dynamically, a notification can be used; `UIAccessibility.voiceOverStatusDidChangeNotification`.

One of the essential things when talking about VoiceOver is to understand that most people that use VoiceOver have visibility issues. For that reason, the app should notify the user when something is changed on the screen or layout. Such alterations should be called should be called `UIAccessibility.Notification.screenChanged` for more significant changes (e.g., screen change) or `UIAccessibility.Notification.layoutChanged` for more minor changes on the screen (e.g., component change).

Also, when talking about notifications and changes for the user, another important thing is changes or app features like modals. Users should be aware of that, and in this case `UIAccessibility.Notification.announcement` should be used.

There are other notifications that improve users’ experience while using VoiceOver. Find more about them [here](https://developer.apple.com/documentation/uikit/uiaccessibility/notification).

As mentioned before, an important thing about VoiceOver is navigation. With correctly defined navigation, a user can navigate through our app and use all features as a user without disabilities.

Still, some features may not be easy to use, such as long lists with different types of data or different components with inner components. But, to make that a bit easier, there is a functionality called the rotor. The rotor defines how users can go through the different types of data (or components) without going through all of them. By implementing a custom rotor, users get the ability to use and navigate the apps easier and faster (when applicable).

### Dynamic Type (Larger Text)

The dynamic type, commonly known as larger text, is an accessibility feature that allows users to change the font size used across the operating system and applications. Users can change the size to smaller or bigger font and use extra large fonts on the provided scale in the iOS settings.

If the font is used as `UIFontTextStyle`, this functionality is supported by default, and changes its appearance immediately after the change is made in the iOS settings.

Still, many applications use custom fonts, but iOS supports custom styles that support the dynamic type.
To do that, `UIFontMetrics` should be used for the custom font, which provides data for scaling the font.

```swift
let font = UIFont(name: "SomeCustomFont", size: someDefaultSize)
let fontMetrics = UIFontMetrics(forTextStyle: .body)

someLabel.font = fontMetrics.scaledFont(for: font)
someLabel.adjustFontForContentSizeCategory = true
```

_Note: Recommendation is to use the `.body` style for defining the scaled font._

### Differentiate Without Color

This feature is compelling because people with color blindness may find it challenging to read the screen where color does define the context (e.g., bank account status where green color text represents positive and red color text negative status of the account).

To distinguish the context, which is only defined by the color, when this feature is enabled, the appearance of the components should be changed. E.g., if the bank account is negative, it should have a minus sign in front. The appearance can be only textual, but it can also include other elements like views, images, buttons, etc.

To be able to get the status of this feature, use `UIAccessibility.shouldDifferentiateWithoutColor` or observe the change via `UINotification.shouldDifferentiateWithoutColorDidChangeNotification`.

### Reduce Transparency

This is an important feature of iOS, which helps people with vision disabilities. Mostly, this is a design concern, but it is important to understand that iOS provides a tool that can dynamically change the transparency of the components when needed.

Sometimes, blurry components can be challenging to see or use by people with vision disabilities. Reducing that and adding a different component appearance (e.g., different background color) can make the app much easier to use.

The status of this property can be read by using `UIAccessibility.isReduceTransparencyEnabled` or via notification `UIAccessibility.reduceTransparencyStatusDidChange`.

### Reduce Motion

There are many people affected by the motion, and some motions can trigger things like dizziness. Because of that, iOS provides this functionality where users can reduce the motion of the applications.

This is supported by default on all system-defined animations (e.g., present, push, etc.). Still, when working with custom animations, the user's choice will not be considered.

Because of that, it is important to check `UIAccessibility.isReduceMotionEnabled` before using custom animations. The same value can be read via notification `UIAccessibility.reduceMotionStatusDidChangeNotification`.

### Switch Control

Switch control is a powerful tool for people with extreme motor disabilities (like issues with touching/tapping the screen).
This feature works similarly to VoiceOver but does not go through all elements.

The main idea is to navigate through interactive elements – like buttons. And when on that element, the user can select different actions from the context menu (like tap or scroll). With this implementation, users with motor disabilities can use the app with one single gesture.

Some apps are more interactive, and some aren't, but there should be custom actions available for switch control for some of them. This can also be done, so users can use our app in a smaller number of interactions, which benefits users with motor disabilities.

The state of this feature can be checked via `UIAccessibility.isSwitchControlRunning` or via notification `UIAccessibility.switchControlStatusDidChangeNotificatication`.

⎯

[← Features per mobile platform](../features_per_mobile_platform.md)
