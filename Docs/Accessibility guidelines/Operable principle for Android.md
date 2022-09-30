# Operable guidelines for Android 

_User interface components and navigation must be operable._

In this section we will describe guidelines and define examples of implementation that will help in making your application more operable. 

## Keyboard accessible

:white_check_mark: **Success criteria**

Except on-screen keyboard, Android also supports physical keyboards that offer convenient way to input text but also to navigate and interact with the app. This is also of huge benefit for the users with motor difficulties that use Switch Access service to interact with the app. 

- Handle tab navigation

When the is navigating through he app **using Tab key** on the keyboard, the system passes focus based on the the order elements are appeared on the screen. This means that in case the order of the elements on the screen is not entirely the same as the order defined in the file, you might need to manually specify the focus order. 

**Code example:** 

```
<ConstraintLayout ...>
    <Button
        android:id="@+id/button1"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        android:nextFocusForward="@+id/editText1"
    ... />

    <Button
        android:id="@+id/button2"
        app:layout_constraintTop_toBottomOf="@id/button1"
        android:nextFocusForward="@+id/button1"
    ... />

    <EditText
        android:id="@id/editText1"
        app:layout_constraintBottom_toBottomOf="@+id/button2"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toStartOf="@id/button2"
        android:nextFocusForward="@+id/button2"
    ... />
    ...
</ConstraintLayout>
```

- Handle directional navigation

When the user is navigating through the app **using arrow keys on the keyboard**, the system provides the best-guess as to which view should be given focus in the given direction based on the layout of the views on the screen. This behavior corresponds to navigating using D-pad or trackball. But, there are situation when the system could make wrong guess and in that case it is important to manually specify which view should receive focus. This could be achieved using following attributes: `android:nextFocusUp`, `android:nextFocusDown`, `android:nextFocusLeft` and `android:nextFocusRight`.

**Code example:** 

```
<Button
    android:id="@+id/button1"
    android:nextFocusRight="@+id/button2"
    android:nextFocusDown="@+id/editText1"
    ... />
<Button
    android:id="@id/button2"
    android:nextFocusLeft="@id/button1"
    android:nextFocusDown="@id/editText1"
    ... />
<EditText
    android:id="@id/editText1"
    android:nextFocusUp="@id/button1"
    ...  />
```

:no_entry_sign: **Failure criteria**

- not defining custom order if the views it the layout file are not defined in the same order they should be presented to the user

## Enough time

_Provide users enough time to read and use content._

:white_check_mark: **Success criteria**

All the users should have ability to interact with the content displayed on the screen even if there is time limit defined for interaction with that specific view. Therefore, users should have the ability to turn off defined time-limit, adjust it or extend it.

- In case of session inactivity it is recommended to notify the user that will about to be signed off with ability to extend that time-limit. The notification could be displayed in form of Alert or something similar. TalkBack service tells you about alerts and notifications so users using accessibility services would also be aware of the defined limit.

- In case of auto-updating content it is recommended to allow user to extend the defined time-limit to at least ten times the length of the default setting for everyone to be able to process the displayed information.

:no_entry_sign: **Failure criteria**

- logging out user without prior warning and possibility to extend session

- define time-limited actions in the app with no ability to extend that limit

## Navigable 

_Provide ways to help users navigate, find content, and determine where they are._

### Bypass Blocks

:white_check_mark: **Success criteria**

The app should be implemented in a way that it is possible to relatively easy skip the content that is repeated on the screen or the content that is irrelevant to the user.

This is feature is based on a good implementation of grouping the views that are displayed in the app as described in [link to perceivable guidelines].

For example, accessibility services users should be able to skip the whole RecyclerView list if the content is irrelevant to them without having to go through each item in the list. 

- Headings within text

It is also possible to use _headings_ to summarize groups of text that appear on the screen. To mark some view to be treated as heading you can set `android:accessibilityHeading` to true.

That way users of accessibility services can choose to navigate between headings instead of between paragraphs or between words which can improve text navigation experience.

