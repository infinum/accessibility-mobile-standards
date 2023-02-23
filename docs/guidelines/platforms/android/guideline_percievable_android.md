# Perceivable guidelines for Android

All content displayed on the screen at some point must be presented to the user in a perceivable manner.

## Text alternatives

_Provide text alternatives for any non-text content so that it can be changed into other forms people need, such as large print, braille, speech, symbols or simpler language._

:white_check_mark: **Success criteria**

### Non-text context

Each UI element should include a description that describes its purpose. All elements presented on the screen must have the description provided, especially the ones that are important for the screen’s functionality. That way, screen readers such as TalkBack can announce these labels to users who rely on these services.

If an element exists on the UI only for decorative purposes it is recommended that you set its `contentDescription` to "null" or `android:importantForAccessibility` to "no" for devices running Android 4.1 and higher.

:no_entry_sign: **Failure criteria**

- Not providing descriptions of elements presented on the screen that do not exist only for decorative purposes

#### Additional notes

This guideline covers point 1.1.1 Non-text Content – Level A of the WCAG standard.

---

## Time-based Media

_Provide alternatives for time-based media._

:white_check_mark: **Success criteria**

Suppose the app you are building includes media content such as video clips or audio recordings. In that case, it is suggested to provide an alternative for users with different types of accessibility needs for them to understand the material. The suggested practice would be to:

- Include controls that allow users to pause and stop media, change volume and toggle subtitles (captions)

- If a video presents information that is vital to completing workflow, provide the same content in an alternative format, such as a transcript

:no_entry_sign: **Failure criteria**

- All media is presented to the user without the possibility of changing some of the controls (slow down, pause, volume up, etc.).

#### Additional notes

This guideline covers point 1.2 Time-Based Media – Level A of the WCAG standard.

---

## Adaptable

_Create content that can be presented in different ways without losing information or structure._

### Info and Relationships

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

#### Additional notes

This guideline covers point 1.3.1 Info and Relationships - Level A of the WCAG standard.

---

### Meaningful sequence

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

#### Additional notes

This guideline covers point 1.3.2 Meaningful sequence – Level A of the WCAG standard.

---

### Sensory characteristics

:white_check_mark: **Success criteria**

The content provided in your app must be easily understandable to all users. That is why it is recommended to use cues or symbols rather than colors to distinguish different views and different actions that those views provide. That way, users with color vision deficiencies could also easily understand the whole UI.

:no_entry_sign: **Failure criteria**

- An important difference between elements is stressed only with colors.

#### Additional notes

This guideline covers point 1.3.3 Sensory characteristics – Level A of the WCAG standard.

---

#### Sources

- [Google Support Page](https://support.google.com/accessibility/android)
- [Official Documentation](https://developer.android.com/guide/topics/ui/accessibility)

---

[← Perceivable principle](../../principles/perceivable_principle.md "Perceivable principle")
