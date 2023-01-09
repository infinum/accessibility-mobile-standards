# Perceivable guidelines for Android

All content displayed on the screen at some point must be presented to the user in a perceivable manner.

## Text alternatives

_Provide text alternatives for any non-text content so that it can be changed into other forms people need, such as large print, braille, speech, symbols or simpler language._

:white_check_mark: **Success criteria**

### Non-text context

Each UI element should include a description that describes it's purpose. It is important that all elements presented on the screen have the description provided, especially the ones that are important for the functionality of the screen on which they are presented. That way, screen readers such as TalkBack can announce these labels to users who rely on these services.

If an element exists on the UI only for decorative purposes it is recommended that you set its `contentDescription` to "null" or `android:importantForAccessibility` to "no" for devices running Android 4.1 and higher.

#### Label elements

In most cases you can include required description in the layout resource file as the element's `contentDescription`. It is recommended to use string resources for defining all required descriptions for easier localization.

**Code example:**

```
<!-- The en-US value for the following string is "Inspect". -->
<ImageView
    ...
    android:contentDescription="@string/inspect" />
```

_Note:_ You should not provide descriptions for TextView elements because Android accessibility services automatically announce the text itself as required description.


- Editable elements

When thinking about describing editable elements such as EditText objects, it is usually helpful to provide text that gives examples of valid input in the element itself. That way, users who navigate through the app using screen readers, could get a bit more info about the required input when they focus the editable element.

In these situations it is recommended to use `android:hint` attribute.

**Code example:**

```
<!-- The hint text for en-US locale would be
     "Username". -->
<EditText
   android:id="@+id/usernameInputField"
   android:hint="@string/username_hint_text" ... />
```


- Elements in the collection

When working with collections, it is very important that provided labels **are unique for each item**. That way, the system accessibility services can refer to exactly one specific item when announcing the label.

This will help users to get general idea when they've cycled through the complete UI of your app.

In particular, you should provide additional text or contextual information in elements within reused layouts, such as RecyclerView or ListView objects, so that each child element is uniquely identified.

The described requests could be achieved by setting content description as part of adapter implementation.

**Code example:**

An example of defining content description in adapter is given in the following snippet:

```
data class MovieRating(val title: String, val starRating: Integer)

class MyMovieRatingsAdapter(private val myData: Array<MovieRating>):
        RecyclerView.Adapter<MyMovieRatingsAdapter.MyRatingViewHolder>() {

    class MyRatingViewHolder(val ratingView: ImageView) :
            RecyclerView.ViewHolder(ratingView)

    override fun onBindViewHolder(holder: MyRatingViewHolder, position: Int) {
        val ratingData = myData[position]
        holder.ratingView.contentDescription = "Movie ${position}: " +
                "${ratingData.title}, ${ratingData.starRating} stars"
    }
}
```

:no_entry_sign: **Failure criteria**

- there are relevant UI views with no description provided

- descriptions provided for the relevant views are not unique and are repeated shortly one after another

- descriptions provided for the relevant views are too long and too complex

- descriptions provided for the relevant views are hardcoded and are not localized properly

## Time-based Media

_Provide alternatives for time-based media._

:white_check_mark: **Success criteria**

If the app you are building includes media content such as video clips or audio recordings, it is suggested to provide an alternative for users with different types of accessibility needs in order for them to understand the material. The suggested practice would be to:

- include controls that allow users to pause and stop media, change volume and toggle subtitles (captions)

- if a video presents information that is vital to completing workflow, provide the same content in an alternative format, such as transcript

:no_entry_sign: **Failure criteria**

- all media is presented to the user without the possibility to change some of the controls (slow down, pause, volume up etc.)

## Adaptable

_Create content that can be presented in different ways without losing information or structure._

### Info and Relationships

:white_check_mark: **Success criteria**

- Groups of related content

If multiple UI elements that form a natural group should be displayed on the screen, it is recommended to arrange these elements within a container which is usually a subclass of ViewGroup. Also, you should set the **container object's** `android:screenReaderFocusable` (for devices running Android 8.1. - API level 27) or `android:focusable` to true. Furthermore, you should set `android:focusable` attribute of each inner object to `false` because doing so will make accessibility services present the inner element's content descriptions one after the other, in a single announcement.

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

_Note:_ In cases like this it is recommended to define content descriptions as short as possible considering that accessibility services will read them one after the other.

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

If the app you are building provides multi-dimensional information, it is recommended to use the `android:screenReaderFocusable` attribute on the inner group containers. That kind of grouping and labeling will provide good balance between number of announcements needed to discover the screen's content and the length of each announcement.

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

It is also possible to use _headings_ to summarize groups of text that appear on the screen. To mark a view to be treated as heading you can set `android:accessibilityHeading` to true.

That way users of accessibility services can choose to navigate between headings instead of navigating between paragraphs or between words which can improve text navigation experience.

:no_entry_sign: **Failure criteria**

- it is not clear which parts of the screen are contextually connected to each other

### Sensory characteristics

:white_check_mark: **Success criteria**

It is important that the content provided in your app is easily understandable to all users. That is why it is recommended to use cues or symbols rather than colors to distinguish different views and different actions that those views provide. That way users with color vision deficiencies could also easily understand the whole UI.

:no_entry_sign: **Failure criteria**

- important difference between elements is stressed only with colors