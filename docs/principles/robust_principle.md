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

⎯

[⬅️ Principles and guidelines](../accessibility_principles_and_guidelines.md)

# Perceivable principle

Information and user interface components must be presentable to users in ways they can perceive.

## Text alternatives (WCAG 1.1)

Provide text alternatives for any non-text content to be changed into other forms people need, such as large print, braille, speech, symbols, or more straightforward language.

### Non-text content (WCAG 1.1.1 - Level A)

When talking about the screen elements, it is important to make information about all elements accessible and available. Some elements may not have text included by design or as a default user interface component. This can be seen when buttons are used with icons only, images, or other decorative elements.

Some users may have issues identifying an element's functionality or description in general, and because of that, it is important to define non-text elements by accessibility features.

> This guideline with provided techniques covers the *1.1.1 Non-text Content - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_percievable_android.md#non-text-content-wcag-111---level-a)
* [Flutter](../platforms/flutter/techniques_perceivable_flutter.md#non-text-content-wcag-111---level-a)
* [iOS](../platforms/ios/techniques_perceivable_ios.md#non-text-content-wcag-111---level-a)

## Time-based Media (WCAG 1.2)

Provide alternatives for time-based media.

### Captions support for prerecorded media (WCAG 1.2.1-1.2.2 - Level A)

Due to some disabilities, some users may not be able to hear the content of the media provided by the application. An example of that can be a prerecorded audio or video track. In some cases, it is necessary to add support for some accessibility features to make this content accessible to all users.

> This guideline with provided techniques covers the *1.2.1 Audio-only and Video-only (Prerecorded) - Level A and 1.2.2 Captions (Prerecorded) - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_percievable_android.md#captions-support-for-prerecorded-media-wcag-121-122---level-a)
* [Flutter](../platforms/flutter/techniques_perceivable_flutter.md#captions-support-for-prerecorded-media-wcag-121-122---level-a)
* [iOS](../platforms/ios/techniques_perceivable_ios.md#captions-support-for-prerecorded-media-wcag-121-122---level-a)

### Audio Description or Media Alternative (WCAG 1.2.3 - Level A)

People that have vision disability may have issues with understanding the content of a video. To make the video accessible to all users, it is important to provide an audio description of the video content.

> This guideline with provided techniques covers the *1.2.3 Audio Description or Media Alternative (Prerecorded) - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_percievable_android.md#audio-description-or-media-alternative-wcag-123---level-a)
* [iOS](../platforms/ios/techniques_perceivable_ios.md#audio-description-or-media-alternative-wcag-123---level-a)

### Captions support for live media (WCAG 1.2.4 - Level AA)

In some cases, live media is used in the application. To make this content accessible to all users, it is important to provide captions for the live media.

> This guideline with provided techniques covers the *1.2.4 Captions (Live) - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_percievable_android.md#captions-support-for-live-media-wcag-124---level-aa)
* [iOS](../platforms/ios/techniques_perceivable_ios.md#captions-support-for-live-media-wcag-124---level-aa)

### Audio Description for Prerecorded Media (WCAG 1.2.5 - Level AA)

As a part of this guideline, it is important to provide an audio description for prerecorded video content.

> This guideline with provided techniques covers the *1.2.5 Audio Description (Prerecorded) - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_percievable_android.md#audio-description-for-prerecorded-media-wcag-125---level-aa)
* [iOS](../platforms/ios/techniques_perceivable_ios.md#audio-description-for-prerecorded-media-wcag-125---level-aa)

## Adaptable (WCAG 1.3)

Create content that can be presented differently without losing information or structure.

### Element information and relationship (WCAG 1.3.1 - Level A)

Every accessible element on the screen should hold information about itself, and it should be identifiable. From the web perspective, this is defined as a definition of the regions and elements on the page, while on the mobile side, this can be used to identify components or different areas of the page.

Moreover, when thinking about a given part of an application, it is important to make the layout structure logical and easy to use. With that in mind, semantic views that use accessibility features like VoiceOver may improve user experience. With that in hand goes the definition of the relationship, or connected elements (via container) – to give the user more context.

> This guideline with provided techniques covers the *1.3.1 Info and Relationships - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_percievable_android.md#element-information-and-relationship-wcag-131---level-a)
* [Flutter](../platforms/flutter/techniques_perceivable_flutter.md#element-information-and-relationship-wcag-131---level-a)
* [iOS](../platforms/ios/techniques_perceivable_ios.md#element-information-and-relationship-wcag-131---level-a)

### Meaningful sequence (WCAG 1.3.2 - Level A)

On iOS, screen elements are consumed from the top left to the bottom right. This is a standard way in which nearly all screens work correctly in most scenarios. Still, we should always provide the best experience to the user, even if elements are not structured in a preferred way.

> This guideline with provided techniques covers the *1.3.2 Meaningful Sequence - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_percievable_android.md#meaningful-sequence-wcag-132---level-a)
* [Flutter](../platforms/flutter/techniques_perceivable_flutter.md#meaningful-sequence-wcag-132---level-a)
* [iOS](../platforms/ios/techniques_perceivable_ios.md#meaningful-sequence-wcag-132---level-a)


### Sensory characteristics (WCAG 1.3.3 - Level A)

Instructions for understanding and operating content do not rely solely on sensory characteristics of components such as shape, color, size, visual location, orientation, or sound.

> This guideline with provided techniques covers the *1.3.3 Sensory characteristics - Level A of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_percievable_android.md#sensory-characteristics-wcag-133---level-a)
* [Flutter](../platforms/flutter/techniques_perceivable_flutter.md#sensory-characteristics-wcag-133---level-a)
* [iOS](../platforms/ios/techniques_perceivable_ios.md#sensory-characteristics-wcag-133---level-a)


### Orientation (WCAG 1.3.4 - Level AA)

Content should not be restricted to operation in a single display orientation, such as portrait or landscape, unless a specific display orientation is essential.

> This guideline with provided techniques covers the *1.3.4 Orientation - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_percievable_android.md#orientation-wcag-134---level-aa)
* [iOS](../platforms/ios/techniques_perceivable_ios.md#orientation-wcag-134---level-aa)


### Identify input purpose (WCAG 1.3.5 - Level AA)

In forms, every input field should indicate a purpose of the input for ease of use. With this guideline, the autocomplete feature should be added to the input fields, but the mobile platforms does not support that.

Still, to support this as much as possible, every input should at least define type of input (e.g., email, password, phone number, etc.).

> This guideline with provided techniques covers the *1.3.5 Identify Input Purpose - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_percievable_android.md#identify-input-purpose-wcag-135---level-aa)
* [iOS](../platforms/ios/techniques_perceivable_ios.md#identify-input-purpose-wcag-135---level-aa)


## Distinguishable (WCAG 1.4)

Make it easier for users to see and hear content including separating foreground from background.

### Use of Color (WCAG 1.4.1 - Level A)

Make sure that color isn't the only visual cue used for conveying information, indicating actions, prompting responses, or distinguishing elements. This is important to ensure that users with disabilities also have a clear and accessible understanding of the app's content.

> This guideline covers _1.4.1 Use of Color - Level A of the WCAG standard._

#### Implementation techniques
* [Android](../platforms/android/techniques_percievable_android.md#use-of-color-wcag-141---level-a)

### Audio control (WCAG 1.4.2 - Level A)

If any audio plays automatically for more than 3 seconds, there should be [an option to pause or stop the audio](https://developer.android.com/guide/topics/ui/accessibility/principles#media-content), or a way to adjust the audio volume independently from the overall system volume.

> This guideline covers _1.4.2 Audio control - Level A of the WCAG standard._

#### Implementation techniques
* [Android](../platforms/android/techniques_percievable_android.md#audio-control-wcag-142---level-a)

### Resizeable text (WCAG 1.4.4 - Level AA)

The text should be resizeable up to 200% without loss of content or functionality. This applies to every text content on the screen except captions and images of text.

> This guideline with provided techniques covers the **1.4.4 Resizeable Text - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_percievable_android.md#resizeable-text-wcag-144---level-aa)
* [iOS](../platforms/ios/techniques_perceivable_ios.md#resizeable-text-wcag-144---level-aa)


### Images of text (WCAG 1.4.5 - Level AA)

Where components with image of text are used, they cannot satisfy the other guidelines due to image constraints. E.g., the text in the image cannot be resized which breaks the guideline 1.4.4. To avoid that, use of images of text should be avoided, or at least a text alternative should be provided.

This does not affect components which are essential for the functionality of the application, like logos or branding images.

> This guideline with provided techniques covers the *1.4.5 Images of Text - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_percievable_android.md#images-of-text-wcag-145---level-aa)
* [iOS](../platforms/ios/techniques_perceivable_ios.md#images-of-text-wcag-145---level-aa)


### Reflow (WCAG 1.4.10 - Level AA)

The reflow is basically another name to responsible design in this context. The content should be able to reflow from one screen size to another without losing information or functionality.

> This guideline with provided techniques covers the *1.4.10 Reflow - Level AA of the WCAG standard.*

#### Implementation techniques
* [Android](../platforms/android/techniques_percievable_android.md#reflow-wcag-1410---level-aa)
* [iOS](../platforms/ios/techniques_perceivable_ios.md#reflow-wcag-1410---level-aa)


### Text Spacing (WCAG - 1.4.12 - Level AA)

To ensure consistent accessibility, these text spacing requirements should be incorporated directly into design specifications. Designers and developers should collaborate to confirm that the line height, paragraph spacing, letter spacing, and word spacing meet the standards across all text elements.

#### Implementation techniques
* [Android](../platforms/android/techniques_percievable_android.md#text-spacing-wcag---1412---level-aa)

## Other perceivable guidelines

This section contains guidelines that may not applicable for the mobile platforms, or its criteria is a not the responsibility of the mobile team. Still, take into account that those guidelines needs to be satisfied.

* [Contrast (Minimum) (WCAG 1.4.3 - Level AA)](https://www.w3.org/WAI/WCAG22/quickref/#contrast-minimum)
* [Non-text Contrast (WCAG 1.4.11 - Level AA)](https://www.w3.org/WAI/WCAG22/quickref/#non-text-contrast)
* [Content on Hover or Focus (WCAG 1.4.13 - Level AA)](https://www.w3.org/WAI/WCAG22/quickref/#content-on-hover-or-focus)

⎯

[← Understandable](understandable_principle.md) | [Testing accessibility →](../accessibility_testing.md)
