[⬅️ Principles and guidelines](../accessibility_principles_and_guidelines.md)

# Operable principle

The [operable chapter in the WCAG standard](https://www.w3.org/WAI/WCAG21/quickref/?currentsidebar=%23col_overview&levels=aa%2Caaa&technologies=smil%2Cpdf%2Cflash%2Csl#principle2) describes how disabilities might make it hard for some users to interact with the app. It contains information about how they alter the way users perform in-app actions and how to ensure users with nonstandard input devices can operate all parts of the app.

## Keyboard Accessible (WCAG 2.1)

The app should be fully functional for users whose only input device is the keyboard. Operating via the keyboard should be concise and possible without requiring specific timing for individual keystrokes. Navigating into and out of different parts of the app should be possible without getting stuck. Document unconventional keyboard navigation methods. For keyboard shortcuts that only require pressing a single letter or number, the user should be able to turn the shortcut off or remap it.

### Keyboard (WCAG 2.1.1 - Level A)

Make all functionality available from a keyboard.

*This guideline covers point 2.1.1 Keyboard - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#keyboard-wcag-211---level-a)
* [Flutter](../platforms/flutter/techniques_operable_flutter.md#keyboard-wcag-211---level-a)

## Enough Time (WCAG 2.2)

Some users might have trouble grasping and interacting with the content that is available only for a limited time or is auto-updating. If possible, there should be a way to extend, pause or disable the timing.

### Timing Adjustable (WCAG 2.2.1 - Level A)

The user can turn off, adjust, or extend each time limit set by the content.

> This guideline covers point *2.2.1 Timing Adjustable - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#timing-adjustable-wcag-221---level-a)
* [Flutter](../platforms/flutter/techniques_operable_flutter.md#timing-adjustable-wcag-221---level-a)
* [iOS](../platforms/ios/techniques_operable_ios.md#timing-adjustable-wcag-221---level-a)


### Pause, Stop, Hide (WCAG 2.2.2 - Level A)

Moving, blinking, or scrolling, or auto-updating content in the app.

> This guideline covers point *2.2.2 Pause, Stop Hide - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#pause-stop-hide-wcag-222---level-a)
* [Flutter](../platforms/flutter/techniques_operable_flutter.md#pause-stop-hide-wcag-222---level-a)
* [iOS](../platforms/ios/techniques_operable_ios.md#pause-stop-hide-wcag-222---level-a)

## Seizures and Physical Reactions (WCAG 2.3)

For some users, excessive flashing might cause seizures. As a general rule, avoid content that flashes more than three times in any one-second period.

### Three Flashed or Below Threshold (WCAG 2.3.1 - Level A)

Apps should not contain any element that flashes more than three times in one second.

> This guideline covers point *2.3.1 - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#three-flashed-or-below-threshold-wcag-231---level-a)
* [Flutter](../platforms/flutter/techniques_operable_flutter.md#three-flashed-or-below-threshold-wcag-231---level-a)
* [iOS](../platforms/ios/techniques_operable_ios.md#three-flashed-or-below-threshold-wcag-231---level-a)

## Navigable (WCAG 2.4)

The app's navigation structure should be concise and easy to understand. Users should have an indication of where they are located and how their actions will affect their location. There should be a way to bypass content that is repeated on multiple screens. The focus order should be clear and predictable.

### Bypass Blocks (WCAG 2.4.1 - Level A)

A skip mechanism is available to bypass blocks of content that are repeated in the app.

> This guideline covers point *2.4.1 Bypass Blocks - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#bypass-blocks-wcag-241---level-a)
* [Flutter](../platforms/flutter/techniques_operable_flutter.md#bypass-blocks-wcag-241---level-a)
* [iOS](../platforms/ios/techniques_operable_ios.md#bypass-blocks-wcag-241---level-a)

### Page Titled (WCAG 2.4.2 -Level A)

Screens have a clear, descriptive, and possibly unique title that describes the topic or purpose and is easily understood by all users.

> This guideline covers point *2.4.2 Page Titled - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#page-titled-wcag-242---level-a)
* [Flutter](../platforms/flutter/techniques_operable_flutter.md#page-titled-wcag-242---level-a)
* [iOS](../platforms/ios/techniques_operable_ios.md#page-titled-wcag-242---level-a)

### Focus Order (WCAG 2.4.3 - Level A)

Ensure that information is read (VoiceOver, TalkBack) in an order consistent with the meaning and content.

> This guideline covers point *2.4.3 Focus Order - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#focus-order-wcag-243---level-a)
* [iOS](../platforms/ios/techniques_operable_ios.md#focus-order-wcag-243---level-a)

### Link Purpose (WCAG 2.4.4 - Level A)

The purpose of a button or link action is clear and easily understandable by all users

> This guideline covers point *2.4.4 Link Purpose (In Context) - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#link-purpose-wcag-244---level-a)
* [Flutter](../platforms/flutter/techniques_operable_flutter.md#link-purpose-wcag-244---level-a)
* [iOS](../platforms/ios/techniques_operable_ios.md#link-purpose-wcag-244---level-a)

### Heading and Labels (WCAG 2.4.6 - Level AA)

Based on this guideline, the user should be able to understand the purpose of the heading or label. The heading or label should be descriptive and provide information about the content that follows.

> This guideline covers point *2.4.6 Headings and Labels - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#heading-and-labels-wcag-246---level-aa)
* [iOS](../platforms/ios/techniques_operable_ios.md#heading-and-labels-wcag-246---level-aa)

### Focus Visibility (WCAG 2.4.7 - Level AA)

This guideline states that the user should be able to see the focus on the element that is currently selected. With a mobile platform in mind, this guideline is automatically satisfied if VoiceOver is used - handled by the system (iOS).

> This guideline covers point *2.4.7 Focus Visible - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#focus-visibility-wcag-247---level-aa)
* [iOS](../platforms/ios/techniques_operable_ios.md#focus-visibility-wcag-247---level-aa)


### Focus Not Obscured (Minimum) (WCAG 2.4.11 - Level AA)

When the user navigates through the app, the focus should not be obscured by other elements and should be visible (at least partially).

> This guideline covers point *2.4.11 Focus Not Obscured (Minimum) - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#focus-not-obscured-minimum-wcag-2411---level-aa)
* [iOS](../platforms/ios/techniques_operable_ios.md#focus-not-obscured-minimum-wcag-2411---level-aa)

## Input modalities (WCAG 2.5)

Some users might have trouble moving the device themselves or performing complex gestures. Strive for the app to be operable using a variety of input methods. If possible, the user should have a way to undo the interaction and disable the input methods he might trigger accidentally.

### Label in Name (WCAG 2.5.3 - Level A)

All user interface components that are defined as labels should contain the name, which is visible (presented visually).

> This guideline covers point *2.5.3 Label in Name - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#label-in-name-wcag-253---level-a)
* [iOS](../platforms/ios/techniques_operable_ios.md#label-in-name-wcag-253---level-a)

### Motion Actuation (WCAG 2.5.4 - Level A)

We need to ensure that content does not rely on device motion for control, as some users may have difficulty moving or holding a device steadily. This helps make content accessible to everyone, regardless of their physical abilities (e.g. shake to undo).

> This guideline covers point *2.5.4 Motion Actuation - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#motion-actuation-wcag-254---level-a)
* [iOS](../platforms/ios/techniques_operable_ios.md#motion-actuation-wcag-254---level-a)

### Dragging Movements (WCAG 2.5.7 - Level AA)

Due to different disabilities, some users may have difficulty performing dragging movements. This guideline states that the application should provide an alternative way to perform the action that is not based on dragging movements.

> This guideline covers point *2.5.7 Dragging Movements - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#dragging-movements-wcag-257---level-aa)
* [iOS](../platforms/ios/techniques_operable_ios.md#dragging-movements-wcag-257---level-aa)

### Target Size (Minimum) (WCAG 2.5.8 - Level AA)

This guideline tries to ensure that the target size of the elements is large enough to be easily operable by touch. To fully understand the requirements, please check examples and details about it [here](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html).

> This guideline covers point *2.5.8 Target Size (Minimum) - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_operable_android.md#target-size-minimum-wcag-258---level-aa)
* [iOS](../platforms/ios/techniques_operable_ios.md#target-size-minimum-wcag-258---level-aa)

## Other operable guidelines

This section contains guidelines that may not applicable for the mobile (iOS) platform, or its criteria is a not the responsibility of the mobile team. Still, take into account that those guidelines needs to be satisfied.

- [No Keyboard Trap (WCAG 2.1.2 - Level A)](https://www.w3.org/WAI/WCAG22/quickref/#no-keyboard-trap)
- [Character Key Shortcuts (WCAG 2.1.4 - Level A)](https://www.w3.org/WAI/WCAG22/quickref/#character-key-shortcuts)
- [Multiple Ways (WCAG 2.4.5 - Level AA)](https://www.w3.org/WAI/WCAG22/quickref/#multiple-ways)
- [Pointer Gestures (WCAG 2.5.1 - Level A)](https://www.w3.org/WAI/WCAG22/quickref/#pointer-gestures)
- [Pointer Cancellation (WCAG 2.5.2 - Level A](https://www.w3.org/WAI/WCAG22/quickref/#pointer-cancellation)

⎯

[← Perceivable](perceivable_principle.md) | [Understandable →](understandable_principle.md)
