 [🔼 Accessibility principles and examples](accessibility_principles_and_examples.md "Accessibility principles and examples") | [⬅️  Robust principle](../../principles/robust_principle.md "Robust principle")

# Robust guidelines for Flutter

## Compatible

### Name, Role, Value

*This guideline covers point 4.1.2 Name, Role, Value - Level A of the WCAG standard.*

#### ✅ Success technique(s)

UI components, like form elements, can have beside accessibility label their role and value. If you are using standard widgets
from Flutter framework these roles and values will be handled for you.

If you are building something custom, like painting your own RenderObject, then you need to be aware of it.

Some examples are:

- Is the widget a text field:
```dart
Semantics(label: 'Add', hint: 'Adds an entry in the list',  ...)
```

- Is the widget a text field:
```dart
Semantics(textField: true, ...)
```

- Is the widget is obscured text field:
```dart
Semantics(textField: true, obscured: true, ...)
```

- Is the widget a checkbox, pass the value:
```dart
Semantics(checked: true or false, ...)
```

- Mixed state, Half-checked or tri-state checkbox:
```dart
Semantics(mixed: true, ...)
```

- Widget can be selected
```dart
Semantics(selected: true or false, ...)
```

- Is the widget a slider control:
```dart
Semantics(slider: true, ...)
```

And several other fields.


#### 🚫 Failures

Implementing custom controls which are unfamiliar to the users and don't carry the necessary accessibility identifying information as defined in this guideline.

Changing the value or role of a user interface element without adjusting it's identifier programmatically.

⎯

[← Robust principle](../../principles/robust_principle.md "Robust principle")
