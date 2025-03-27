[⬅️ Principles and guidelines](../accessibility_principles_and_guidelines.md)

# Robust principle

This principle describes that the content of an application should be robust enough to be interpreted by the user but also by different user agents, including assistive technologies.

To be more precise, we can interpret it as: the application should be compatible with the assistive technology available on the platform the user uses.

## Compatible (WCAG 4.1)

Compatible is the only aspect defined by this principle, and it describes how to maximize compatibility with the current platform and assistive technologies on it. Also, it defines that all components should be programmatically determined – their name, role, and value.

### Name, Role, Value (WCAG 4.1.2 - Level A)

User interface elements should be clearly defined by their name ([accessibility label](https://developer.apple.com/documentation/objectivec/nsobject/1615181-accessibilitylabel) & [accessibility hint](https://developer.apple.com/documentation/objectivec/nsobject/1615093-accessibilityhint)), the role that they have (accessibility identifier), and the value they carry([accesibility value](https://developer.apple.com/documentation/objectivec/nsobject/1615117-accessibilityvalue)). The app should be able to notify the user if any of these parameters change programmatically without user input (or the changes should be reflected in the element's accessibility attributes) so that the user remains aware of what this element does at all times.

> This guideline covers point *4.1.2 Name, Role, Value - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_robust_android.md#name-role-value-wcag-412---level-a)
* [Flutter](../platforms/flutter/techniques_robust_flutter.md#name-role-value-wcag-412---level-a)
* [iOS](../platforms/ios/techniques_robust_ios.md#name-role-value-wcag-412---level-a)

### Status messages (WCAG 4.1.3 - Level AA)

The guideline states that status messages should be programmatically determinable by the user. 
This means that the user should be able to know the status of the app at any given time without having to interact with it.

On mobile this means that the user should be able to know if the current state has been changed - which is especially important for users who rely on screen readers.

> This guideline covers point *4.1.3 Status messages - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_robust_android.md#status-messages-wcag-413---level-aa)
* [iOS](../platforms/ios/techniques_robust_ios.md#status-messages-wcag-413---level-aa)

[← Understandable](understandable_principle.md) | [Platform specifics →](../accessibility_platform_specifics.md)