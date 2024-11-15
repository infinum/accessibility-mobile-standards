[⬅️ Principles](../accessibility_principles.md)

# 1. Perceivable principle

Information and user interface components must be presentable to users in ways they can perceive.

## 1.1 Text alternatives

Provide text alternatives for any non-text content to be changed into other forms people need, such as large print, braille, speech, symbols, or more straightforward language.

### 1.1.1 Non-text content (Level A)

When talking about the screen elements, it is important to make information about all elements accessible and available. Some elements may not have text included by design or as a default user interface component. This can be seen when buttons are used with icons only, images, or other decorative elements.

Some users may have issues identifying an element's functionality or description in general, and because of that, it is important to define non-text elements by accessibility features.

> This guideline with provided techniques covers the *1.1.1 Non-text Content - Level A of the WCAG standard.*

**Techniques**\
[Android](../platforms/android/techniques_percievable_android.md#111-non-text-content-level-a), [iOS](../platforms/ios/techniques_perceivable_ios.md#111-non-text-content-level-a), [Flutter](../platforms/flutter/techniques_perceivable_flutter.md#111-non-text-content-level-a)

## 1.2 Time-based Media

Provide alternatives for time-based media.

### 1.2.1-1.2.2 Captions support for prerecorded media (Level A)

Due to some disabilities, some users may not be able to hear the content of the media provided by the application. An example of that can be a prerecorded audio or video track. In some cases, it is necessary to add support for some accessibility features to make this content accessible to all users.

> This guideline with provided techniques covers the *1.2.1 Audio-only and Video-only (Prerecorded) - Level A and 1.2.2 Captions (Prerecorded) - Level A of the WCAG standard.*

**Techniques**\
[Android](../platforms/android/techniques_percievable_android.md#121-122-captions-support-for-prerecorded-media-level-a), [iOS](../platforms/ios/techniques_perceivable_ios.md#121-122-captions-support-for-prerecorded-media-level-a), [Flutter](../platforms/flutter/techniques_perceivable_flutter.md#121-122-captions-support-for-prerecorded-media-level-a)

### 1.2.3 Audio Description or Media Alternative (Level A)

People that have vision disability may have issues with understanding the content of a video. To make the video accessible to all users, it is important to provide an audio description of the video content.

> This guideline with provided techniques covers the *1.2.3 Audio Description or Media Alternative (Prerecorded) - Level A of the WCAG standard.*

**Techniques**\
[Android](../platforms/android/techniques_percievable_android.md#123-audio-description-or-media-alternative-level-a), [iOS](../platforms/ios/techniques_perceivable_ios.md#123-audio-description-or-media-alternative-level-a)

### 1.2.4 Captions support for live media (Level AA)

In some cases, live media is used in the application. To make this content accessible to all users, it is important to provide captions for the live media.

> This guideline with provided techniques covers the *1.2.4 Captions (Live) - Level AA of the WCAG standard.*

**Techniques**\
[Android](../platforms/android/techniques_percievable_android.md#124-captions-support-for-live-media-level-aa), [iOS](../platforms/ios/techniques_perceivable_ios.md#124-captions-support-for-live-media-level-aa)

### 1.2.5 Audio Description for Prerecorded Media (Level AA)

As a part of this guideline, it is important to provide an audio description for prerecorded video content.

> This guideline with provided techniques covers the *1.2.5 Audio Description (Prerecorded) - Level AA of the WCAG standard.*

**Techniques**\
[Android](../platforms/android/techniques_percievable_android.md#125-audio-description-for-prerecorded-media-level-aa), [iOS](../platforms/ios/techniques_perceivable_ios.md#125-audio-description-for-prerecorded-media-level-aa)

## 1.3 Adaptable

Create content that can be presented differently without losing information or structure.

### 1.3.1 Element information and relationship (Level A)

Every accessible element on the screen should hold information about itself, and it should be identifiable. From the web perspective, this is defined as a definition of the regions and elements on the page, while on the mobile side, this can be used to identify components or different areas of the page.

Moreover, when thinking about a given part of an application, it is important to make the layout structure logical and easy to use. With that in mind, semantic views that use accessibility features like VoiceOver may improve user experience. With that in hand goes the definition of the relationship, or connected elements (via container) – to give the user more context.

> This guideline with provided techniques covers the *1.3.1 Info and Relationships - Level A of the WCAG standard.*

**Techniques**\
[Andriod](../platforms/android/techniques_percievable_android.md#131-element-information-and-relationship-level-a), [iOS](../platforms/ios/techniques_perceivable_ios.md#131-element-information-and-relationship-level-a), [Flutter](../platforms/flutter//techniques_perceivable_flutter.md#131-element-information-and-relationship-level-a)

### 1.3.2 Meaningful sequence (Level A)

On iOS, screen elements are consumed from the top left to the bottom right. This is a standard way in which nearly all screens work correctly in most scenarios. Still, we should always provide the best experience to the user, even if elements are not structured in a preferred way.

> This guideline with provided techniques covers the *1.3.2 Meaningful Sequence - Level A of the WCAG standard.*

**Techniques**\
[Andriod](../platforms/android/techniques_percievable_android.md#132-meaningful-sequence-level-a), [iOS](../platforms/ios/techniques_perceivable_ios.md#132-meaningful-sequence-level-a), [Flutter](../platforms/flutter//techniques_perceivable_flutter.md#132-meaningful-sequence-level-a)


### 1.3.3 Sensory characteristics (Level A)

Instructions for understanding and operating content do not rely solely on sensory characteristics of components such as shape, color, size, visual location, orientation, or sound.

> This guideline with provided techniques covers the *1.3.3 Sensory characteristics - Level A of the WCAG standard.*

**Techniques**\
[Andriod](../platforms/android/techniques_percievable_android.md#133-sensory-characteristics-level-a), [iOS](../platforms/ios/techniques_perceivable_ios.md#133-sensory-characteristics-level-a), [Flutter](../platforms/flutter//techniques_perceivable_flutter.md#133-sensory-characteristics-level-a)


### 1.3.4 Orientation (Level AA)

Content should not be restricted to operation in a single display orientation, such as portrait or landscape, unless a specific display orientation is essential.

> This guideline with provided techniques covers the *1.3.4 Orientation - Level AA of the WCAG standard.*

**Techniques**\
[Andriod](../platforms/android/techniques_percievable_android.md#134-orientation-level-aa), [iOS](../platforms/ios/techniques_perceivable_ios.md#134-orientation-level-aa)


### 1.3.5 Identify input purpose (Level AA)

In forms, every input field should indicate a purpose of the input for ease of use. With this guideline, the autocomplete feature should be added to the input fields, but the mobile platforms does not support that.

Still, to support this as much as possible, every input should at least define type of input (e.g., email, password, phone number, etc.).

> This guideline with provided techniques covers the *1.3.5 Identify Input Purpose - Level AA of the WCAG standard.*

**Techniques**\
[Andriod](../platforms/android/techniques_percievable_android.md#135-identify-input-purpose-level-aa), [iOS](../platforms/ios/techniques_perceivable_ios.md#135-identify-input-purpose-level-aa)


## 1.4 Distinguishable

Make it easier for users to see and hear content including separating foreground from background.

### 1.4.1 Use of Color (Level A)

Make sure that color isn't the only visual cue used for conveying information, indicating actions, prompting responses, or distinguishing elements. This is important to ensure that users with disabilities also have a clear and accessible understanding of the app's content.

> This guideline covers _1.4.1 Use of Color - Level A of the WCAG standard._

**Techniques**\
[Andriod](../platforms/android/techniques_percievable_android.md#141-use-of-color-level-a)


### 1.4.2 Audio control (Level A)

If any audio plays automatically for more than 3 seconds, there should be [an option to pause or stop the audio](https://developer.android.com/guide/topics/ui/accessibility/principles#media-content), or a way to adjust the audio volume independently from the overall system volume.

> This guideline covers _1.4.2 Audio control - Level A of the WCAG standard._

**Techniques**\
[Andriod](../platforms/android/techniques_percievable_android.md#142-audio-control-level-a)


### 1.4.4 Resizeable text (Level AA)

The text should be resizeable up to 200% without loss of content or functionality. This applies to every text content on the screen except captions and images of text.

> This guideline with provided techniques covers the **1.4.4 Resizeable Text - Level AA of the WCAG standard.*

**Techniques**\
[Andriod](../platforms/android/techniques_percievable_android.md#144-resizeable-text-level-aa), [iOS](../platforms/ios/techniques_perceivable_ios.md#144-resizeable-text-level-aa)


### 1.4.5 Images of text (Level AA)

Where components with image of text are used, they cannot satisfy the other guidelines due to image constraints. E.g., the text in the image cannot be resized which breaks the guideline 1.4.4. To avoid that, use of images of text should be avoided, or at least a text alternative should be provided.

This does not affect components which are essential for the functionality of the application, like logos or branding images.

> This guideline with provided techniques covers the *1.4.5 Images of Text - Level AA of the WCAG standard.*

**Techniques**\
[Andriod](../platforms/android/techniques_percievable_android.md#145-images-of-text-level-aa), [iOS](../platforms/ios/techniques_perceivable_ios.md#145-images-of-text-level-aa)


### 1.4.10 Reflow (Level AA)

The reflow is basically another name to responsible design in this context. The content should be able to reflow from one screen size to another without losing information or functionality.

> This guideline with provided techniques covers the *1.4.10 Reflow - Level AA of the WCAG standard.*

**Techniques**\
[Andriod](../platforms/android/techniques_percievable_android.md#1410-reflow-level-aa), [iOS](../platforms/ios/techniques_perceivable_ios.md#1410-reflow-level-aa)


### 1.4.12 Text Spacing (Level AA)

To ensure consistent accessibility, these text spacing requirements should be incorporated directly into design specifications. Designers and developers should collaborate to confirm that the line height, paragraph spacing, letter spacing, and word spacing meet the standards across all text elements.

**Techniques**\
[Andriod](../platforms/android/techniques_percievable_android.md#1412-text-spacing-level-aa)


## Other perceivable guidelines

This section contains guidelines that may not applicable for the mobile platforms, or its criteria is a not the responsibility of the mobile team. Still, take into account that those guidelines needs to be satisfied.

* [1.4.3 Contrast (Minimum) (Level AA)](https://www.w3.org/WAI/WCAG22/quickref/#contrast-minimum)
* [1.4.11 Non-text Contrast (Level AA)](https://www.w3.org/WAI/WCAG22/quickref/#non-text-contrast)
* [1.4.13 Content on Hover or Focus (Level AA)](https://www.w3.org/WAI/WCAG22/quickref/#content-on-hover-or-focus)

⎯

[← Principles](../accessibility_principles.md) | [Operable →](operable_principle.md)
