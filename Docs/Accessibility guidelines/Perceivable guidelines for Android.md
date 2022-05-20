# Perceivable guidelines for Android 

All content that is displayed on the screen at some point must be presented to the user in a way that he can perceive.

## Text alternatives 

// TODO add simple description of this section

### Non-text context

Each UI element should include a description that describes it's purpose. It is important that all element presented on the screen have the description provided, especially the ones that are important for the functionality of the screen on which they are presented. That way, screen readers such as TalkBack can announce these labels to users who rely on these services.

If an element exists on the UI only for decorative purposes it is recommended that you set its `contentDescription` to "null" or `android:importantForAccessibility` to "no" for devices running Android 4.1 and higher. 

#### Label elements

In most cases you can include required description in the layout resource file as the element's `contentDescription`. It is recommended to use string resources for defining all required descriptions for easier localization.

The example is shown on the following snippet:

```
<!-- The en-US value for the following string is "Inspect". -->
<ImageView
    ...
    android:contentDescription="@string/inspect" />
```

_Note:_ You should not provide descriptions for TextView elements because Android accessibility services automatically announce the text itself as required description.


- Editable elements

When thinking about describing editable elements such as EditText objects, it is usually helpful to provide text that give examples of valid input in the element itself. That way, users who navigate through the app using screen readers, could get a bit more info about the required input when they focus the editable element. 

In these situations it is recommended to use `android:hint` attribute: 

```
<!-- The hint text for en-US locale would be
     "Apartment, suite, or building". -->
<EditText
   android:id="@+id/addressLine2"
   android:hint="@string/aptSuiteBuilding" ... />
```


- Elements in the collection

When working with collections, it is very important that provided labels **are unique for each item**. That way, the system accessibility services can refer to exactly one specific item when announcing the label. 

This will help users to get general idea when they've cycled through the complete UI of your app.

In particular, you should provide additional text or contextual information in elements within reused layouts, such as RecyclerView or ListView objects, so that each child element is uniquely identified.

The described requests could be achieved by setting content description as part of adapter implementation.

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

:white_check_mark: **Success criteria**

:no_entry_sign: **Failure criteria**

## Time-based Media

**Make media content more accessible**

If the app you are building includes media content such as video clip or audio recording, it is suggested to provide alternative for users with different types of accessibility needs in order for them to understand the material. The suggested practice would be to:

- include controls that allow users ro pause and stop media, change volume and toggle subtitles (captions)

- if a video presents information that is vital to completing workflow, provide the same content in an alternative format, such as transcript

// TO-DO ADD CODE examples

:white_check_mark: **Success criteria**

:no_entry_sign: **Failure criteria**

## Adaptable 

### Info and Relationships

- Groups of related content

If multiple UI elements that form a natural group should be displayed on the screen, it is recommended to arrange these elements within a container which is usually subclass of ViewGroup. Also, you should set the **container object's** `android:screenReaderFocusable` (for devices running Android 8.1. - API level 27) or `android:focusable` to true. Furthermore, you should set `android:focusable` attribute of each inner object to `false` because doing so, accessibility services can present the inner element's content descriptions one after the other, in a single announcement.

Grouping elements based on the context helps users that benefit from using accessibility services to discover the information that is on the screen more efficiently.

The example of grouping elements is given in the following snippet:

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

The example is given in the snippet down below:

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

The example is given in the snippet down below:

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

It is also possible to use _headings_ to summarize groups of text that appear on the screen. To mark some view to be treated as heading you can set `android:accessibilityHeading` to true.

That way users of accessibility services can choose to navigate between headings instead of between paragraphs or between words which can improve text navigation experience.

:white_check_mark: **Success criteria**

:no_entry_sign: **Failure criteria**

### Meaningful sequence

- Pairs od elements where one describes the other

It is common case that given EditText has corresponding View that describes the content that the user should enter within the EditText element. This relationship between elements could be achieved by setting `android:labelFor` attribute on that specific View.

That way, services such as TalkBack will read defined relationship to the user to give him a bit more context when EditText is in focus.

An example of labeling such element pair is given in the following snippet:

```
<!-- Label text for en-US locale would be "Username:" -->
<TextView
   android:id="@+id/usernameLabel" ...
   android:text="@string/username"
   android:labelFor="@+id/usernameEntry" />

<EditText
   android:id="@+id/usernameEntry" ... />
```

In the given example, services such as TalkBack will read - "EditBox for username" when user sets focus to EditText.

:white_check_mark: **Success criteria**

:no_entry_sign: **Failure criteria**

### Sensory characteristics

It is important that the content provided in your app is easily understandable to all users. That is why it is recommended to use cues or symbols rather than colors to distinguish different view and different actions that those views provide. That way users with color vision deficiencies could also easily understand the whole UI. 

The example is given in the screenshots down below. On the left screenshot there is example of the bills UI in MojA1 app. The only difference between paid and unpaid bills in the list is the color. Unpaid bills are presented in red color instead of the regular black. For users with color vision deficiencies this could be a problem. A better solution is provided on the right screenshot. There is example of the bills UI in MojTomato app. As you can see, unpaid bills are presented there with different symbol instead of color and that way users could more easily distinguish there is difference between items presented in the list. 

| ![a1-bills.jpg](https://imgur.com/RcsRuYf.png) | ![tomato-bills.jpg](https://imgur.com/pWejQkl.png) |
|:--:|:--:|
| <b>A1 App - Bills</b> | <b>Tomato App - Bills</b>|

:white_check_mark: **Success criteria**

:no_entry_sign: **Failure criteria**

### Distinguishable

// TO-DO add distinguishable section

:white_check_mark: **Success criteria**

:no_entry_sign: **Failure criteria**






