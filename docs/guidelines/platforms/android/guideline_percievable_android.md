 [🔼 Accessibility principles and examples](../../principles/accessibility_principles_and_examples.md  "Accessibility principles and examples") | [⬅️ Perceivable principle](../../principles/perceivable_principle.md "Perceivable principle")
# Perceivable guidelines for Android

All content displayed on the screen at some point must be presented to the user in a perceivable manner.

## Text alternatives (WCAG 1.1)

Provide text alternatives for any non-text content so that it can be changed into other forms people need, such as large print, braille, speech, symbols or simpler language.

### Non-text content identification (WCAG 1.1.1 - Level A)

When talking about the screen elements, it is important to make information about all elements accessible and available. Some elements may not have text included by design or as a default user interface component. This can be seen when buttons are used with icons only, images, or other decorative elements.

Some users may have issues identifying an element's functionality or description in general, and because of that, it is important to define non-text elements by accessibility features.

✅ **Success criteria**

Each UI element should include a description that describes its purpose. All elements presented on the screen must have the description provided, especially the ones that are important for the screen’s functionality. That way, screen readers such as TalkBack can announce these labels to users who rely on these services.

Set `contentDescription` attribute to non-decorative elements. The labels need to be localized, so make sure to use string resources.

```xml
<string name='copy'>Copy</string>

<ImageView
    ...
    android:contentDescription="@string/copy"/>
```

If an element exists only for decorative purposes, it is recommended that you set its `contentDescription` to `null` or `android:importantForAccessibility` to `no` for devices running Android 4.1 and higher.

In Compose, use the `contentDescription` parameter to set the description. Some Composables do not offer it as a parameter, in which case it can also be set through `semantics`.


```kotlin
@Composable
private fun CopyButton(onClick: () -> Unit) {
    IconButton(onClick = onClick) {
        Icon(
            imageVector = Icons.Filled.Copy,
            contentDescription = stringResource(R.string.copy)
        )
    }
}

@Composable
private fun MyCustomButton(onClick: () -> Unit) {
    val copyDescription = stringResource(R.string.copy)
    Canvas(modifier = Modifier
        .clickable { onClick() }
        .semantics { contentDescription = copyDescription }
    ) { ... }
}
```

🚫 **Failure criteria**

- Not providing descriptions of elements presented on the screen that do not exist only for decorative purposes.
- Setting content description to non-functional or decorative elements. In those cases, labeling the elements may confuse the user and should be avoided.

---

## Time-based Media (WCAG 1.2)

Provide alternatives for time-based media.

### Captions support for prerecorded media (WCAG 1.2.1 and 1.2.2 - Level A)

