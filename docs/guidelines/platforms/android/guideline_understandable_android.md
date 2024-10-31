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
<!-- Label text for en-US locale would be "Email Address" -->
TextField(
    value = email,
    onValueChange = { email = it },
    label = { Text(stringResource(R.string.email)) },
    placeholder = { Text(stringResource(R.string.email_example)) }
)
```

:no_entry_sign: **Failure criteria**

- Not providing enough context for the views / composables that expect user interaction.

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
