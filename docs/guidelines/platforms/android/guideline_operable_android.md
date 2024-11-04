 [🔼 Accessibility principles and examples](../../principles/accessibility_principles_and_examples.md "Accessibility principles and examples") | [⬅️ Operable principle](../../principles/operable_principle.md "Operable principle")
# Operable guidelines for Android

User interface components and navigation must be operable.

## Keyboard accessible

Make all functionality available from a keyboard.

*This guideline covers point 2.1.1 Keyboard - Level A of the WCAG standard.*

:white_check_mark: **Success criteria**

Besides the on-screen keyboard, Android also supports physical keyboards that offer a convenient way to input text and navigate and interact with the app. This feature greatly benefits users with motor difficulties who use the Switch Access service to interact with the app.

- Handle tab navigation

When the user navigates through the app using the `Tab` key on the keyboard, the system focuses on the order of elements appearing on the screen. This is why, if the order of the view elements on the screen is not entirely the same as the order defined in the file, you might need to manually specify the focus order. You can achieve this by simply defining `android:nextFocusForward` attribute.

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

When the user is navigating through the app **using the arrow keys on the keyboard**, the system provides a best guess as to which view should be given focus in the given direction, based on the layout of the views on the screen. This behavior corresponds to navigating using a D-pad or trackball. But, there are situations when the system could guess incorrectly; in that case, it is important to manually specify which view should receive focus. This could be achieved using the following attributes:  `android:nextFocusUp`, `android:nextFocusDown`, `android:nextFocusLeft` and `android:nextFocusRight`.

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

- Not defining custom order if the views in the layout file are not defined in the same order they should be presented to the user.

---

## Enough time

Provide users enough time to read and use the content.

*This guideline covers point 2.2.1 Timing Adjustable - Level A of the WCAG standard.*

:white_check_mark: **Success criteria**

All users should be able to interact with the content displayed on the screen, even if a time limit is defined for interaction with a specific view. Therefore, users should be able to turn off the defined time limit, adjust it or extend it.

- In case of session inactivity, it is recommended to notify the user that they are about to be signed off with the ability to extend that time limit. The notification could be displayed in the form of an AlertDialog or something similar. TalkBack service tells you about alerts and notifications so users using accessibility services would also be aware of the defined limit.

- In the case of auto-updating content, it is recommended to allow the user to extend the defined time limit to at least ten times the length of the default setting so that they're able to process the displayed information.

:no_entry_sign: **Failure criteria**

- Logging out the user without prior warning and the possibility to extend the session.

- Define time-limited actions in the app with no ability to extend that limit.

---

### Pause, Stop, Hide

Moving, blinking, or scrolling, or auto-updating content in the app.

*This guideline covers point 2.2.2 Pause, Stop Hide - Level A of the WCAG standard.*

#### ✅ Success technique(s)

- When auto-scrolling page views, whose animation starts automatically, make sure to provide a way for the user to pause, stop, or hide it.

- If there is no parallel content next to the moving, blinking, or scrolling content, there's no need to provide a pause, stop, or hide button.

- Loading screens don't require to meet this success criterion.

#### 🚫 Failures

- Using an auto-updating or auto-scrolling view that can't be paused/stopped.

---

## Seizures and Physical Reactions

Do not design content in a way that is known to cause seizures or physical reactions.

### Three Flashed or Below Threshold

Apps should not contain elements that flash more than three times in one second.

*This guideline covers point 2.3.1 - Level A of the WCAG standard.*

#### ✅ Success technique(s)

- Avoiding flashing content in general, if possible.

- If using flashing content, keep the flash of an element running for a minimum of 333ms.

- If using of an element that flashes more frequently is unavoidable, make sure that the flashing area covers less than 25% within 10 degrees of a visual field.

#### 🚫 Failures

- Using rapidly flashing elements to catch the user's attention.

- Having a larger area of screen flashing more than three times per second.

---

## Navigable

Provide ways to help users navigate, find content, and determine where they are.

### Bypass Blocks (WCAG 2.4.1 - Level A)

The app should be implemented so that it is possible to relatively easily skip the content that is repeated on the screen or the content that is irrelevant to the user.

