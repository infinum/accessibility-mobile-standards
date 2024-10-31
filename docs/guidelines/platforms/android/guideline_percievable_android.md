 [🔼 Accessibility principles and examples](../../principles/accessibility_principles_and_examples.md  "Accessibility principles and examples") | [⬅️ Perceivable principle](../../principles/perceivable_principle.md "Perceivable principle")
# Perceivable guidelines for Android

All content displayed on the screen at some point must be presented to the user in a perceivable manner.

## Text alternatives

Provide text alternatives for any non-text content so that it can be changed into other forms people need, such as large print, braille, speech, symbols or simpler language.

*This guideline covers point 1.1.1 Non-text Content - Level A of the WCAG standard.*

#### ✅ Success technique(s)

### Non-text context

Each UI element should include a description that describes its purpose. All elements presented on the screen must have the description provided, especially the ones that are important for the screen’s functionality. That way, screen readers such as TalkBack can announce these labels to users who rely on these services.

If an element exists on the UI only for decorative purposes it is recommended that you set its `contentDescription` to "null" or `android:importantForAccessibility` to "no" for devices running Android 4.1 and higher.

##### 🚫 Failures

- Not providing descriptions of elements presented on the screen that do not exist only for decorative purposes

---

## Time-based Media

Provide alternatives for time-based media.

*This guideline covers point 1.2 Time-Based Media - Level A of the WCAG standard.*

#### ✅ Success technique(s)

Suppose the app you are building includes media content such as video clips or audio recordings. In that case, it is suggested to provide an alternative for users with different types of accessibility needs for them to understand the material. The suggested practice would be to:

- Include controls that allow users to pause and stop media, change volume and toggle subtitles (captions)

- If a video presents information that is vital to completing workflow, provide the same content in an alternative format, such as a transcript

##### 🚫 Failures

- All media is presented to the user without the possibility of changing some of the controls (slow down, pause, volume up, etc.).

---

## Adaptable

Create content that can be presented in different ways without losing information or structure.

### Info and Relationships

Information, structure, and relationships conveyed through presentation are available in text.

*This guideline covers point 1.3.1 Info and Relationships - Level A of the WCAG standard.*

#### ✅ Success technique(s)

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

##### 🚫 Failures

- It is not clear which parts of the screen are contextually connected.

---

### Meaningful sequence

*This guideline covers point 1.3.2 Meaningful sequence - Level A of the WCAG standard.*

#### ✅ Success technique(s)

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

```kotlin
ViewCompat.setAccessibilityDelegate(button1, object : AccessibilityDelegateCompat() {
    override fun onInitializeAccessibilityNodeInfo(host: View?, info: AccessibilityNodeInfoCompat?) {
        super.onInitializeAccessibilityNodeInfo(host, info)
        info?.setTraversalAfter(button2)
    }
})
```

##### 🚫 Failures

- Views displayed on the screen break consistency of the navigation.

---

### Sensory characteristics

*This guideline covers point 1.3.3 Sensory characteristics - Level A of the WCAG standard.*

#### ✅ Success technique(s)

The content provided in your app must be easily understandable to all users. That is why it is recommended to use cues or symbols rather than colors to distinguish different views and different actions that those views provide. That way, users with color vision deficiencies could also easily understand the whole UI.

##### 🚫 Failures

- An important difference between elements is stressed only with colors.

---


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

#### Sources

- [Google Support Page](https://support.google.com/accessibility/android)
- [Official Documentation](https://developer.android.com/guide/topics/ui/accessibility)

---

[← Perceivable principle](../../principles/perceivable_principle.md "Perceivable principle")
