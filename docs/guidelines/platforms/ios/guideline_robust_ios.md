 [🔼 Accessibility principles and examples](../../principles/accessibility_principles_and_examples.md  "Accessibility principles and examples") | [⬅️  Robust principle](../../principles/robust_principle.md "Robust principle")

# Robust guidelines for iOS

Content must be robust enough that it can be interpreted by a wide variety of mobile devices, including those which use accessibility features.

[](#wcag-41)

## Compatible (WCAG 4.1)

Maximize compatibility with current and future devices, taking into account the accessibility features that they might be using.

[](#wcag-412)

### Name, Role, Value (WCAG 4.1.2 - Level A)

User interface elements should be clearly defined by their name ([accessibility label](https://developer.apple.com/documentation/objectivec/nsobject/1615181-accessibilitylabel) & [accessibility hint](https://developer.apple.com/documentation/objectivec/nsobject/1615093-accessibilityhint)), the role that they have (accessibility identifier), and the value they carry([accesibility value](https://developer.apple.com/documentation/objectivec/nsobject/1615117-accessibilityvalue)). The app should be able to notify the user if any of these parameters change programmatically without user input (or the changes should be reflected in the element's accessibility attributes) so that the user remains aware of what this element does at all times.

> This guideline covers point *4.1.2 Name, Role, Value - Level A of the WCAG standard.*

#### ✅ Success technique(s)

Every user interface element should have an accessibility label that can be used by VoiceOver.

```swift
addButton.accessibilityLabel = "Add"
addButton.accessibilityHint = "Adds an entry in the list"
```

For elements that carry a value, such as a label, the accessibility value should be used to represent this value. If the accessibility value is not set, then the actual value (in this case, the text value) will be read.

```swift
titleLabel.text = "Entries"
titleLabel.accessibilityValue = "Entries list"
```

#### 🚫 Failures

Not providing accessibility identifiers for user interface elements.

Implementing custom controls that are unfamiliar to the users and don't carry the necessary accessibility identifying information as defined in this guideline.

Changing the value or role of a user interface element without adjusting its identifier programmatically.

[](#wcag-413)

### Status messages (WCAG 4.1.3 - Level AA)

The guideline states that status messages should be programmatically determinable by the user. 
This means that the user should be able to know the status of the app at any given time without having to interact with it.

On mobile this means that the user should be able to know if the current state has been changed - which is especially important for users who rely on screen readers.

> This guideline covers point *4.1.3 Status messages - Level AA of the WCAG standard.*

#### ✅ Success technique(s)

To satisfy this guideline, the app should provide a way for the user to know the current status of the app at any given time. This can be in situations like;

- search results are being loaded,
- cooking time has changes,
- items has been added to the cart,
- etc.

Based on changes like that, the `UIAccessibility.Notification` can be used to notify the user of the change.

```swift
UIAccessibility.post(notification: .announcement, argument: "5 results found.")
```

For more information about examples and success criteria, please refer to the [Understanding WCAG 4.1.3 - Status messages](https://www.w3.org/WAI/WCAG21/Understanding/status-messages) page.

#### 🚫 Failures

Not providing a way for the user to know the current status of the application at any given time.

⎯

[← Robust principle](../../principles/robust_principle.md "Robust principle")
