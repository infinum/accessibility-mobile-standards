 [🔼 Accessibility principles and examples](../../principles/accessibility_principles_and_examples.md  "Accessibility principles and examples") | [⬅️ Understandable principle](../../principles/understandable_principle.md "Understandable principle")

# Understandable guidelines for Flutter

## Readable

Make text content readable and understandable.

### Language of Page

The default human language of an App can be programmatically determined.

*This guideline covers point 3.1.1 Language of Page - Level A of the WCAG standard.*
#### ✅ Success technique(s)

If the app supports multiple languages, we should also care that accessibility labels are localized as well.

You should use `LocalizationsDelegate` in the MaterialApp and all labels in the widget should use the delegate instead of being hardcoded. Same rule applies to labels inside `Semantics` widgets.

If the label is not known at the runtime, e.g. if it's coming from HTTP request, then response of that request should be localized in a way where app sends the language as a header:
```
Accept-Language: de-DE
```

and the labels are returned localized in selected language so they can be shown to the user.

#### 🚫 Failures

Hard-coding a language code and labels inside an app should be avoided.

Also, every app should be developed as a localizable app, even if it seems like it makes no sense at the start, or all of the intended audience speak a single language, it can still happen that some users will not be able to use that language and there is always a possibility that your app will scale to different language regions or that parts of your code will be reused on different projects which _do_ use localization.

## Predictable

Make mobile apps appear and operate in predictable ways.

### On Focus & On Input

*This technique covers points 3.2.1 On Focus - Level A & 3.2.2 On Input - Level A of the WCAG standard.*
#### ✅ Success technique(s)

Users need to be able to consume content without any sudden interruptions and/or changes of context. Receiving focus on or interacting with any component should not initiate a change of context unless previously announced. By change of context we mean major changes in the content of the screen.

Interacting with any UI component doesn't automatically cause a change of context unless the user has been previously advised of the behavior _before_ using the component.

Changes of focus and thus context should only ever be done intentionally and consciously.

#### 🚫 Failures

Showing programmatically pre-planned popups, modals, or any unusual navigation not directly initiated by the user is considered a change of context.

```dart

  void onUserEnteredScreen() {
    await Future(() {}, duration: Duration(seconds: 10));
    showAdDialog();
  }
```

- A form is submitted automatically when a certain UI element receives focus.
- Focus is automatically moved to a different UI element when a give UI receives focus.

## Input Assistance

Help users avoid and correct mistakes when interacting with the app.

### Error Identification

If an input error is automatically detected, the item that is in error is identified and the error is clearly described to the user in text.


*This technique covers point 3.3.1 Error Identification - Level A of the WCAG standard.*

#### ✅ Success technique(s)

If a form contains fields for which information from the user is mandatory the app should provide text descriptions to help identify those fields which are not sufficiently filled-out. The app should be able to validate and present a human-understandable error to the user even without needing to reach a remote endpoint.

```dart
TextField(
    errorText: hasError ? errorLabel : null
)
// or
TextFormField(
    validator: (value) {
        if (value.length < 4) {
            return AppString.shortName;
        }
        return null;
    },
)
```

#### 🚫 Failures

Preventing some action or flow from continuing because an error was detected but not communicating to the user how/when the error was made and/or what needs to be done to correct it.

### Labels or Instructions

Labels or instructions are provided when content requires user input.

*This technique covers point 3.3.2 Labels or Instructions - Level A of the WCAG standard.*

#### ✅ Success technique(s)

Descriptive labels should be applied to user interface elements, especially those that the user is expected to interact with.

```dart
TextField(
    decoration: InputDecoration(hintText: 'Username'),
)
```

It's a good practice that fields that expect entering input in some format, contains initial text which indicates the correct format. For example:

```dart
Column(children: [
    Text('Enter code:'),
    TextField(
        decoration: InputDecoration(hintText: 'ABC-445'),
    ),
])
```
#### 🚫 Failures

User enters some data into a user interface element without knowing what the end result is and/or triggering an unannounced change of context in the process.

⎯

[← Understandable principle](../../principles/understandable_principle.md "Understandable principle")
