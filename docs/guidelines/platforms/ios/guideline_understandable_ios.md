 [🔼 Accessibility principles and examples](../../principles/accessibility_principles_and_examples.md  "Accessibility principles and examples") | [⬅️ Understandable principle](../../principles/understandable_principle.md "Understandable principle")

# Understandable guidelines for iOS

Information and the operation of the user interface must be understandable.

## [Readable (WCAG 3.1)](#wcag-31)

Make text content readable and understandable.

### [Language of Page (WCAG 3.1.1 -Level A)](#wcag-311)

The default human language of an App can be programmatically determined.

> This guideline covers point *3.1.1 Language of Page - Level A of the WCAG standard.*

#### ✅ Success technique(s)

Specify the default language of the application in the HTTP headers of the API calls.

```text
Content-Language: de-DE
or
Content-Language: en-US
or
Content-Language: de-DE, en-CA
etc.
```

This would allow for the app language to be changed dynamically by any back-end response, which would, for example, allow users from a certain location to get the app in their own language, even if they want to keep using their device in a different language. We should also provide an option for the user to choose this option in the in-app settings, or maybe even display a popup reminding them that the app uses a default language based on their location/region settings and that if they want to override this setting, they can do so in the in-app setting. Users should also be able to allow the app to follow the device settings for language preference.

#### 🚫 Failures

Hard-coding a language code inside an app should be avoided.

```swift
let language = "en"
UserDefaults.standard.set([language], forKey: "AppleLanguages")
Bundle.setLanguage(language)
```

Also, every app should be developed as a localizable app. Even if it seems that it makes no sense in the beginning or that all of the intended audience speak a single language, it can still happen that some users will not be able to use that language. here is always a possibility that your app will scale to different language regions or parts of your code will be reused on different projects which _do_ use localization.

### [Language of Parts (WCAG 3.1.2 - Level AA)](#wcag-312)

To be able to give the best possible experience to users, the language of each part of the app should be programmatically determined. With that in mind, VoiceOver should be able to read the content in the correct language.

> This guideline covers point *3.1.2 Language of Parts - Level AA of the WCAG standard.*

#### ✅ Success technique(s)

Due to need for VoiceOver to read the content in the correct language, the part of the content should get the correct language interpretation.

