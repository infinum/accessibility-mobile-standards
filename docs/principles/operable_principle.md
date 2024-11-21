[⬅️ Principles and guidelines](../accessibility_principles_and_guidelines.md)

# 2. Operable principle

The [operable chapter in the WCAG standard](https://www.w3.org/WAI/WCAG21/quickref/?currentsidebar=%23col_overview&levels=aa%2Caaa&technologies=smil%2Cpdf%2Cflash%2Csl#principle2) describes how disabilities might make it hard for some users to interact with the app. It contains information about how they alter the way users perform in-app actions and how to ensure users with nonstandard input devices can operate all parts of the app.

## 2.1. Keyboard Accessible

The app should be fully functional for users whose only input device is the keyboard. Operating via the keyboard should be concise and possible without requiring specific timing for individual keystrokes. Navigating into and out of different parts of the app should be possible without getting stuck. Document unconventional keyboard navigation methods. For keyboard shortcuts that only require pressing a single letter or number, the user should be able to turn the shortcut off or remap it.

### 2.1.1 Keyboard (Level A)

Make all functionality available from a keyboard.

*This guideline covers point 2.1.1 Keyboard - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#211-keyboard-level-a)
* [Flutter](../platforms/flutter/techniques_operable_flutter.md#211-keyboard-level-a)

## 2.2 Enough Time

Some users might have trouble grasping and interacting with the content that is available only for a limited time or is auto-updating. If possible, there should be a way to extend, pause or disable the timing.

### 2.2.1 Timing Adjustable (Level A)

The user can turn off, adjust, or extend each time limit set by the content.

> This guideline covers point *2.2.1 Timing Adjustable - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#221-timing-adjustable-level-a)
* [Flutter](../platforms/flutter/techniques_operable_flutter.md#221-timing-adjustable-level-a)
* [iOS](../platforms/ios/techniques_operable_ios.md#221-timing-adjustable-level-a)


### 2.2.2 Pause, Stop, Hide (Level A)

Moving, blinking, or scrolling, or auto-updating content in the app.

> This guideline covers point *2.2.2 Pause, Stop Hide - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#222-pause-stop-hide-level-a)
* [Flutter](../platforms/flutter/techniques_operable_flutter.md#222-pause-stop-hide-level-a)
* [iOS](../platforms/ios/techniques_operable_ios.md#222-pause-stop-hide-level-a)

## 2.3 Seizures and Physical Reactions

For some users, excessive flashing might cause seizures. As a general rule, avoid content that flashes more than three times in any one-second period.

### 2.3.1 Three Flashed or Below Threshold (Level A)

Apps should not contain any element that flashes more than three times in one second.

> This guideline covers point *2.3.1 - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#231-three-flashed-or-below-threshold-level-a)
* [Flutter](../platforms/flutter/techniques_operable_flutter.md#231-three-flashed-or-below-threshold-level-a)
* [iOS](../platforms/ios/techniques_operable_ios.md#231-three-flashed-or-below-threshold-level-a)

## 2.4 Navigable

The app's navigation structure should be concise and easy to understand. Users should have an indication of where they are located and how their actions will affect their location. There should be a way to bypass content that is repeated on multiple screens. The focus order should be clear and predictable.

### 2.4.1 Bypass Blocks (Level A)

A skip mechanism is available to bypass blocks of content that are repeated in the app.

> This guideline covers point *2.4.1 Bypass Blocks - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#241-bypass-blocks-level-a)
* [Flutter](../platforms/flutter/techniques_operable_flutter.md#241-bypass-blocks-level-a)
* [iOS](../platforms/ios/techniques_operable_ios.md#241-bypass-blocks-level-a)

### 2.4.2 Page Titled (Level A)

Screens have a clear, descriptive, and possibly unique title that describes the topic or purpose and is easily understood by all users.

> This guideline covers point *2.4.2 Page Titled - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#242-page-titled-level-a)
* [Flutter](../platforms/flutter/techniques_operable_flutter.md#242-page-titled-level-a)
* [iOS](../platforms/ios/techniques_operable_ios.md#242-page-titled-level-a)

### 2.4.3 Focus Order (Level A)

Ensure that information is read (VoiceOver, TalkBack) in an order consistent with the meaning and content.

> This guideline covers point *2.4.3 Focus Order - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#243-focus-order-level-a)
* [iOS](../platforms/ios/techniques_operable_ios.md#243-focus-order-level-a)

### 2.4.4 Link Purpose (Level A)

The purpose of a button or link action is clear and easily understandable by all users

> This guideline covers point *2.4.4 Link Purpose (In Context) - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#244-link-purpose-level-a)
* [Flutter](../platforms/flutter/techniques_operable_flutter.md#244-link-purpose-level-a)
* [iOS](../platforms/ios/techniques_operable_ios.md#244-link-purpose-level-a)

### 2.4.6 Heading and Labels (Level AA)

Based on this guideline, the user should be able to understand the purpose of the heading or label. The heading or label should be descriptive and provide information about the content that follows.

> This guideline covers point *2.4.6 Headings and Labels - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#246-heading-and-labels-level-aa)
* [iOS](../platforms/ios/techniques_operable_ios.md#246-heading-and-labels-level-aa)

### 2.4.7 Focus Visibility (Level AA)

This guideline states that the user should be able to see the focus on the element that is currently selected. With a mobile platform in mind, this guideline is automatically satisfied if VoiceOver is used - handled by the system (iOS).

> This guideline covers point *2.4.7 Focus Visible - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#247-focus-visibility-level-aa)
* [iOS](../platforms/ios/techniques_operable_ios.md#247-focus-visibility-level-aa)


### 2.4.11 Focus Not Obscured (Minimum) (Level AA)

When the user navigates through the app, the focus should not be obscured by other elements and should be visible (at least partially).

> This guideline covers point *2.4.11 Focus Not Obscured (Minimum) - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#2411-focus-not-obscured-minimum-level-aa)
* [iOS](../platforms/ios/techniques_operable_ios.md#2411-focus-not-obscured-minimum-level-aa)

## 2.5 Input modalities

Some users might have trouble moving the device themselves or performing complex gestures. Strive for the app to be operable using a variety of input methods. If possible, the user should have a way to undo the interaction and disable the input methods he might trigger accidentally.

### 2.5.3 Label in Name (Level A)

All user interface components that are defined as labels should contain the name, which is visible (presented visually).

> This guideline covers point *2.5.3 Label in Name - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#253-label-in-name-level-a)
* [iOS](../platforms/ios/techniques_operable_ios.md#253-label-in-name-level-a)

### 2.5.4 Motion Actuation (Level A)

We need to ensure that content does not rely on device motion for control, as some users may have difficulty moving or holding a device steadily. This helps make content accessible to everyone, regardless of their physical abilities (e.g. shake to undo).

> This guideline covers point *2.5.4 Motion Actuation - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#254-motion-actuation-level-a)
* [iOS](../platforms/ios/techniques_operable_ios.md#254-motion-actuation-level-a)

### 2.5.7 Dragging Movements (Level AA)

Due to different disabilities, some users may have difficulty performing dragging movements. This guideline states that the application should provide an alternative way to perform the action that is not based on dragging movements.

> This guideline covers point *2.5.7 Dragging Movements - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#257-dragging-movements-level-aa)
* [iOS](../platforms/ios/techniques_operable_ios.md#257-dragging-movements-level-aa)

### 2.5.8 Target Size (Minimum) (Level AA)

This guideline tries to ensure that the target size of the elements is large enough to be easily operable by touch. To fully understand the requirements, please check examples and details about it [here](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html).

> This guideline covers point *2.5.8 Target Size (Minimum) - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#258-target-size-minimum-level-aa)
* [iOS](../platforms/ios/techniques_operable_ios.md#258-target-size-minimum-level-aa)

## Other operable guidelines

This section contains guidelines that may not applicable for the mobile (iOS) platform, or its criteria is a not the responsibility of the mobile team. Still, take into account that those guidelines needs to be satisfied.

- [2.1.2 No Keyboard Trap - Level A](https://www.w3.org/WAI/WCAG22/quickref/#no-keyboard-trap)
- [2.1.4 Character Key Shortcuts - Level A](https://www.w3.org/WAI/WCAG22/quickref/#character-key-shortcuts)
- [2.4.5 Multiple Ways - Level AA](https://www.w3.org/WAI/WCAG22/quickref/#multiple-ways)
- [2.5.1 Pointer Gestures - Level A](https://www.w3.org/WAI/WCAG22/quickref/#pointer-gestures)
- [2.5.2 Pointer Cancellation - Level A](https://www.w3.org/WAI/WCAG22/quickref/#pointer-cancellation)

⎯

[← Perceivable](perceivable_principle.md) | [Understandable →](understandable_principle.md)
