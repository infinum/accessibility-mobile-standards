[⬅️ Principles and guidelines](../accessibility_principles_and_guidelines.md)

# Understandable principle

The understandable principle from the [WCAG](https://www.w3.org/WAI/WCAG21/quickref/?currentsidebar=%23col_overview&levels=aa%2Caaa&technologies=smil%2Cpdf%2Cflash%2Csl#principle3) describes how elements of the user interface should be understandable to the users. In this case, it should be understandable and clear from the content, design, and action point of view – whether the application is used with or without assistive technology.

## Readable (WCAG 3.1)

The application content should be identifiable by the language used in the application. Content and all words mentioned in the application should have a context while avoiding unusual words, abbreviations, and jargon.

### Language of Page (WCAG 3.1.1 - Level A)

The default human language of an App can be programmatically determined.

> This guideline covers point *3.1.1 Language of Page - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_understandable_android.md#language-of-page-wcag-311---level-a)
* [Flutter](../platforms/flutter/techniques_understandable_flutter.md#language-of-page-wcag-311---level-a)
* [iOS](../platforms/ios/techniques_understandable_ios.md#language-of-page-wcag-311---level-a)

### Language of Parts (WCAG 3.1.2 - Level AA)

To be able to give the best possible experience to users, the language of each part of the app should be programmatically determined. With that in mind, VoiceOver should be able to read the content in the correct language.

> This guideline covers point *3.1.2 Language of Parts - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_understandable_android.md#language-of-parts-wcag-312---level-aa)
* [iOS](../platforms/ios/techniques_understandable_ios.md#language-of-parts-wcag-312---level-aa)

## Predictable (WCAG 3.2)

This is initially defined for web pages but is also applicable for mobile applications (pages or screens). The idea is to have a consistent design and application behavior to make users comfortable using the application.

The context in which the user operates should be logical, without problematic behavior, which would lead to inconsistent navigation, component identification, or context switching.

### On Focus & On Input (WCAG 3.2.1-3.2.2 - Level A)

Receiving focus on or interacting with any component should not initiate a change of context unless previously announced.

> This technique covers points *3.2.1 On Focus - Level A and 3.2.2 On Input - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_understandable_android.md#on-focus--on-input-wcag-321-322---level-a)
* [Flutter](../platforms/flutter/techniques_understandable_flutter.md#on-focus--on-input-wcag-321-322---level-a)
* [iOS](../platforms/ios/techniques_understandable_ios.md#on-focus--on-input-wcag-321-322---level-a)

### Consistent Navigation (WCAG 3.2.3 - Level AA)

For users, it is important to have a consistent navigation experience throughout the app. With that satisfied, users can easily predict where they are and where they can go next.

> This technique covers point *3.2.3 Consistent Navigation - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_understandable_android.md#consistent-navigation-wcag-323---level-aa)
* [iOS](../platforms/ios/techniques_understandable_ios.md#consistent-navigation-wcag-323---level-aa)

### Consistent Identification (WCAG 3.2.4 - Level AA)

While using the application, components that have the same functionality should be identified consistently.

> This technique covers point *3.2.4 Consistent Identification - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_understandable_android.md#consistent-identification-wcag-324---level-aa)
* [iOS](../platforms/ios/techniques_understandable_ios.md#consistent-identification-wcag-324---level-aa)

## Input Assistance (WCAG 3.3)

One of the most important parts of the application is user input, and as a developer, you should provide the best experience for operations that involves user input.

We should provide enough information to the user when input elements are used inside the application, like labels, placeholders, or instructions. The same goes for error identification and appearance, which should provide enough information and context of the input state. With a good approach, users will be able to use input elements with ease, whether they use them with or without assistive technologies.

### Error Identification (WCAG 3.3.1 - Level A)

If an input error is automatically detected, the item in error is identified, and the error is clearly described to the user in text.

> This technique covers point *3.3.1 Error Identification - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_understandable_android.md#error-identification-wcag-331---level-a)
* [Flutter](../platforms/flutter/techniques_understandable_flutter.md#error-identification-wcag-331---level-a)
* [iOS](../platforms/ios/techniques_understandable_ios.md#error-identification-wcag-331---level-a)

### Labels or Instructions (WCAG 3.3.2 - Level A)

Labels or instructions are provided when content requires user input.

> This technique covers point *3.3.2 Labels or Instructions - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_understandable_android.md#labels-or-instructions-wcag-332---level-a)
* [Flutter](../platforms/flutter/techniques_understandable_flutter.md#labels-or-instructions-wcag-332---level-a)
* [iOS](../platforms/ios/techniques_understandable_ios.md#labels-or-instructions-wcag-332---level-a)

### Error Suggestion (WCAG 3.3.3 - Level AA)

To provide the best user experience, the application should suggest solutions for input errors when they are detected.

> This technique covers point *3.3.3 Error Suggestion - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_understandable_android.md#error-suggestion-wcag-333---level-aa)
* [iOS](../platforms/ios/techniques_understandable_ios.md#error-suggestion-wcag-333---level-aa)

### Error Prevention (Legal, Financial, Data) (WCAG 3.3.4 - Level AA)

To prevent users from making mistakes, the application should provide a mechanism before finalizing a transaction that involves legal, financial, or data-sensitive actions.

> This technique covers point *3.3.4 Error Prevention (Legal, Financial, Data) - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_understandable_android.md#error-prevention-legal-financial-data-wcag-334---level-aa)
* [iOS](../platforms/ios/techniques_understandable_ios.md#error-prevention-legal-financial-data-wcag-334---level-aa)

### Redundant Entry (WCAG 3.3.7 Level A)

Ensure that multi-step processes are user-friendly by not requesting the same information multiple times in a session, as this can be challenging for those with cognitive disabilities. This approach enhances accessibility by reducing memory load and simplifying tasks.

> This technique covers point *3.3.7 Redundant Entry - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_understandable_android.md#redundant-entry-wcag-337-level-a)
* [iOS](../platforms/ios/techniques_understandable_ios.md#redundant-entry-wcag-337-level-a)

### Accessible Authentication (Minimum) (WCAG 3.3.8 - Level AA)

To make authentication accessible to all users, the application should not require a cognitive function test unless that step provides at least one of the following:

- **Alternative**: Another authentication method that does not rely on a cognitive function test.
- **Mechanism**: A mechanism is available to assist the user in completing the cognitive function test.
- **Object Recognition**: The cognitive function test is to recognize objects.
- **Personal Content**: The cognitive function test is to identify non-text content the user provided to the application.

> This technique covers point *3.3.8 Accessible Authentication (Minimum) - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_understandable_android.md#accessible-authentication-minimum-wcag-338---level-aa)
* [iOS](../platforms/ios/techniques_understandable_ios.md#accessible-authentication-minimum-wcag-338---level-aa)

## Other understandable guidelines

This section contains guidelines that may not be applicable to the mobile platforms or its criteria is not the responsibility of the mobile team. Still, take into account that those guidelines need to be satisfied.

- [Consistent Help (WCAG 3.2.6 - Level A)](https://www.w3.org/WAI/WCAG22/quickref/#consistent-help)

⎯

[← Operable](operable_principle.md) | [Robust →](robust_principle.md)
