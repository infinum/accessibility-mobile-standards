# Understandable guidelines for Android

## Readable

_Make text content readable and understandable._

### Language of the App

The app should be implemented in a way to reach the most users. It should handle text, audio files, numbers, currency, and graphics in ways appropriate to the locales where it is used. It should provide a text alternative for, at least English language if the one is not the default language of the app.

It is recommended that all text content used in the application, including `contentDescriptions`, is implemented using the Android resource framework.

It is also important to support localization because of accessibility services. Even though TalkBack supports [various languages](https://support.google.com/accessibility/android/answer/11101402?hl=en), not all of them are supported on every Android version.

**Server-driven application**

If the application is server-driven and most of the content is depending on the backend output, it is important to create logic where the app will on launch send information about the current locale. In that scenario, the backend should based on the received information about the current locale, return the content in the corresponding language.

:white_check_mark: **Success criteria**

- application's content is localized based on the current locale

:no_entry_sign: **Failure criteria**

- the default language of the app is hardcoded and it is impossible to change it

## Predictable

_Make mobile apps appear and operate in predictable ways._

### On Focus & On Input

The user should be able to navigate through the app without constant context switching. Also, interacting with the view should not cause a change of context. If view interaction changes the context that should be signalized to the user **before** the interaction.

If the content that is displayed on the screen is designed and implemented following [Perceivable guidelines] these requirements should be met by default.

:white_check_mark: **Success criteria**

- the content is grouped and labeled following [Perceivable guidelines].

:no_entry_sign: **Failure criteria**

- the content is not grouped based on context relationships and has no meaningful labels defined

## Input Assistance

_Help users avoid and correct mistakes._

### Error identification

If an error occurs on the item that the user is interacting with, the one should be clearly defined and described so the user could have a clear picture of why the error occurred and what to do to fix it.

It is recommended to always use or extend system-provided widgets that are as far down Android's class hierarchy as possible because the ones already have the most accessibility capabilities that your app needs.

On the other hand, if your app requires the implementation of custom components, you will need to implement [custom accessibility events](https://developer.android.com/guide/topics/ui/accessibility/principles#define-custom-events)
to provide all accessibility updates the same as system-provided widgets do.

### Labels or instruction

When the accessibility services user focuses on some sort of input view (for example in the form or login screen or something else) it is important to give him enough information about the type of input that is expected from him to provide.

- Pairs of elements where one describes the other

It is a common case that given EditText has a corresponding View that describes the content that the user should enter within the EditText element. This relationship between elements could be achieved by setting the` android:labelFor` attribute on that specific View.

That way, services such as TalkBack will read defined relationships to the user to give him a bit more context when EditText is in focus.

An example of labeling such an element pair is given in the following snippet:

```
<!-- Label text for en-US locale would be "Username:" -->
<TextView
   android:id="@+id/usernameLabel" ...
   android:text="@string/username"
   android:labelFor="@+id/usernameEntry" />

<EditText
   android:id="@+id/usernameEntry" ... />
```

In the given example, services such as TalkBack will read - "EditBox for username" when the user sets focus to EditText.

:white_check_mark: **Success criteria**

- input views are paired with other descriptions in a way that they provide meaningful information about the required input type

:no_entry_sign: **Failure criteria**

- input views have no additional descriptions provided about the required input type 