On iOS, this can be done by using `NSAttributedStrings` and setting the [speech attributes](https://developer.apple.com/documentation/objectivec/nsobject/uiaccessibility/speech_attributes_for_attributed_strings) for the specific part of the string.

```swift
let attributedString = NSAttributedString(
    string: "Arc de Triomphe",
    attributes: [.accessibilitySpeechLanguage: "fr-FR"]
)
```

If the whole text (label) is using the same language, the `accessibilityLanguage` property can be set in that case instead.

## [Predictable (WCAG 3.2)](#wcag-32)

Make mobile apps appear and operate in predictable ways.

### [On Focus & On Input (WCAG 3.2.1 and 3.2.2 - Level A)](#wcag-321-and-322)

Receiving focus on or interacting with any component should not initiate a change of context unless previously announced.

> This technique covers points *3.2.1 On Focus - Level A and 3.2.2 On Input - Level A of the WCAG standard.*

#### ✅ Success technique(s)

Users need to be able to consume content without any sudden interruptions or changes in context. Interacting with any UI component doesn't automatically cause a change of context unless the user has been previously advised of the behavior _before_ using the component.

Changes of focus and, thus, context should only ever be done intentionally and consciously.

```swift
textField.rightViewMode = .whileEditing
textField.rightView = someHelpButton

...

func someHelpButtonAction() {
    present(someInformativeViewController, animated: true)
}
```

#### 🚫 Failures

Showing programmatically pre-planned popups, modals, or any unusual navigation not directly initiated by the user is considered a change of context.

```swift
override func viewDidAppear(_ animated: Bool) {
    super.viewDidAppear(animated)
  
    viewAppearCount += 1
    if viewAppearCount > 3 {
        present(someInformativeViewController, animated: true)
    }
}
```

A form is submitted automatically when a certain UI element receives focus.

```swift
func textFieldShouldReturn(_ textField: UITextField) -> Bool {
    if textField == passwordTextField {
        performLogin()
    }
}
```

Focus is automatically moved to a different UI element when a given UI element receives focus.

```swift
func textFieldDidBeginEditing(_ textField: UITextField) {
    present(someInformativeViewController, animated: true)  
}
```

### [Consistent Navigation (WCAG 3.2.3 - Level AA)](#wcag-323)

For users is important to have a consistent navigation experience throughout the app. With that satisfied, users can easily predict where they are and where they can go next.

> This technique covers point *3.2.3 Consistent Navigation - Level AA of the WCAG standard.*

#### ✅ Success technique(s)

To satisfy this criterion, try to keep the navigation structure consistent, with elements like tab bar (and tab bar items), search bar or navigation bar always in the same place, and with the same functionality (when possible).

#### 🚫 Failures

Changing the position of elements or making the app behaviour unconsistent can confuse users and make it harder for them to navigate through the app, which results in failure to satisfy this criterion.

### [Consistent Identification (WCAG 3.2.4 - Level AA)](#wcag-324)

While using the application, components that have the same functionality should be identified consistently.

> This technique covers point *3.2.4 Consistent Identification - Level AA of the WCAG standard.*

#### ✅ Success technique(s)

To satisfy this criterion, try to keep the identification of the same components consistent throughout the application. Use properties like `accessibilityLabel` and `accessibilityHint` with other parts of implementation (traits or custom actions) to make sure they are defined and function in a same way.

To simplify this, try to think about a simple download icon, which should have the same accessibility label across the application (if possible). If elements are defined in a same way, users won't get confused and will know how to use the application and recognize its components.

#### 🚫 Failures

As a failure, we can consider components and elements that have different identification across the application. This can confuse users and make it harder for them to use the application.

## [Input Assistance (WCAG 3.3)](#wcag-33)

Help users avoid and correct mistakes when interacting with the app.

### [Error Identification (WCAG 3.3.1 - Level A)](#wcag-331)

If an input error is automatically detected, the item in error is identified, and the error is clearly described to the user in text.

> This technique covers point *3.3.1 Error Identification - Level A of the WCAG standard.*

#### ✅ Success technique(s)

If a form contains fields for which information from the user is mandatory the app should provide text descriptions to help identify those fields which are not sufficiently filled-out. The app should be able to validate and present a human-understandable error to the user even without needing to reach a remote endpoint.

```swift
let usernameTextField = UITextField()
usernameTextField.placeholder = "Username"
usernameTextField.accessibilityIdentifier = "username-text-field"
usernameTextField.accessibilityLabel = "Username text field"

let usernameErrorLabel = UILabel()
usernameErrorLabel.text = "Wrong username. Please enter a correct username and try again."
usernameErrorLabel.accessibilityLabel = "Username error indicator label"
```

Information provided by the user that is required to be in a specific format or contain certain values should be clearly communicated to the user, and the error messages must be even more descriptive, providing concrete information regarding the required format or the range of values an input needs to satisfy.

```swift
let passwordTextField = UITextField()
passwordTextField.placeholder = "Password"
passwordTextField.accessibilityIdentifier = "password-text-field"
passwordTextField.accessibilityLabel = "Password text field"
passwordTextField.accessibilityHint = "Enter a password which contains 8 characters, at least one number, and one of the special characters /\*!;@"
```

When data is successfully entered in such a form, on the other hand, some success feedback should be given to the user so that they know they've completed the action.

```swift
let generator = UINotificationFeedbackGenerator()
generator.prepare()
generator.notificationOccurred(.success)
```

#### 🚫 Failures

Preventing some action or flow from continuing because an error was detected but not communicating to the user how/when the error was made and/or what needed to be done to correct it.

### [Labels or Instructions (WCAG 3.3.2 - Level A)](#wcag-332)

Labels or instructions are provided when content requires user input.

> This technique covers point *3.3.2 Labels or Instructions - Level A of the WCAG standard.*

#### ✅ Success technique(s)

Descriptive labels should be applied to user interface elements, especially those the user is expected to interact with.

```swift
let usernameTextField = UITextField()
usernameTextField.placeholder = "Username"
```

Elements should be grouped into logical groups to help users distinguish between different parts of the user interface and switch between contexts quickly and easily.

```swift
let usernameHolderView = UIStackView()
let usernameTextField = UITextField()
let usernameErrorLabel = UILabel()
usernameHolderView.addArrangedSubviews = [usernameTextField, usernameErrorLabel]
usernameHolderView.shouldGroupAccessibilityChildren = true
```

#### 🚫 Failures

A user enters some data into a user interface element without knowing what the end result is and/or triggering an unannounced change of context in the process.

### [Error Suggestion (WCAG 3.3.3 - Level AA)](#wcag-333)

To provide the best user experience, the application should suggest solutions for input errors when they are detected.

> This technique covers point *3.3.3 Error Suggestion - Level AA of the WCAG standard.*

#### ✅ Success technique(s)

When an error is detected, the application should provide a suggestion for the user on how to correct it. This can be done by providing a hint or a description of the error, or providing a suggestion on how to correct it.

This is not just an accessibility feature, but also a usability feature, as it helps users to understand what they did wrong and how to correct it. Of course, if the suggestion is presented, this should be done in accessible way (e.g. using accessibility label).

*Note: This should be avoided if the error suggestion would jeopardize the security or purpose of the content.*

### [Error Prevention (Legal, Financial, Data) (WCAG 3.3.4 - Level AA)](#wcag-334)

To prevent users from making mistakes, the application should provide a mechanism before finalizing a transaction that involves legal, financial, or data-sensitive actions.

> This technique covers point *3.3.4 Error Prevention (Legal, Financial, Data) - Level AA of the WCAG standard.*

#### ✅ Success technique(s)

To satisfy this criterion, the app should provide at least one of the following mechanisms:

- **Reversible**: The submission is reversible.
- **Checked**: Data entered by the user is checked for input errors and the user is provided with an opportunity to correct them.
- **Confirmed**: A mechanism is available for reviewing, confirming, and correcting information before finalizing the submission.

Based on the type of the application, the mechanism should be implemented in a way that is most suitable for the user and the application's purpose.

### [Redundant Entry (WCAG 3.3.7 - Level A)](#wcag-337)

Ensure that multi-step processes are easy for users by not requesting the same information multiple times in a session, as this can be challenging for those with cognitive disabilities. This approach enhances accessibility by reducing memory load and simplifying tasks.

> This technique covers point *3.3.7 Redundant Entry - Level A of the WCAG standard.*

#### ✅ Success technique(s)

Information previously entered by or provided to the user that is required to be entered again in the same process is either:

- auto-populated, or
- available for the user to select.

Techniques mentioned above does not apply to the following cases:

- when re-entering the information is essential,
- when the information is required to ensure the security of the content, or
- when previously entered information is no longer valid.

### [Accessible Authentication (Minimum) (WCAG 3.3.8 - Level AA)](#wcag-338)

To make authentication accessible to all users, the application should not require a cognitive function test unless that step provides at least one of the following:

- **Alternative**: Another authentication method that does not rely on a cognitive function test.
- **Mechanism**: A mechanism is available to assist the user in completing the cognitive function test.
- **Object Recognition**: The cognitive function test is to recognize objects.
- **Personal Content**: The cognitive function test is to identify non-text content the user provided to the application.

> This technique covers point *3.3.8 Accessible Authentication (Minimum) - Level AA of the WCAG standard.*

#### ✅ Success technique(s)

Some of the success techniques to satisfy this criterion are:

- Support for text (copy and) paste to reduce the cognitive burden of re-typing
- Support for password entry by password managers
- Support for biometric authentication
- Support for email link authentication
- Support for OAuth authentication

#### 🚫 Failures

To fail this criterion, users should be required to complete a cognitive function test to authenticate themselves, or enter the values in a different way than they were originally created/provided.

Some examples:

- Write 2nd and 5th character of your password
- Write every character of the verification code in a separate field

## [Other understandable guidelines](#other-understandable-guidelines)

This section contains guidelines that may not applicable for the mobile (iOS) platform, or its criteria is a not the responsibility of the mobile team. Still, take into account that those guidelines needs to be satisfied.

- [WCAG 3.2.6 Consistent Help - Level A](https://www.w3.org/WAI/WCAG22/quickref/#consistent-help)

⎯

[← Understandable principle](../../principles/understandable_principle.md "Understandable principle")
