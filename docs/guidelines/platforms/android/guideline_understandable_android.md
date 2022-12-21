# Understandable guidelines for Android

## Readable

_Make text content readable and understandable._

### Language of the App

:white_check_mark: **Success criteria**

The app should be implemented in a way to reach the largest number of users. It should handle text, audio files, numbers, currency, and graphics in ways appropriate to the locales where it is used. It should provide a text alternative at least in English if it already isn't the default language of the app.

It is recommended that all text content used in the application, including `contentDescription`, is implemented using the Android resource framework.

It is also important to support localization because of accessibility services. Even though TalkBack supports [various languages](https://support.google.com/accessibility/android/answer/11101402?hl=en), not all of them are supported on every Android version.

**Server-driven application**

If the application is server-driven and most of the content is depending on the backend output, it is important to create logic where the app will send the information about the current locale at launch. In that scenario, the backend should, based on the received information about the current locale, return the content in the corresponding language.

:no_entry_sign: **Failure criteria**

- the default language of the app is hardcoded and it is impossible to change it

## Predictable

_Make mobile apps appear and operate in predictable ways._

### On Focus & On Input

:white_check_mark: **Success criteria**

The user should be able to navigate through the app without constant context switching. Also, interacting with the view should not cause a change of context. If view interaction changes the context that should be signalized to the user **before** the interaction.

If the content that is displayed on the screen is designed and implemented following [Perceivable guidelines](https://github.com/infinum/accessibility-mobile-standards/blob/master/docs/guidelines/platforms/android/guideline_percievable_android.md) these requirements should be met by default.

:no_entry_sign: **Failure criteria**

- the content is not grouped based on context relationships and has no meaningful labels defined

## Input Assistance

_Help users avoid and correct mistakes._

### Error identification

:white_check_mark: **Success criteria**

If an error occurs on the item that the user is interacting with, the error should be clearly defined and described so the user can get a clear information of why the error occurred and what to do in order to fix it.

It is recommended to always use or extend system-provided widgets that are as far down Android's class hierarchy as possible, because they already have most accessibility capabilities that your app needs.

On the other hand, if your app requires the implementation of custom components, you will need to implement [custom accessibility events](https://developer.android.com/guide/topics/ui/accessibility/principles#define-custom-events) to provide all accessibility updates that the system-provided widgets do.

:no_entry_sign: **Failure criteria**

- error messages do not exist or are not descriptive enough

- custom components do not support custom error handling 

### Labels or instruction

:white_check_mark: **Success criteria**

When the accessibility services user focuses on input view (for example in the form or login screen) it is important to give him enough information about the type of input that is expected from him to provide.

- Pairs of elements where one describes the other

It is a common case that a given EditText has a corresponding View that describes the content that the user should input within the EditText element. This relationship between elements could be achieved by setting `android:labelFor` attribute on that specific View.

That way, services such as TalkBack will read defined relationships to the user giving him more context about expected input when EditText is in focus.

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

In the given example, services such as TalkBack will read - "EditBox for username" when user sets focus to EditText.

:no_entry_sign: **Failure criteria**

- not providing enough context for the views that expect user interaction
