 [🔼 Accessibility principles and examples](accessibility_principles_and_examples.md "Accessibility principles and examples") | [⬅️  Robust principle](../../principles/robust_principle.md "Robust principle")

# Robust guidelines for iOS

Content must be robust enough that it can be interpreted by a wide variety of mobile devices including those which use accessibility features.

## Compatible

Maximize compatibility with current and future devices, taking into account the accessibility features that they might be using.

### Parsing

All user-visible content be grouped logically and assigned identifiers appropriately.

*This guideline covers point 4.1.1 Parsing - Level A of the WCAG standard.*

#### ✅ Success technique(s)

##### Using accessibility identifiers

Every user interface element should have a unique [accessibility identifier](https://developer.apple.com/documentation/uikit/uiaccessibilityidentification/1623132-accessibilityidentifier) which will define it. Identifiers should not be reused, except where this is by design (i.e. the same exact element exists in several different locations). This property is not actually part of the accessibility context, but is rather used to differentiate between objects programmatically.

```swift
submitFormButton.accessibilityIdentifier = "submit-form-button"
```

For iterative elements, such as lists and tables there are two approaches: if the elements don't need to be distinguishable from each other for UI testing purposes (or some other explicit need) then using a single accessibility identifier for all elements is acceptable, otherwise the identifier could be suffixed with an index or more concrete information regarding it's meaning.

```swift
func tableView(
    _ tableView: UITableView,
    cellForRowAt indexPath: IndexPath
) -> UITableViewCell {
    let cell = tableView.dequeueReusableCell(withIdentifier: identifier)
    ...

    cell.accesibilityIdentifier = "login-form-cell"

    // or

    cell.accesibilityIdentifier = "login-form-cell-\(indexPath.row)"
    
    ... 
    return cell
}
```

#### 🚫 Failures

Duplicate identifiers used for elements which are essentially different in their action or role.

Elements are not grouped or are badly organized on the screen which prevents accessibility features from quickly and efficiently moving through them.

### Name, Role, Value

User interface elements should be clearly defined by their name ([accessibility label](https://developer.apple.com/documentation/objectivec/nsobject/1615181-accessibilitylabel) & [accessibility hint](https://developer.apple.com/documentation/objectivec/nsobject/1615093-accessibilityhint)), the role that they have (accessibility identifier), and the value they carry([accesibility value](https://developer.apple.com/documentation/objectivec/nsobject/1615117-accessibilityvalue)). The app should be able to notify the user if any of these parameters change programmatically without user input (or the changes should be reflected in the element's accessibility attributes), so that the user remains aware of what this element does at all times.

*This guideline covers point 4.1.2 Name, Role, Value - Level A of the WCAG standard.*

#### ✅ Success technique(s)

Every user interface element should have a unique accessibility label which can be used by VoiceOver.

```swift
addButton.accessibilityLabel = "Add"
addButton.accessibilityHint = "Adds an entry in the list"
```

For elements which carry a value, such as a label, the accessibility value should be used to represent this value. If the accessibility value is not set then the actual value (in this case, the text value) will be read.

```swift
titleLabel.text = "Entries"
titleLabel.accessibilityValue = "Entries list"
```

#### 🚫 Failures

Not providing accessibility identifiers for user interface elements.

Implementing custom controls which are unfamiliar to the users and don't carry the necessary accessibility identifying information as defined in this guideline.

Changing the value or role of a user interface element without adjusting it's identifier programmatically.

⎯

[← Robust principle](../../principles/robust_principle.md "Robust principle")