This guideline addresses [1.2.1 Audio-only and Video-only (Prerecorded) - Level A](https://www.w3.org/WAI/WCAG22/quickref/#audio-only-and-video-only-prerecorded) and [1.2.2 Captions (Prerecorded) - Level A](https://www.w3.org/WAI/WCAG22/quickref/#captions-prerecorded) from the WCAG standard.

Some users have disabilities that prevent them from hearing media content in an application, such as prerecorded audio or video. To ensure this content is accessible to everyone, techniques like adding captions must be incorporated. This ensures all users, regardless of hearing ability, can fully engage with the media.

#### ✅ Success technique(s)

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

##### 🚫 Failures

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

### Info and Relationships (WCAG 1.3.1 - Level A)

Information, structure, and relationships conveyed through presentation are available in text. Important information and element relationship should be preserved when the presentation format changes (e.g. read out by a screen reader).

#### Element information

Every accessible element on the screen should hold information about itself and should be identifiable by the user. In addition to visual cues (e.g. using bigger font for headings), relevant information needs to be provided in such a way that it is also accessible to assistive technologies, such as TalkBack.

✅ **Success criteria**

The most important technique for achieving this criteria is properly labeling all of the elements on the screen, i.e. giving them a proper name and a role (heading, button, switch, edit text, etc.). In that way, no important information is lost when the user relies only on the auditory information read out by TalkBack and it is much easier to understand the purpose of an element on the screen.

The techniques for adding names and roles to elements can be found in the [Name, Role, Value chapter](guideline_robust_android.md#name-role-value-wcag-412---level-a).

🚫 **Failure criteria**
- The purpose of an element on the screen is conveyed only through visual cues, and completely lost when using assistive technologies.
    - For example, using a clickable image as a toggle without setting any accessibility information. TalkBack will only announce that the element is clickable, but all other information regarding its behavior or state (e.g. the element being toggleable) is lost.

---

#### Element relationships

Many UI components should work together to create a context for the user. For example, if there is a list of components with two labels inside, one with a title and another for the value, it may be suitable to read those two labels as one sentence to give more context. Additionally, it is important to know how elements relate to one another.

✅ **Success criteria**

When there are multiple elements that are connected, this connection needs to be clear when using assistive technologies. For example, in the case of an input field which has a label above it and an error text below it, the user needs to be aware that those two text labels are connected to this specific input field.

This can be achieved by following the [Labels or instruction](guideline_understandable_android.md#labels-or-instructions-wcag-332---level-a) and [Error identification](guideline_understandable_android.md#error-identification-wcag-331---level-a) guidelines.

If multiple UI elements that form a natural group should be displayed on the screen, it is recommended to arrange these elements within a container which is usually a subclass of `ViewGroup`. Also, you should set the container object's `android:screenReaderFocusable` (for devices running Android 8.1. – API level 27) or `android:focusable` to `true`. Furthermore, you should set `android:focusable` attribute of each inner object to `false` because doing so will make accessibility services present the inner element's content descriptions, one after the other, in a single announcement.

Grouping elements based on the context helps users that benefit from using accessibility services to discover the information that is on the screen more efficiently.

**Code example:**

```xml
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

In Compose, the same can be achieved using the `mergeDescendants` parameter:
```kotlin
@Composable
private fun SongCard(title: String, artist: String) {
    Column(modifier = Modifier.semantics(mergeDescendants = true) {}) {
        Text(title)
        Text(artist)
    }
}
```

_Note 1:_ In cases like these, it is recommended to define content descriptions as concisely as possible, considering that accessibility services will read them one after the other.

_Note 2:_ It is also possible to define a `contentDescription` for the whole group, in which case the descriptions of the children will be ignored. But setting the description for the whole group by aggregating the descriptions of its descendants is not advised, as it is error-prone. For example, if any of the descendants' text changes, the group description will not be updated automatically, as explained in the [Developer documentation](https://developer.android.com/guide/topics/ui/accessibility/principles#content-groups).

- Nested groups

If the app you are building provides multi-dimensional information, it is recommended to use the `android:screenReaderFocusable` attribute on the inner group containers. That kind of grouping and labeling will provide a good balance between the number of announcements needed to discover the screen's content and the length of each announcement.

**Code example:**

```xml
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

In Compose, nested groups can be merged in a similar way

```kotlin
@Composable
fun FestivalEventTable() {
    Row {
        Column(modifier = Modifier.semantics(mergeDescendants = true) { }) {
            // UI elements that describe the events on Stage A
        }

        Column(modifier = Modifier.semantics(mergeDescendants = true) { }) {
            // UI elements that describe the events on Stage B
        }
    }
}
```

🚫 **Failure criteria**

- It is not clear which parts of the screen are contextually connected.

---

### Meaningful sequence (WCAG 1.3.2 - Level A)

If the order of the content displayed on the screen is crucial for understanding, it is very important to make sure it will be presented in the same order when using accessibility services. That way, users of accessibility services (such as TalkBack) can get a clearer picture of the content and possible actions on the current screen that is being navigated through.

✅ **Success criteria**

By default, screen elements are read out from the top left to the bottom right. This is a standard way in which nearly all screens work correctly in most scenarios. In the occasions where that is not sufficient, a full-screen redesign with the correct logical and traversal order should be considered. If that is not an option, the traversal order can be modified manually.

On apps with minSdk >= 22, setting `android:accessibilityTraversalBefore` or `android:accessibilityTraversalAfter` attributes could help create a new order of displayed views that will make a bit more sense to TalkBack users.

An example of using `android:accessibilityTraversalBefore` or `android:accessibilityTraversalAfter` attributes is given down below:

```xml
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

In some cases, it might happen that a `View` ignores the statically set property (for example, this problem was observed with `ComposeView`). If that happens, the traversal order can be defined programmatically using `ViewCompat`. It is also the only way to define it in apps with minSdk < 22:

```kotlin
ViewCompat.setAccessibilityDelegate(
    button2,
    object : AccessibilityDelegateCompat() {
        override fun onInitializeAccessibilityNodeInfo(host: View?, info: AccessibilityNodeInfoCompat) {
            super.onInitializeAccessibilityNodeInfo(host, info)
            info.setTraversalAfter(button3)
        }
    }
)
```

In Compose, the same can be achieved using `isTraversalGroup` alone or in conjunction with `traversalIndex` semantics.

Traversal groups identify semantically important groups, so that all children of the node are visited before moving to other elements. This can be useful when arranging elements inside a layout that is not a traversal group by default, and does not necessarily output the elements in a linear manner, such as a `Box`.

```kotlin
@Composable
fun CardBox(
    topSampleText: String,
    bottomSampleText: String,
    modifier: Modifier = Modifier
) {
    Box(modifier) {
        Column {
            Text(topSampleText)
            Text(bottomSampleText)
        }
    }
}

@Composable
fun TraversalGroupDemo() {
    val topSampleText1 = "This sentence is in "
    val bottomSampleText1 = "the left column."
    val topSampleText2 = "This sentence is "
    val bottomSampleText2 = "on the right."
    
    Row {
        CardBox(
            topSampleText1,
            bottomSampleText1,
            Modifier.semantics { isTraversalGroup = true }
        )
        CardBox(
            topSampleText2,
            bottomSampleText2,
            Modifier.semantics { isTraversalGroup = true }
        )
    }

}
```

Had `isTraversalGroup` not been set to `true`, the reading order of the Composables would be "This sentence is in" -> "This sentence is" -> "the left column" -> "on the right".

When that is not enough, the `traversalIndex` float can be used in conjunction with traversal groups to modify the order further. Elements with lower `traversalIndex` are prioritized first when in the same traversal group, the default value is `0f` and the values can be negative.

Be wary that sometimes all elements of a traversal group will need to have a defined `traversalIndex` to be read in the correct order (and/or grouped into smaller traversal groups), since there is no relative traversal before/after property as in XML. This can be error-prone and difficult to maintain, so the `traversalIndex` approach should be used only as a last resort.

```kotlin
@Composable
fun ButtonsScreen() {
    Column {
        // Traversal index not needed - 0f by default
        Button {
            Text("Button 1")
        }
        Button(modifier = Modifier.semantics { traversalIndex = 2f }) {
            Text("Button 2")
        }
        Button(modifier = Modifier.semantics { traversalIndex = 1f }) {
            Text("Button 3")
        }
    }
}
```

_**Note.** When modifying the traversal order, make sure that it is done in a way that does not create any loops or traps that will prevent users from interacting with all relevant views displayed on the screen._

🚫 **Failure criteria**

- Elements displayed on the screen break consistency of the navigation. For example, having sudden jumps to unrelated components in the middle of a sequence of similar elements.

---

### Sensory characteristics

*This guideline covers point 1.3.3 Sensory characteristics - Level A of the WCAG standard.*

#### ✅ Success technique(s)

The content provided in your app must be easily understandable to all users. That is why it is recommended to use cues or symbols rather than colors to distinguish different views and different actions that those views provide. That way, users with color vision deficiencies could also easily understand the whole UI.

##### 🚫 Failures

- An important difference between elements is stressed only with colors.

---

## Distinguishable (WCAG 1.4)

### Resizeable text (WCAG 1.4.4 - Level AA)

The text should be resizeable up to 200% without loss of content or functionality. This applies to every text content on the screen except captions and images of text.


#### ✅ Success technique(s)

Mobile apps must ensure that text can be resized up to **200%** without loss of content or functionality. This is essential for users with low vision who need larger text for readability. Specifically:

- Text should be resizable up to **200%** using the device’s text size settings.
- There should be no horizontal scrolling, content overlap, or loss of functionality when text is resized.
- All UI components should remain usable and readable, even at larger text sizes.


**Important Point:** Handling Large Text Without Scrollable Container
- When presenting large text or content that may exceed the visible area of the screen, it is crucial to provide a way for users to read all the content without losing access. This is especially important for users who might need larger text for better readability.

```
<!-- Using ScrollView to contain large text -->
<ScrollView
    android:layout_width="match_parent"
    android:layout_height="wrap_content">

    <TextView
        android:id="@+id/large_text"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="This is a very long piece of text that might not fit on the screen when enlarged. Users need to be able to scroll to read all of it."
        android:textSize="24sp" />
</ScrollView>
```

```kotlin
// Compose example with scrollable text
val largeText = "This is a very long piece of text that might not fit on the screen when enlarged. Users need to be able to scroll to read all of it."

Column(modifier = Modifier.verticalScroll(rememberScrollState())) {
    Text(
        text = largeText,
        fontSize = 24.sp  // Large font size
    )
}
```

##### 🚫 Failures

- An app where text overflows or overlaps when scaled up to 200%, making it unreadable, would fail this criterion.
- If an app forces horizontal scrolling to read resized text, it would also fail.
- Defining text sizes in pixels (px) rather than sp would prevent proper scaling and lead to accessibility issues.

**Bad practice example:** Fixed Height with Text Encapsulation and limiting the line count

```
<TextView
    android:id="@+id/fixed_text"
    android:layout_width="wrap_content"
    android:layout_height="50dp" <!-- Fixed height -->
    android:maxLines="2"  <!-- Limits the text to 2 lines -->
    android:ellipsize="end" <!-- Adds "..." at the end if text is too long -->
    android:text="This is a long piece of text that might be cut off when resized."
    android:textSize="16sp" />
```

```kotlin
Box(modifier = Modifier.height(50.dp)) {
    Text(
        text = "This is a long piece of text that might be cut off when resized.",
        fontSize = 16.sp,
        maxLines = 2,  // Limits the text to 2 lines
        overflow = TextOverflow.Ellipsis  // Adds "..." at the end if text is too long
    )
}
```

**Good practice:**

```
<TextView
    android:id="@+id/fixed_text"
    android:layout_width="wrap_content"
    android:minHeight="50dp"  <!-- Minimum height but flexible -->
    android:text="This is a long piece of text that might be cut off when resized."
    android:textSize="16sp" />
```

```kotlin
Box(modifier = Modifier
    .minHeight(50.dp)  // Minimum height but flexible
    .wrapContentHeight()) {
    Text(
        text = "This is a long piece of text that will resize appropriately.",
        fontSize = 16.sp
    )
}
```


---

### Images of text (WCAG 1.4.5 - Level AA)

Where components with image of text are used, they cannot satisfy the other guidelines due to image constraints. E.g., the text in the image cannot be resized which breaks the guideline 1.4.4. To avoid that, use of images of text should be avoided, or at least a text alternative should be provided.

This does not affect components which are essential for the functionality of the application, like logos or branding images.

#### ✅ Success technique(s)

Mobile apps should avoid using images of text unless the text is **part of a logo or brand name**. When images of text are used, the following must be ensured:

- The text contained in the image must have a sufficient contrast ratio with its background.
- There must be an equivalent textual alternative available to convey the same information as the image of text.
- Users should be able to resize text up to 200% without losing content or functionality.
- This guideline ensures that users with visual impairments, including those who rely on screen readers, can access and understand the content.
- The content description of the image should be meaningful, providing context that accurately conveys the image’s purpose and information.

##### 🚫 Failures

- Images of Text: It uses images of text without providing a text alternative, limiting access for users relying on screen readers.
- Inadequate Contrast: The text in an image does not meet the required contrast ratio of 4.5:1, making it difficult for users with low vision to read.
- Poor Text Alternatives: The contentDescription for an image of text is vague or does not convey the image’s meaning.
- Cutoff Content: Text in images cannot be resized and becomes cut off or unreadable when enlarged.
- Fixed Sizes: Images of text have fixed dimensions that do not adapt to user-defined text sizes, reducing accessibility.

---
### Text Spacing (WCAG 1.4.12 - Level AA)

To ensure consistent accessibility, these text spacing requirements should be incorporated directly into design specifications. Designers and developers should collaborate to confirm that the line height, paragraph spacing, letter spacing, and word spacing meet the standards across all text elements.

#### ✅ Success technique(s)

Mobile apps must ensure that the following text spacing requirements are met to enhance readability:

- Line Height: The line height (line spacing) must be at least 1.5 times the font size.
- Paragraph Spacing: The spacing between paragraphs must be at least 2 times the font size.
- Letter Spacing: The letter spacing (tracking) must be at least 0.12 times the font size.
- Word Spacing: The word spacing must be at least 0.16 times the font size.
- These spacing guidelines help ensure that users with low vision or reading difficulties can read text comfortably.

These spacing guidelines help ensure that users with low vision or reading difficulties can read text comfortably.

**Common Example:** Setting Text Spacing

- **XML Example:** Use the following attributes in your `TextView` to ensure proper text spacing.

```
<!-- Example of setting text spacing in XML -->
<TextView
    android:id="@+id/spaced_text"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="This text is spaced according to WCAG guidelines."
    android:textSize="16sp"
    android:lineSpacingExtra="4dp"  <!-- Line height (1.5 times the font size) -->
    android:letterSpacing="0.1"  <!-- Letter spacing (0.12 times font size) -->
    android:paddingBottom="8dp" />  <!-- Paragraph spacing (2 times font size) -->
```

- **Jetpack Compose Example:** Use `lineHeight`, `letterSpacing`, and `padding` to achieve the desired spacing.

```kotlin
// Compose example with text spacing
Text(
    text = "This text is spaced according to WCAG guidelines.",
    fontSize = 16.sp,
    lineHeight = 24.sp,  // Line height (1.5 times font size)
    letterSpacing = 0.1.em,  // Letter spacing (0.12 times font size)
    modifier = Modifier.padding(bottom = 8.dp)  // Paragraph spacing (2 times font size)
)
```

##### 🚫 Failures

- Inadequate Spacing: Text spacing does not meet the minimum requirements (line height, paragraph spacing, letter spacing, and word spacing).
- Overlapping Text: Text lines overlap or are too close together, which can confuse users.
- No Spacing Between Paragraphs: There is no extra space between paragraphs, making the content look cluttered.
- Fixed Text Spacing: The app uses fixed spacing that does not allow for adjustments according to user preferences.

---

### Reflow (WCAG 1.4.10 - Level AA)

The reflow is basically another name for responsible design in this context. The content should be able to reflow from one screen size to another without losing information or functionality.

#### ✅ Success criteria

Every component on the screen should be able to reflow from one screen size to another, without any content disappearing or becoming obscured. The same applies when the device orientation is changed or the content is enlarged in any way (increased font or display size in the device settings).

The above can be achieved by using:
- Components with variable size (i.e. by not restricting the maximum height/width).
- Scrollable containers when content is laid out linearly. In XML, use `ScrollView`, `NestedScrollView` or a `RecyclerView` for any content that can potentially go off screen on smaller screen sizes. In Compose, the same can be achieved by using a `LazyColumn/Row` or just a regular `Column/Row` with a `vertical/horizontalScroll()` modifier if lazy behavior is not needed.
- Layouts that allow the content to flow and wrap into multiple lines if it becomes too wide to fit the screen. In XML, this can be achieved by using the [`Flow`](https://developer.android.com/reference/androidx/constraintlayout/helper/widget/Flow) layout. In Compose, there are [`FlowRow/Column`](https://developer.android.com/develop/ui/compose/layouts/flow) for the same purpose. Do note that the flow layouts were added only in version 1.4 and are still experimental in Compose, so expect possible API changes.

For additional techniques regarding text scaling, see the [Resize text guideline](guideline_percievable_android.md#resizeable-text-wcag-144---level-aa).

This should not be done only on the screen level, but also on the component level. Every component should be able to reflow from one size to another without losing information or functionality (e.g. buttons, labels, images, etc.).

The content should also never become scrollable in both directions --- having scrolling in both directions on one screen is permitted, but not for one single piece of content (e.g. a block of text). Luckily, this is not likely to happen due to the behavior of native layouts and components, but it should still be kept in mind.

#### 🚫 Failure criteria

Content becomes unusable on a device with a smaller screen, when changing the orientation or when increasing font/display size. For example, the elements go off the screen, start overlapping or important parts of some text are cut off (e.g. ellipsized).

---

#### Sources

- [Google Support Page](https://support.google.com/accessibility/android)
- [Official Documentation](https://developer.android.com/guide/topics/ui/accessibility)

---

[← Perceivable principle](../../principles/perceivable_principle.md "Perceivable principle")
