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

## Predictable (WCAG 3.2)

Make mobile apps appear and operate in predictable ways.

*This technique covers points 3.2.1 On Focus - Level A & 3.2.2 On Input - Level A of the WCAG standard.*

### On Focus & On Input

:white_check_mark: **Success criteria**

The user should be able to navigate through the app without constant context switching. Also, interacting with the view should not cause a change of context. If view interaction changes the context, that should be signalized to the user **before** the interaction.

If the content displayed on the screen is designed and implemented following [Perceivable guidelines](https://github.com/infinum/accessibility-mobile-standards/blob/master/docs/guidelines/platforms/android/guideline_percievable_android.md), these requirements should be met by default.

:no_entry_sign: **Failure criteria**

- The content is not grouped based on context relationships and has no meaningful labels defined.

### Consistent Identification (WCAG 3.2.4 - Level AA)

While using the application, components that have the same functionality should be identified consistently.

> This technique covers point *3.2.4 Consistent Identification - Level AA of the WCAG standard.*

#### ✅ Success technique(s)

To satisfy this criterion, try to keep the identification of the same components consistent throughout the application. Use properties like `contentDescription` and `AccessibilityAction` with other parts of implementation to make sure they are defined and function in a same way.

Example 1: Consider a search icon that consistently uses the same accessibility label throughout the application. By standardising the label, users can easily recognise and understand its function, reducing confusion and enhancing usability.

Example 2: Identification should be consistent but not identical. For instance, an arrow that links to the next page can have the label "Go to page 4" on one page and "Go to page 5" on the next. While the labels differ, they maintain consistency in function.

Example 3: While a search icon benefits from having a consistent label, a check mark can mean different things like "approved," "completed," or "included," depending on where it is used. This means it needs different labels based on the context.

#### 🚫 Failures

- As a failure, we can consider components and elements that have different identification across the application. This can confuse users and make it harder for them to use the application.

Note: Certain elements may require context-specific labels to convey their functions accurately, balancing consistency with clarity to enhance user understanding

---

## Input Assistance (WCAG 3.3)

Help users avoid and correct mistakes.

### Error identification (WCAG 3.3.1 - Level A)

If an input error is automatically detected, the item that is in error is identified and the error is described to the user in text.

> This technique covers point *3.3.1 Error Identification - Level A of the WCAG standard.*

#### ✅ Success technique(s)

If an error occurs on the item the user is interacting with, the error should be clearly defined and described so the user can get clear information on why the error occurred and what to do in order to fix it.

It is recommended to always use or extend system-provided widgets that are as far down Android's class hierarchy as possible because they already have the most accessibility capabilities that your app needs.

On the other hand, if your app requires the implementation of custom components, you will need to implement [custom accessibility events](https://developer.android.com/guide/topics/ui/accessibility/principles#define-custom-events) to provide all accessibility updates that the system-provided widgets do.

For Views, `TextView` can be used to display error message. `TextInputLayout` can also be used, as it has built-in support for error messages.

Example - showing error on `TextInputLayout`:

```
// Error message for en-US locale would be "Invalid date, must be in the form DD/MM/YYYY, for example, 01/01/1990"
 textInputLayout.error = getString(R.string.date_error)
 textInputLayout.setErrorEnabled(true)
```

For Compose, an `error` semantics property can be used. However, this will only announce the error message, but it won't be shown on the screen.
`TextField` can be used to display the error message. Its `label` parameter can be used to provide the message, and by combining it with `isError`, the `TextField`
 will change its appearance to indicate an error.

Example - showing error on `TextField`:

```
// Error message for en-US locale would be "Invalid date, must be in the form DD/MM/YYYY, for example, 01/01/1990"
TextField(
    value = "",
    label = {
        Text(errorMessage.ifEmpty { "TextField label" })
    },
    isError = isError,
    onValueChange = { /* State update logic */ },
    modifier = Modifier
        .semantics {
            if (errorMessage.isNotEmpty()) {
                error(errorMessage)
            }
        }
)
```

##### Important Note:
Ensure `androidx.compose.ui.semantics.error` is present when using the error function. If not included, Kotlin will use the standard error function, which throws an IllegalStateException with defined message.

#### 🚫 Failures

- Error messages do not exist in text nor text alternative or are not descriptive enough.

- Custom components do not support custom error handling.

- Preventing further actions without communicating the issue and necessary corrections to the user.

---

### Labels or Instructions (WCAG 3.3.2 - Level A)

> This technique covers point *3.3.2 Labels or Instructions - Level A of the WCAG standard.*

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

In Compose, there is no built-in way to link a label between different components. However, the `TextField` composable has a `label` parameter that can be used to provide a label for the input field. Another option is to use the `placeholder` parameter to hint at what should be entered into the field.

Example:
```
// Label text for en-US locale would be "Email Address"
TextField(
    value = email,
    onValueChange = { email = it },
    label = { Text(stringResource(R.string.email)) },
    placeholder = { Text(stringResource(R.string.email_example)) }
)
```

:no_entry_sign: **Failure criteria**

- Not providing enough context for the views / composables that expect user interaction.

### Error Suggestion (WCAG 3.3.3 - Level AA)

To provide the best user experience, the application should suggest solutions for input errors when they are detected, unless doing so compromises security or the content's purpose.

> This technique covers point *3.3.3 Error Suggestion - Level AA of the WCAG standard.*

#### ✅ Success technique(s)

When an error is detected, the application should provide the user with a suggestion on how to correct it. This can be done by providing a hint or a description of the error, along with suggested correction text to guide the user.

Using an alert dialog is recommended because it ensures that users see the alert content first, making them aware of any errors. Without this notification, users may not realise an error has occurred and might mistakenly believe the form is not functioning correctly.

Regardless of the method used, the error message should indicate the location of the error and provide a clear explanation of the issue.

### Error Prevention (Legal, Financial, Data) (WCAG 3.3.4 - Level AA)

To prevent users from making mistakes, the application should provide a mechanism before finalizing a transaction that involves legal, financial, or data-sensitive actions.

> This technique covers point *3.3.4 Error Prevention (Legal, Financial, Data) - Level AA of the WCAG standard.*

#### ✅ Success technique(s)

To satisfy this criterion, the app should provide at least one of the following mechanisms:
- **Reversible**: The submission is reversible.
- **Checked**: Data entered by the user is checked for input errors and the user is provided with an opportunity to correct them.
- **Confirmed**: A mechanism is available for reviewing, confirming, and correcting information before finalizing the submission.

For legal transactions, the app should provide a stated time within which the transaction may be amended or canceled by the user after the request.

App should enable users to recover deleted information by temporarily marking it for deletion, moving it to a holding area for a set time, or maintaining a record of deletions for easy restoration requests.

#### 🚫 Failures

Failures are not defined by the WCAG at the time of writing this.

### Redundant Entry (WCAG 3.3.7 - Level A)

Ensure that multi-step processes are user-friendly by not requesting the same information multiple times in a session, as this can be challenging for those with cognitive disabilities. This approach enhances accessibility by reducing memory load and simplifying tasks.

> This technique covers point *3.3.7 Redundant Entry - Level A of the WCAG standard.*

#### ✅ Success technique(s)

Information previously entered by or provided to the user that is required to be entered again in the same process is either:

- auto-populated, or
- available for the user to select.

Techniques mentioned above does not apply to the following cases:

- when re-entering the information is essential
  - Example: A banking app asks users to re-enter their password before confirming a money transfer.
- when the information is required to ensure the security of the content
  - Example: A login screen requires users to re-enter their password after a period of inactivity.
- when previously entered information is no longer valid
  - Example: After changing their email address, a user must re-enter the new email to confirm it.

---

#### Sources

- [Google Support Page](https://support.google.com/accessibility/android)
- [Official Documentation](https://developer.android.com/guide/topics/ui/accessibility)

---

[← Understandable principle](../../principles/understandable_principle.md "Understandable principle")
