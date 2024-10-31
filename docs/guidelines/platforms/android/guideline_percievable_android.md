 [🔼 Accessibility principles and examples](../../principles/accessibility_principles_and_examples.md  "Accessibility principles and examples") | [⬅️ Perceivable principle](../../principles/perceivable_principle.md "Perceivable principle")
# Perceivable guidelines for Android

All content displayed on the screen at some point must be presented to the user in a perceivable manner.

## Text alternatives

Provide text alternatives for any non-text content so that it can be changed into other forms people need, such as large print, braille, speech, symbols or simpler language.

*This guideline covers point 1.1.1 Non-text Content - Level A of the WCAG standard.*

:white_check_mark: **Success criteria**

### Non-text context

Each UI element should include a description that describes its purpose. All elements presented on the screen must have the description provided, especially the ones that are important for the screen’s functionality. That way, screen readers such as TalkBack can announce these labels to users who rely on these services.

If an element exists on the UI only for decorative purposes it is recommended that you set its `contentDescription` to "null" or `android:importantForAccessibility` to "no" for devices running Android 4.1 and higher.

:no_entry_sign: **Failure criteria**

- Not providing descriptions of elements presented on the screen that do not exist only for decorative purposes

---

## Time-based Media (WCAG 1.2)

Provide alternatives for time-based media.

### Captions support for prerecorded media (WCAG 1.2.1 and 1.2.2 - Level A)

