# iOS

## The fundamentals

This chapter will provide information about the accessibility components used for user interaction on the user interface. That includes the accessibility tree, accessibility element, its label, value, hint, and traits. After that, we will describe essential component properties for better accessibility usage and user experience.

### Accessibility tree

The accessibility tree represents a list of elements on the screen in a specific order. This order on iOS is from top left to bottom right. Every element in the accessibility tree contains information about itself - in this case, it is essential to have accessibility information about every element in that tree. Information used to describe accessibility elements is; label, value, hint, traits, and actions.

Try to think about the accessibility tree as a DOM used on the web to make this more descriptive.

### Accessibility element

As mentioned before, the essential thing when talking about accessibility is the accessibility tree. The accessibility tree creates its inner elements from elements defined as accessible elements. For example, Apple defined some UI elements accessible by default, like `UILabel`, `UITextField`, `UIProgressView`, and all subclasses of `UIControl`. Still, some elements like `UIView` are not accessible by default.

To define if an element on the UI is accessible, there is a property called `isAccessibilityElement` of type `Bool`. Still, when talking about SwiftUI, the method used for the same behavior is `accessibility(hidden:)`. The value can be changed via code or in the interface builder. 

When discussing custom accessibility elements, it is essential to check if they are accessible. Creating custom control can be done by subclassing `UIView` and `UIControl`. Still, the first one will not be accessible by default, while the second will. Both approaches have pros and cons, but try to test accessibility elements when creating custom components.

### Accessibility label

The Accessibility label represents the text that VoiceOver will read to the users. It is one of the most important components of the accessibility tree because it gives users the UI context. It is used to identify every component on the UI, but it does not need to provide the content of the component.

In most scenarios, the accessibility label will be read as the value of that element, e.g., the element’s text. Still, some components don’t have a value to provide, like buttons with an image only. In that case, values like “Start”, “Play” or “Delete” should be provided via the accessibility label. Also, in some cases, the label should give more information with an included default value, which can be done by changing the property.

To change the accessibility label of the element, there are different ways; change it via code with property `accessibilityLabel` or in SwiftUI as `accessibility(label:)`. Another way is changing the value in the interface builder.

### Accessibility value

The accessibility value represents the current value of the element. The value can represent a different state based on the component and even a different value type. E.g., text field accessibility value is value inside the text field (as a text), while a slider provides a value as a number.

The important thing here is to understand how to create custom components and define the accessibility value and its type for that component. Also, when talking about VoiceOver, it is important to know that VoiceOver reads the accessibility value after the accessibility label.
The value can be provided (or changed) via `accessibilityValue` property, in SwiftUI with modifier `accessibility(value:)` or via interface builder.

### Accessibility hint

The accessibility hint is the latest thing VoiceOver reads. It is used to describe or help users to use our app and interact with its components.
Based on the Apple recommendations, an excellent example of an accessibility hint would be; “Deletes your photo.” or “Adds a reaction to the message.”.

Still, there is one caveat, the accessibility hint can be disabled, and because of that, the recommendation is not to define essential information as an accessibility hint. With that in mind, try to think about accessibility hint as additional information when using the application.

Accessibility hint can be defined via property `accessibilityHint`, in SwiftUI with modifier `accessibility(hint:)` and via interface builder.

### Accessibility traits

Accessibility traits add additional information to UI elements and define how every element should be treated. That describes how every user can interact with every element on the UI when using accessibility features.

For example, creating a custom component that should work as a slider could use the `adjustable` accessibility trait with increment and decrement functionality.

Apple did a fantastic job with this, and every `UIView` element supports `UIAccessibilityTraits`. There is a lot of accessibility traits that are supported by iOS, and at this moment, those are:

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

Each of those traits has its functionality. To understand them a bit more, you can check this [link](https://developer.apple.com/documentation/uikit/uiaccessibility/uiaccessibilitytraits).

## Accessibility features on iOS

When talking about the accessibility on iOS devices, Apple defined four main categories to satisfy the accessibility needs of their users. Those categories are:

* Cognitive
* Motor
* Vision
* Hearing

The main idea is to create assistive technologies to help users with disabilities use our apps with our support and accessibility implementation. This chapter will cover some of the most important accessibility features available on iOS devices and give information about using them in iOS applications.

### Dynamic Type (Larger Text)

// TODO

### Differentiate Without Color

// TODO

### Button Shapes

// TODO

### Reduce Transparency

// TODO

### Reduce Motion

// TODO

### VoiceOver

// TODO

### Switch Control

// TODO

### Voice Control

// TODO

### Assistive Touch

// TODO

### Guided Access

// TODO

### Captioning

// TODO
