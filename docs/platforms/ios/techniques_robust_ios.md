# [Robust principle](../../principles/robust_principle.md#robust-principle)

## [Compatible (WCAG 4.1)](../../principles/robust_principle.md#compatible-wcag-41)

### [Name, Role, Value (WCAG 4.1.2 - Level A)](../../principles/robust_principle.md#name-role-value-wcag-412---level-a)

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

### [Status messages (WCAG 4.1.3 - Level AA)](../../principles/robust_principle.md#status-messages-wcag-413---level-aa)

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