In addition to the basic left/right swipe navigation through elements, TalkBack offers navigation by element types (headings, controls and links) and fine-grained navigation through text (by paragraphs, lines, words and characters) which is controlled with up/down swipes, as explained in the [Reading controls chapter](https://support.google.com/accessibility/android/answer/6007066?hl=en) of Google's TalkBack support page. These alternate modes of navigation are the main tool used for bypassing blocks, so it is important to make sure they all work as intended. Fortunately, most of them work well with native components, but some require additional effort.

✅ **Success criteria**

The first step in satisfying the criteria is having a design that breaks content into smaller pieces and provides us with "anchor points" that can be used to skip chunks of content (for example, splitting long text into paragraphs, or grouping form fields into sections with headings). After that, these anchor points need to be properly categorized (as headings, controls, etc.) in order to become visible to assistive services and used for navigation.

#### Headings within text

⚠️ There is no way for an element to be recognized as a heading automatically, so it must always be marked as a heading manually.

Once that is done, it will get picked up by TalkBack and the user will be able to skip parts of content by navigating through headings. This should be automatically satisfied by following the [Heading and Labels guideline](guideline_operable_android.md#heading-and-labels-wcag-246---level-aa).

#### Controls
TalkBack can recognize that something is a control based on the element's role (button, toggle, edit text etc.). Native controls will always be recognized automatically. For custom components, make sure to set a proper role as described in the [Name, Role, Value chapter](guideline_robust_android.md#name-role-value-wcag-412---level-a).

#### Links
This criteria should be satisfied by following the recommendations from [Link purpose guideline](guideline_operable_android.md#link-purpose).

#### Skippable groups

In addition to the above, a section of a screen containing numerous items should have related items grouped, so that they are easily skippable and do not require multiple swipes to go over. This feature is based on a good implementation of grouping as described in [Info and relationships - Element relationships guideline](guideline_percievable_android.md#element-relationships).

🚫 **Failure criteria**

- The user of accessibility services has to navigate through all the items displayed on the screen with no possibility to fasten the navigation process.
    - No elements set as headings to separate bigger parts of text or groups in general.
    - Controls not being recognized as such. This can happen when, for example, using `TextView` instead of a `Button` or `ImageView` instead of a `Checkbox` or a `Switch` without any accessibility info modifications.

---

### Page Titles

*This guideline covers point 2.4.2 Page Titled - Level A of the WCAG standard.*

:white_check_mark: **Success criteria**

Each screen should have a clear, descriptive, and, if possible, unique title that describes the purpose of that screen that will be understandable to all users. Also, it is important to make sure that the title is the first element read when the user enters the screen. This could be achieved by following design guidelines or with the help of setting the `android:accessibilityTraversalBefore` attribute.

If the title is defined using a toolbar with custom behavior or another custom view, it is important to ensure that it will be read using accessibility services.

:no_entry_sign: **Failure criteria**

- Screens have no titles defined, or the defined titles are not descriptive enough.

- Defined titles are not the first elements that are read when the user enters the screen and therefore users using accessibility services have no information about which screen they opened.

---

### Focus Order (WCAG 2.4.3 - Level A)

Ensure that information is read in an order consistent with the meaning and content.

✅ **Success criteria**

Order of the components that are displayed on the screen should have a logical traversal order. This is very important for people using accessibility services (such as TalkBack) to get a clearer picture of the content and possible actions on the current screen that is navigated through.

Defining the content of the screen as described in the [Meaningful sequence guideline](guideline_percievable_android.md#meaningful-sequence-wcag-132---level-a) automatically results in appropriate traversal order when navigating through the screen.

🚫 **Failure criteria**

- Views displayed on the screen break consistency of the navigation.

---

### Link Purpose

*This guideline covers point 2.4.4 Link Purpose (In Context) - Level A of the WCAG standard.*

:white_check_mark: **Success criteria**

All the links displayed in the application's components and screens should explain its unique purpose. This is important because, based on the provided descriptions, users would get a better idea of whether they want to follow the provided link.

If the context of the text is not self-explanatory, users of accessibility services could try to find more information about the provided link in its surroundings.

Some of the recommended techniques that could improve clarifying the context of the provided link are listed below:

- Pair the link with descriptive text elements that provide more context for the link itself.

An example is given in **Screenshot 1.**

- Set an accessibility description (content description) for the link item that will provide more information about it.

The example shown in **Screenshot 2.** - If the link item is implemented as regular TextView or Button, additional contentDescription should be provided to give more information and stress that the user is leaving the app.

- Define self-explanatory link text labels.

The example shown in **Screenshot 3.** - If the link text is well defined and implemented using URLSpan, no additional description is needed. Accessibility services will recognize the link and warn the user that they will leave the app.

- If the link is defined as part of the longer text use **URLSpan** for link implementation.

The example given in the **Screenshot 4.** - **Avoid using ClickableSpan** and instead **use URLSpan** to add a link to the specific text part. That way, an accessibility service such as TalkBack will recognize a link set somewhere in the text, and the user will know that they are able to perform the action if they are interested in the following link.

| <img src="https://imgur.com/5HPJfes.png" width="50%"> | <img src="https://imgur.com/MlWcuYI.png" width="50%"> |
|:--:|:--:|
| **Screenshot 1.** Link paired with a descriptive text element | **Screenshot 2.** Link implemented as regular TextView or Button |
| <img src="https://imgur.com/xHv8oCi.png" width="50%"> | <img src="https://imgur.com/dy92J6y.png" width="50%"> |
| **Screenshot 3.** Link text implemented using URLSpan | **Screenshot 4.** Text containing the link is part of a longer text |

:no_entry_sign: **Failure criteria**

- The link is defined as an unclear label or button and has no additional description provided.

- The link is part of the longer text and implemented using ClickableSpan, so TalkBack users are not aware of the link’s existence.

---

#### Sources

- [Google Support Page](https://support.google.com/accessibility/android)
- [Official Documentation](https://developer.android.com/guide/topics/ui/accessibility)

---

[← Operable principle](../../principles/operable_principle.md "Operable principle")










