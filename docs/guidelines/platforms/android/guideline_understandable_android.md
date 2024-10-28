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

This can be achieved by using **SpannableString** and setting the **LocaleSpan** to define the language for a particular portion of the text. Here's an example:

```kotlin
val text = "Arc de Triomphe"
val spannableString = SpannableString(text)

// Set the language for accessibility
val locale = Locale("fr", "FR")
spannableString.setSpan(LocaleSpan(locale), 0, text.length, Spannable.SPAN_EXCLUSIVE_EXCLUSIVE)

// Assign the spannable string to a TextView
textView.text = spannableString
```

---

## Predictable

Make mobile apps appear and operate in predictable ways.

*This technique covers points 3.2.1 On Focus - Level A & 3.2.2 On Input - Level A of the WCAG standard.*

### On Focus & On Input

:white_check_mark: **Success criteria**

The user should be able to navigate through the app without constant context switching. Also, interacting with the view should not cause a change of context. If view interaction changes the context, that should be signalized to the user **before** the interaction.

If the content displayed on the screen is designed and implemented following [Perceivable guidelines](https://github.com/infinum/accessibility-mobile-standards/blob/master/docs/guidelines/platforms/android/guideline_percievable_android.md), these requirements should be met by default.

:no_entry_sign: **Failure criteria**

- The content is not grouped based on context relationships and has no meaningful labels defined.

---

## Input Assistance

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

#### Sources

- [Google Support Page](https://support.google.com/accessibility/android)
- [Official Documentation](https://developer.android.com/guide/topics/ui/accessibility)

---

[← Understandable principle](../../principles/understandable_principle.md "Understandable principle")