// TODO ADD SNIPPETS OF IMPLEMENTATION and example

:no_entry_sign: **Failure criteria**

- user using accessibility services has to navigate through all the items displayed on the screen with no possibility to fasten the navigation proccess

### Page Titles

Each screen should have clear, descriptive, if possible unique title that describes purpose of that screen that will be understandable to all users. Also, it is important to make sure that title is the first thing that will be read when user enters the screen. This could be achieved following design guidelines or with help of setting `android:accessibilityTraversalBefore` attribute.

If title is defined using toolbar with custom behavior or some other custom view it is important to insure that title will be read using accessibility services.

:white_check_mark: **Success criteria**

- each screen has descriptive title defined that is read when user enters the screen

:no_entry_sign: **Failure criteria**

- screens have no titles defined or the defined titles are not descriptive enough

- defined titles are not the first thing that is read when user enters the screen and therefore users using accessibility services have no information which screen they opened

### Traversal Order 

Order of the components that are displayed on the screen should have logical traversal order. That is very important for people using accessibility services such as TalkBack to get clearer picture of the content and possible actions on the current screen they are navigating through.

The best solution would be to redesign the screen to create logical traversal order. But if that is not an option, setting `android:accessibilityTraversalBefore` or `android:accessibilityTraversalAfter` attributes could help create new order of the displayed views that will make a bit more sense to TalkBack users.

The example of using `android:accessibilityTraversalBefore` or `android:accessibilityTraversalAfter` attributes is given down below:

// TO-DO add screenshot of real app and set the attributes 

_Note 1. Always make sure to define `android:accessibilityTraversalBefore` or `android:accessibilityTraversalAfter` attributes in a way that does not create any loops or traps that will prevent users to interact with all relevant views displayed on the screen._

**Code example:**

// TODO

:no_entry_sign: **Failure criteria**

### Link Purpose 

:white_check_mark: **Success criteria**

All the links that are displayed in the application's components and screens should explain its unique purpose. This is important because based on the provided descriptions users would get a better idea if they want to follow provided link or not. 

If the context of the text is not self-explanatory and clear, users of accessibility services could try to find more information of the provided link in its surroundings. 

Some of the recommended techniques that could improve clarifying the context of the provided link are listed down below: 

- Pair the link with descriptive text element that provide more context of the link itself. 
  
Example is given on the **Screenshot 1.** // TO-DO create this example

- Set accessibility description (content description) for the link item that will provide more information about it. 

Example shown on the **Screenshot 2.** - If the link is implemented using If link item is implemented as regular TextView or Button, additional contentDescription should be provided give more information and stress that user is leaving the app.

- Define self-explanatory link text labels. 

Example shown on the **Screenshot 3.** - If the link text is well defined and implemented using URLSpan, no additional description is needed. Accessibility services will recognize the link and warn user that he will leave the app. 

- If link is defined as part of the longer text use **URLSpan** for link implementation. 

Example given on the **Screenshot 4.** - **Avoid using ClickableSpan** and instead **use URLSpan** for adding link to specific part of text. That way accessibility service such as TalkBack will recognized there is link set somewhere in the text and user will know that he is able to perform action if he is interested in following link.

| <img src="https://imgur.com/b833Hol.png" width="50%"> | <img src="https://imgur.com/6mI8z8W.png" width="50%"> |
|:--:|:--:|
| **Screenshot 1.** Text containing link is part of a longer text | **Screenshot 2.** Link implemented as regular TextView or Button |
| <img src="https://imgur.com/wj8hWQy.png" width="50%"> | <img src="https://imgur.com/b833Hol.png" width="50%"> |
| **Screenshot 3.** Link text implemented using URLSpan | **Screenshot 4.** Link as part of longer text should be implemented using URLSpan |

:no_entry_sign: **Failure criteria**

- link is defined as unclear label or button and has no additional description provided

- link is part of the longer text and implemented using ClickableSpan so TalkBack users are not aware of link existence











