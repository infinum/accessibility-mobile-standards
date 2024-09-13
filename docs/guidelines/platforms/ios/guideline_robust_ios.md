 [🔼 Accessibility principles and examples](../../principles/accessibility_principles_and_examples.md  "Accessibility principles and examples") | [⬅️  Robust principle](../../principles/robust_principle.md "Robust principle")

# Robust guidelines for iOS

Content must be robust enough that it can be interpreted by a wide variety of mobile devices, including those which use accessibility features.

## [Compatible (WCAG 4.1)](#wcag-41)

Maximize compatibility with current and future devices, taking into account the accessibility features that they might be using.

### [Name, Role, Value (WCAG 4.1.2 - Level A)](#wcag-412)

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

⎯

[← Robust principle](../../principles/robust_principle.md "Robust principle")