This guideline addresses [1.2.1 Audio-only and Video-only (Prerecorded) - Level A](https://www.w3.org/WAI/WCAG22/quickref/#audio-only-and-video-only-prerecorded) and [1.2.2 Captions (Prerecorded) - Level A](https://www.w3.org/WAI/WCAG22/quickref/#captions-prerecorded) from the WCAG standard.

Some users have disabilities that prevent them from hearing media content in an application, such as prerecorded audio or video. To ensure this content is accessible to everyone, techniques like adding captions must be incorporated. This ensures all users, regardless of hearing ability, can fully engage with the media.

:white_check_mark: **Success criteria**

One way to enhance accessibility is by adding captions, either open or closed. Open captions are permanently visible as they are integrated into the video, while closed captions require a media format with a player that supports them. Most modern video players support captions, and `ExoPlayer` provides built-in support for displaying them automatically.

##### Using ExoPlayer with captions

To view captions in media that supports them, users must enable the _Show captions_ option. This accessibility feature can be found under **Settings** > **Accessibility** > **Caption preferences**. On this screen, users can also adjust caption size and style; however, these preferences may not work with media apps that don’t support Caption Preferences.

##### Custom solution

If a different player is used instead of `ExoPlayer`, the status of closed captions, along with the font scale and caption style, can be checked programmatically using the [CaptioningManager](https://developer.android.com/reference/android/view/accessibility/CaptioningManager). When the _Show captions_ option is enabled, captions should be turned on in the selected player.

```kotlin
import android.content.Context
import android.view.accessibility.CaptioningManager
import android.view.accessibility.CaptioningManager.CaptionStyle

class CaptionUtils(context: Context) {
    
   private val captioningManager: CaptioningManager =
       context.getSystemService(Context.CAPTIONING_SERVICE) as CaptioningManager
    
   fun areCaptionsEnabled(): Boolean = captioningManager.isEnabled
    
   fun getCaptionFontScale(): Float = captioningManager.fontScale
    
   fun getCustomCaptionStyle(): CaptionStyle = captioningManager.userStyle
}
```

### Audio Description or Media Alternative (WCAG 1.2.3 - Level A)

This guideline covers point [1.2.3 Audio Description or Media Alternative (Prerecorded) - Level A](https://www.w3.org/WAI/WCAG22/quickref/#audio-description-or-media-alternative-prerecorded) of the WCAG standard.

People with vision impairments may have difficulty understanding key visual details in a video. To make the video accessible to everyone, the guideline requires providing an audio description or an alternative method to convey the visual information.

:white_check_mark: **Success criteria**

To satisfy the guideline, there are two ways to make synchronized media accessible for users with vision impairments:
* **Provide an audio description**: Add narration to describe key visual elements (e.g., actions, scenery) in the video that someone with vision impairments would otherwise miss.
* **Provide a text alternative**: If audio description isn't possible, offer a transcript that includes descriptions of both the audio and visual content, allowing users to read what happens in the video.

#### Using audio description
Check [Audio Description for Prerecorded Media (WCAG 1.2.5 - Level AA)](#audio-description-for-prerecorded-media-wcag-125---level-aa) for more information.

#### Using text alternative

A text alternative provides a written description of both the audio and visual content. This is helpful for users who cannot see the video or for those who cannot access the audio.
* **Static text alternative**: For simple videos (like a "talking-head" video, where only a person speaks to the camera), a brief text description can be provided instead of a full audio description.
* **Detailed transcript**: For more complex videos, a full transcript can include descriptions of visual elements as well as the dialogue.

:no_entry_sign: **Failure criteria**

If none of provided success criteria are met, the user may have issues understanding the content of the video. This can lead to a bad user experience and a lack of information, and in the end, the failure of this guideline.

### Captions support for live media (WCAG 1.2.4 - Level AA)

This guideline covers [1.2.4 Captions (Live) - Level AA](https://www.w3.org/WAI/WCAG22/quickref/#captions-live) of the WCAG standard.

In some cases, live media is used in the application. To ensure accessibility for all users, providing captions for live content is important.

:white_check_mark: **Success criteria**

All live media in the application should offer captions through the user interface, available as either open or closed captions. For two-way multimedia calls between individuals, accessibility requirements are the responsibility of content providers, not the application.

- **Open captions**: Captions are embedded directly into the live media and always visible to viewers.
- **Closed captions**: Captions are available in the live media stream and can be programmatically toggled on or off by the user.

The second approach is more customizable and can offer more flexibility than embedded captions, though it requires additional client-side work. For further details, please refer to the [Captions support for prerecorded media (WCAG 1.2.1 and 1.2.2 - Level A) section](#captions-support-for-prerecorded-media-wcag-121-and-122---level-a) and the [ExoPlayer documentation on live streaming](https://developer.android.com/media/media3/exoplayer/live-streaming), which provides more information about HTTP Live Streaming (HLS) on the Android platform.

### Audio Description for Prerecorded Media (WCAG 1.2.5 - Level AA)

This guideline covers [1.2.5 Audio Description (Prerecorded) - Level AA](https://www.w3.org/WAI/WCAG22/quickref/#audio-description-prerecorded) of the WCAG standard.

As a part of this guideline, it is important to provide an audio description for prerecorded video content.

:white_check_mark: **Success criteria**

This can be done by:
* adding a separate audio track to the video that describes the video content
* providing a video version file with audio description
* providing a video with extended audio description

This guideline closely aligns with the [Audio Description or Media Alternative (WCAG 1.2.3 - Level A)](#audio-description-or-media-alternative-wcag-123---level-a), which states that video content must include an audio description. Unlike the previous guideline, which allows for alternatives, this requirement emphasizes the need for a dedicated audio track that describes the video content.

**Note**: Based on the guideline itself, if all of the information in the video track is already provided in the audio track, no audio description is necessary. This applies to both guidelines (1.2.3 and 1.2.5).

##### Audio description with ExoPlayer

In `ExoPlayer`, you can query the available audio and video tracks using `player.currentTracks`. This allows you to present users with options, such as regular audio and an audio description track. You can implement functionality for users to select their preferred track from the available options.

---

## Adaptable

Create content that can be presented in different ways without losing information or structure.

### Info and Relationships

Information, structure, and relationships conveyed through presentation are available in text.

*This guideline covers point 1.3.1 Info and Relationships - Level A of the WCAG standard.*

:white_check_mark: **Success criteria**

- Groups of related content

If multiple UI elements that form a natural group should be displayed on the screen, it is recommended to arrange these elements within a container which is usually a subclass of ViewGroup. Also, you should set the container object's `android:screenReaderFocusable` (for devices running Android 8.1. – API level 27) or `android:focusable` to true. Furthermore, you should set `android:focusable` attribute of each inner object to false because doing so will make accessibility services present the inner element's content descriptions, one after the other, in a single announcement.

Grouping elements based on the context helps users that benefit from using accessibility services to discover the information that is on the screen more efficiently.

**Code example:**

```
<!-- In response to a single user interaction, accessibility services announce
     both the title and the artist of the song. -->
<ConstraintLayout
    android:id="@+id/song_data_container" ...
    android:screenReaderFocusable="true">

    <TextView
        android:id="@+id/song_title" ...
        android:focusable="false"
        android:text="@string/my_song_title" />
    <TextView
        android:id="@+id/song_artist"
        android:focusable="false"
        android:text="@string/my_songwriter" />
</ConstraintLayout>
```

_Note:_ In cases like this, it is recommended to define content descriptions as concisely as possible, considering that accessibility services will read them one after the other.

- Custom group label

It is possible to override the platform's default grouping and ordering of a group's inner element descriptions by providing a content description for the group itself.

**Code example:**

```
<!-- In response to a single user interaction, accessibility services announce the custom content description for the group. -->
<ConstraintLayout
android:id="@+id/song_data_container" ...
android:screenReaderFocusable="true"
android:contentDescription="@string/title_artist_best_song">

    <TextView
        android:id="@+id/song_title" ...

        <!-- Content ignored by accessibility services -->
        android:text="@string/my_song_title" />
    <TextView
        android:id="@+id/song_artist"

        <!-- Content ignored by accessibility services -->
        android:text="@string/my_songwriter" />
</ConstraintLayout>
```

- Nested groups

If the app you are building provides multi-dimensional information, it is recommended to use the `android:screenReaderFocusable` attribute on the inner group containers. That kind of grouping and labeling will provide a good balance between the number of announcements needed to discover the screen's content and the length of each announcement.

**Code example:**

```
<!-- In response to a single user interaction, accessibility services announce the events for a single stage only. -->
<ConstraintLayout
    android:id="@+id/festival_event_table" ... >
    <ConstraintLayout
        android:id="@+id/stage_a_event_column"
        android:screenReaderFocusable="true">

        <!-- UI elements that describe the events on Stage A. -->

    </ConstraintLayout>
    <ConstraintLayout
        android:id="@+id/stage_b_event_column"
        android:screenReaderFocusable="true">

        <!-- UI elements that describe the events on Stage B. -->

    </ConstraintLayout>
</ConstraintLayout>
```

- Headings within text

It is also possible to use _headings_ to summarize groups of text that appear on the screen. To mark a view to be treated as a heading, you can set `android:accessibilityHeading` to true.

That way, users of accessibility services can choose to navigate between headings instead of navigating between paragraphs or between words which can improve the text navigation experience.

:no_entry_sign: **Failure criteria**

- It is not clear which parts of the screen are contextually connected.

---

### Meaningful sequence

*This guideline covers point 1.3.2 Meaningful sequence - Level A of the WCAG standard.*

:white_check_mark: **Success criteria**

If the order of the content displayed on the screen is crucial for understanding, it is very important to make sure it will be presented in the same order when using accessibility services. That way, users of accessibility services (such as TalkBack) can get a clearer picture of the content and possible actions on the current screen that is being navigated through.

The best solution should be a full-screen redesign with the correct and logical traversal order. If that is not an option, on apps with minSdk >= 22, setting `android:accessibilityTraversalBefore` or `android:accessibilityTraversalAfter` attributes could help create a new order of displayed views that will make a bit more sense to TalkBack users.

An example of using `android:accessibilityTraversalBefore` or `android:accessibilityTraversalAfter` attributes is given down below:

```
<Button
    android:id="@+id/button1"
    ... />
<Button
    android:id="@id/button2"
    android:accessibilityTraversalAfter="@id/button3"
    ... />
<Button
    android:id="@id/button3"
    ...  />
```

_Note 2. Always make sure to define `android:accessibilityTraversalBefore` or `android:accessibilityTraversalAfter` attributes in a way that does not create any loops or traps that will prevent users from interacting with all relevant views displayed on the screen._

In apps with minSdk < 22, traversal order can be defined programmatically using ViewCompat.

The example is given below:

```
ViewCompat.setAccessibilityDelegate(button1, object : AccessibilityDelegateCompat() {
    override fun onInitializeAccessibilityNodeInfo(host: View?, info: AccessibilityNodeInfoCompat?) {
        super.onInitializeAccessibilityNodeInfo(host, info)
        info?.setTraversalAfter(button2)
    }
})
```

:no_entry_sign: **Failure criteria**

- Views displayed on the screen break consistency of the navigation.

---

### Sensory characteristics (WCAG 1.3.3 - Level A)

Instructions for using content should avoid relying exclusively on sensory characteristics such as shape, color, size, visual position, orientation, or sound cues. Instead, ensure they include descriptive text or additional indicators that make the content understandable to users of all abilities.

> This guideline covers _1.3.3 Sensory characteristics - Level A of the WCAG standard._

:white_check_mark: **Success technique(s)**

To ensure our app is fully accessible to all users, we should avoid relying on a single characteristic to display elements on the screen.

**Example:**

If the action on the screen depends on the button of a particular shape (e.g., "To submit the form press on the round button"), it is recommended to provide additional cues about the button's purpose.
For example, adding a `check sign` to the button that will be appropriately labeled so users using accessibility services will be able to identify the targeted button more easily ("To submit the form press on the round check button").

That way, users with visual impairments will be able to understand the button's purpose even if they can't see its shape.

:no_entry_sign: **Failures**

- Designing elements that are hard to distinguish and rely on only one characteristic to be visible on the screen.

_Important to note is that this guideline primarily depends on accessible design._

---

#### Sources

- [Google Support Page](https://support.google.com/accessibility/android)
- [Official Documentation](https://developer.android.com/guide/topics/ui/accessibility)

---

[← Perceivable principle](../../principles/perceivable_principle.md "Perceivable principle")
