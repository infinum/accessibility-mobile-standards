 [🔼 Accessibility principles and examples](../../principles/accessibility_principles_and_examples.md  "Accessibility principles and examples") | [⬅️ Understandable principle](../../principles/understandable_principle.md "Understandable principle")

# Understandable guidelines for Android

## Readable (WCAG 3.1)

Make text content readable and understandable.

### Language of Page (WCAG 3.1.1 -Level A)

This guideline covers point [3.1.1 Language of Page - Level A](https://www.w3.org/WAI/WCAG22/quickref/#language-of-page) of the WCAG standard.

The default human language of an App can be programmatically determined.

:white_check_mark: **Success criteria**

The app should be implemented to reach the largest number of users. It should handle text, audio files, numbers, currency, and graphics in ways appropriate to the locales where it is used. It should provide a text alternative, at least in English, if it already isn't the default language of the app.

It is recommended that all text content used in the application, including `contentDescription`, is implemented using the Android resource framework.

To simplify this process, you can use a library like [Localian](https://github.com/infinum/android-localian). It manages application locale and language across multiple Android API levels without requiring a restart of the application process.

It is also important to support localization because of accessibility services. Even though TalkBack supports [various languages](https://support.google.com/accessibility/android/answer/11101402?hl=en), not all of them are supported on every Android version.

**Server-driven application**

If the application is server-driven and most of the content depends on the backend output, it is important to create logic where the app will send the information about the current locale at launch. In that scenario, the backend should return the content in the corresponding language based on the received information about the current locale.

This can be achieved by specifying the application's default language in the HTTP headers of API calls:

```text
Content-Language: de-DE
or
Content-Language: en-US
or
Content-Language: de-DE, en-CA
etc.
```

To enhance user control, include an option in the app’s settings for users to select their preferred language. It’s also beneficial to inform users that the default app language is based on their location or region, with the option to override it if desired. Users should also have the flexibility to allow the app to follow their device’s language settings.

:no_entry_sign: **Failure criteria**

- The default language of the app is hardcoded, and it is impossible to change it.

```kotlin
fun setLocaleEn(context: Context): Context {
   val locale = Locale("en", "US")
   Locale.setDefault(locale)
   
   val config = context.resources.configuration
   config.setLocale(locale)

   return context.createConfigurationContext(config)
}
```

### Language of Parts (WCAG 3.1.2 -Level AA)

This guideline covers point [3.1.2 Language of Parts - Level AA](https://www.w3.org/WAI/WCAG22/quickref/#language-of-parts) of the WCAG standard.

To be able to give the best possible experience to users, the language of each part of the app should be programmatically determined. With that in mind, Talkback should be able to read the content in the correct language.

:white_check_mark: **Success criteria**

Due to need for Talkback to read the content in the correct language, the part of the content should get the correct language interpretation.

In a traditional Android view, you can set the locale for accessibility by applying a **LocaleSpan** to a **SpannableString** and assigning it to a **TextView**:

```kotlin
val text = "Arc de Triomphe"
val spannableString = SpannableString(text)

val locale = Locale("fr", "FR")
spannableString.setSpan(LocaleSpan(locale), 0, text.length, Spannable.SPAN_EXCLUSIVE_EXCLUSIVE)

textView.text = spannableString
```

In Jetpack Compose, achieve the same with an **AnnotatedString**:
```kotlin
val text = "Arc de Triomphe"

val localeList = LocaleList("fr-FR")

val annotatedText = buildAnnotatedString {
    withStyle(style = SpanStyle(localeList = localeList)) {
        append(text)
    }
}

Text(text = annotatedText)
```

---

## Predictable (WCAG 3.2)

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

### Consistent Navigation (WCAG 3.2.3 - Level AA)

For users, it is important to have a consistent navigation experience throughout the app (on all screens). With that satisfied, users can easily predict where they are and where they can go next.

#### ✅ Success criteria

To satisfy this criterion, try to keep the navigation structure consistent, with elements like the toolbar, bottom navigation, search bar or any other repeated elements always in the same place, read out in the same order and with the same functionality.

Visually, this is mostly the responsibility of the design, but it is important to make sure that consistent ordering is preserved when using assistive technologies (e.g. TalkBack) as well.

If there is a need to manually adjust ordering of elements to make them consistent across multiple screens, the same techniques described in [Meaningful sequence guideline](guideline_percievable_android.md#meaningful-sequence-wcag-132---level-a) can be applied.

#### 🚫 Failure examples

Usually, when reusing the same components across multiple screens, the ordering will be preserved automatically. However, there are certain cases where other elements might come "in-between" and there could be some inconsistencies when mixing technologies on the same screen (e.g. the toolbar is a `View`, while all of the other screen contents are in Compose), so pay special attention to those.

- TalkBack: Two screens share the same bottom navigation bar. On the first screen, the bottom bar items are read out last, after all the other content. On the second screen, the bottom bar items are read out after the toolbar and before any other screen content.
- TalkBack: An app has multiple screens that contain a toolbar with a title and a navigation button. On some screens, the navigation button is read out first and, on others, the title is read out before the navigation button.

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

One of the possibilities is using an alert dialog since it ensures that users see the alert content first, making them aware of any errors. Without this notification, users may not realise an error has occurred and might mistakenly believe the form is not functioning correctly.

Regardless of the method used, the error message should indicate the location of the error and provide a clear explanation of the issue.

### Error Prevention (Legal, Financial, Data) (WCAG 3.3.4 - Level AA)

To prevent users from making mistakes, the application should provide a mechanism before finalizing a transaction that involves legal, financial, or data-sensitive actions.

> This technique covers point *3.3.4 Error Prevention (Legal, Financial, Data) - Level AA of the WCAG standard.*

#### ✅ Success technique(s)

To satisfy this criterion, the app should provide at least one of the following mechanisms:
- **Reversible**: The submission is reversible.
  - Example: A shopping app allows users to cancel or modify their order within 30 minutes, displaying a notification with cancellation options immediately after the order is placed. 
- **Checked**: Data entered by the user is checked for input errors and the user is provided with an opportunity to correct them.
  - Example: A registration form highlights fields with errors, such as an invalid email format, and prompts users to correct them before proceeding. 
- **Confirmed**: A mechanism is available for reviewing, confirming, and correcting information before finalizing the submission.
  - Example: A banking app presents a summary of payment order details, allowing users to review and edit information such as recipient account number before finalizing the transaction. 

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

#### 🚫 Failures
  
Failures are not defined by the WCAG at the time of writing this.

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
