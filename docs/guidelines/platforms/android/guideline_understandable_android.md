 [🔼 Accessibility principles and examples](../../principles/accessibility_principles_and_examples.md  "Accessibility principles and examples") | [⬅️ Understandable principle](../../principles/understandable_principle.md "Understandable principle")

# Understandable guidelines for Android

## Readable

Make text content readable and understandable.

### Language of the App

*This guideline covers point 3.1.1 Language of Page - Level A of the WCAG standard.*

:white_check_mark: **Success criteria**

The app should be implemented to reach the largest number of users. It should handle text, audio files, numbers, currency, and graphics in ways appropriate to the locales where it is used. It should provide a text alternative, at least in English, if it already isn't the default language of the app.

It is recommended that all text content used in the application, including `contentDescription`, is implemented using the Android resource framework.

It is also important to support localization because of accessibility services. Even though TalkBack supports [various languages](https://support.google.com/accessibility/android/answer/11101402?hl=en), not all of them are supported on every Android version.

**Server-driven application**

If the application is server-driven and most of the content depends on the backend output, it is important to create logic where the app will send the information about the current locale at launch. In that scenario, the backend should return the content in the corresponding language based on the received information about the current locale.

:no_entry_sign: **Failure criteria**

- The default language of the app is hardcoded, and it is impossible to change it.

---

## Predictable

Make mobile apps appear and operate in predictable ways.

### On Focus & On Input (WCAG 3.2.1 and 3.2.2 - Level A)

Receiving focus on or interacting with any component should not initiate a change of context unless previously announced.

✅ **Success criteria**

Users need to be able to consume content without any sudden interruptions or changes in context. Interacting with any UI component doesn't automatically cause a change of context unless the user has been previously advised of the behavior _before_ using the component.

Changes of focus and, thus, context should only ever be done intentionally and consciously.

Whenever adding a custom callback to a focus or input change event, think about whether the action that will be executed can be considered a change of context and, if so, could the user have expected it before initiating focus/input change.

Here are some examples of focus/input callbacks that would be acceptable with respect to this criteria:
- An app for online shopping includes a form with payment and delivery information. Below payment information, there is a radio button group with options "Delivery address is the same as the payment information" and "I want products delivered to another address". If the user selects the latter option, a new input field for the delivery address appears. This is not considered a change of context, because only some parts of the screen changed, but the overall structure remained the same.
- A theme settings screen has three radio buttons (light/dark/system) and instructions to the user that the theme will be changed immediately upon selecting an option. There is no "Submit" button and the action is executed upon input, but the user is clearly instructed on what to expect. 
- In an input field, a trailing action appears when the input field gets focus. For example, in a password input field, a button for toggling password visibility appears when the field gets focus. This is considered acceptable, as the user is just presented with additional actions and the overall context did not change at all.
- In an input field, a trailing action for clearing the entire input appears when the user enters something into the field.


🚫 **Failure examples**

Some examples of actions that _are_ considered a change of context and would violate the criteria are:
- Automatically submitting a form when a certain field gets focus or input. For example, in a login form, the user is automatically logged in when checking the "Remember me" checkbox, without pressing the "Log in" button.
- Showing an alert dialogs when an element receives focus. For example, an input field receives focus and a help alert dialog describing a field appears. The user would first have to close the dialog before continuing with input, and the dialog would appear any time the user might want to edit their input.

---

## Input Assistance (WCAG 3.3)

Help users avoid and correct mistakes.

### Error identification

*This technique covers point 3.3.1 Error Identification - Level A of the WCAG standard.*

:white_check_mark: **Success criteria**

If an error occurs on the item the user is interacting with, the error should be clearly defined and described so the user can get clear information on why the error occurred and what to do in order to fix it.

It is recommended to always use or extend system-provided widgets that are as far down Android's class hierarchy as possible because they already have the most accessibility capabilities that your app needs.

On the other hand, if your app requires the implementation of custom components, you will need to implement [custom accessibility events](https://developer.android.com/guide/topics/ui/accessibility/principles#define-custom-events) to provide all accessibility updates that the system-provided widgets do.

:no_entry_sign: **Failure criteria**

- Error messages do not exist or are not descriptive enough.

- Custom components do not support custom error handling.

---

### Labels or instruction

*This technique covers point 3.3.2 Labels or Instructions - Level A of the WCAG standard.*

:white_check_mark: **Success criteria**

When the user focuses on an input view (for example, in the form or login screen) through an accessibility service, it is important to give them enough information about the type of input they are expected to provide.

- Pairs of elements where one describes the other

It is common that a given EditText has a corresponding View that describes the content that the user should input within the EditText element. This relationship between elements could be achieved by setting `android:labelFor` attribute on that specific View.

That way, services such as TalkBack will read defined relationships to the user, giving them more context about the expected input when EditText is in focus.

**Code example:**

```
<!-- Label text for en-US locale would be "Username:" -->
<TextView
   android:id="@+id/usernameLabel" ...
   android:text="@string/username"
   android:labelFor="@+id/usernameEntry" />

<EditText
   android:id="@+id/usernameEntry" ... />
```

In the given example, services such as TalkBack will read – "EditBox for username" when the user sets focus to EditText.

:no_entry_sign: **Failure criteria**

- Not providing enough context for the views that expect user interaction.

---

### Accessible Authentication (Minimum) (WCAG 3.3.8 - Level AA)

This guideline covers point [3.3.8 Accessible Authentication (Minimum) - Level AA](https://www.w3.org/WAI/WCAG22/quickref/#accessible-authentication-minimum) of the WCAG standard.

To make authentication accessible to all users, the application should not require a cognitive function (such as remembering a password or solving a puzzle) test unless that step provides at least one of the following:

- **Alternative**: Another authentication method that does not rely on a cognitive function test.
- **Mechanism**: A mechanism is available to assist the user in completing the cognitive function test.
- **Object Recognition**: The cognitive function test is to recognize objects.
- **Personal Content**: The cognitive function test is to identify non-text content the user provided to the application.

:white_check_mark: **Success criteria**

- Support for text (copy and) paste to reduce the cognitive burden of re-typing
- Support for password entry by password managers or passkeys (i.e [Google passkey](https://developers.google.com/identity/passkeys))
- Support for biometric authentication
- Support for email link authentication
- Support for OAuth authentication

:no_entry_sign: **Failure criteria**

To fail this criterion, users should be required to complete a cognitive function test to authenticate themselves or enter the values in a different way than they were originally created/provided.

Some examples:

- Write 2nd and 5th character of your password
- Write every character of the verification code in a separate field

#### Sources

- [Google Support Page](https://support.google.com/accessibility/android)
- [Official Documentation](https://developer.android.com/guide/topics/ui/accessibility)

---

[← Understandable principle](../../principles/understandable_principle.md "Understandable principle")
