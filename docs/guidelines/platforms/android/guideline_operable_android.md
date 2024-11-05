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

### Bypass Blocks

*This guideline covers points 2.4.1 Bypass Blocks - Level A of the WCAG standard.*

:white_check_mark: **Success criteria**

The app should be implemented so that it is possible to relatively easily skip the content that is repeated on the screen or the content that is irrelevant to the user.

This feature is also based on a good implementation of grouping the views displayed in the app as described in [Perceivable guidelines](https://github.com/infinum/accessibility-mobile-standards/blob/master/docs/guidelines/platforms/android/guideline_percievable_android.md).

For example, accessibility services users should be able to skip the whole RecyclerView list if the content is irrelevant to them without going through each item in the list.

- Headings within text

It is also possible to use _headings_ to summarize groups of text that appear on the screen. For apps with minSdk >= 28, you can set `android:accessibilityHeading` to `true` for a view to being treated as a heading.

That way, users of accessibility services, after setting the _navigation mode_ to _Headers_, can choose to navigate between headings instead of between paragraphs or between words which can improve the navigation experience.

_Note 1. Navigation mode can be chosen by swiping **up** and **down** when using **TalkBack**. Once Headers is chosen as a Navigation option, the user can navigate through **headers** by swiping right and left instead of navigating through single items.._

```
<TextView
    android:id="@+id/personalData" ...
    android:text="@string/personal_data_heading"
    android:accessibilityHeading="true"/>

<EditText
    android:id="@+id/nameEntry" ... />

<EditText
    android:id="@+id/surnameEntry" ... />

<TextView
    android:id="@+id/workplaceData" ...
    android:text="@string/personal_data_heading"
    android:accessibilityHeading="true"/>

<EditText
    android:id="@+id/addressEntry" ... />
```

For apps with minSdk < 28, headings can be defined programmatically using ViewCompat.

An example is given down below:

```
ViewCompat.setAccessibilityDelegate(personalData, object : AccessibilityDelegateCompat() {
    override fun onInitializeAccessibilityNodeInfo(host: View?, info: AccessibilityNodeInfoCompat?) {
        super.onInitializeAccessibilityNodeInfo(host, info)
        info?.isHeading = true
    }
})
```

:no_entry_sign: **Failure criteria**

- The user of accessibility services has to navigate through all the items displayed on the screen with no possibility to fasten the navigation process.

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

### Focus Order

*This guideline covers point 2.4.3 Focus Order - Level A of the WCAG standard.*

:white_check_mark: **Success criteria**

Order of the components that are displayed on the screen should have a logical traversal order. This is very important for people using accessibility services (such as TalkBack) to get a clearer picture of the content and possible actions on the current screen that is navigated through.

Defining the content of the screen in the meaningful sequence described in the [Perceivable guidelines](https://github.com/infinum/accessibility-mobile-standards/blob/master/docs/guidelines/platforms/android/guideline_percievable_android.md) automatically results in appropriate traversal order when navigating through the screen.

:no_entry_sign: **Failure criteria**

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

### Focus Visibility (WCAG 2.4.7 - Level AA)

This guideline states that the user should be able to see the focus on the element that is currently selected. With a mobile platform in mind, this guideline is automatically satisfied when TalkBack or Switch access is used --- the focus is made clearly visible with colored borders.

#### ✅ Success technique(s)

Even though the system automatically handles this, think about selection and focus on custom elements; make sure that the focus is visible in the correct way and that the user can see which element is currently selected, especially if the component contains "inner" elements.

#### 🚫 Failure examples
- There are too many nested focusable elements and it is difficult to determine which one is in focus. This primarily might call for a reconsideration in design, where the elements could be laid out in a different way.

---

### Focus Not Obscured (Minimum) (WCAG 2.4.11 - Level AA)

When the user navigates through the app, the focus should not be obscured by any other author-created elements and should be visible, at least partially.

#### ✅ Success technique(s)

When creating a view or a screen, think about the visibility of the focus and make sure that the user can see which element is currently selected.

To satisfy this guideline, check the following:

- The content is scrollable (when needed)
- The element is not obscured by other elements
- The element is (at least) partially visible when focused/used

#### 🚫 Failures

The following should be avoided:

- Element is hidden due to inability to scroll.
- Another element of the screen (e.g. sticky footer or floating element) hides the focused element.

### Other operable guidelines

This section contains guidelines that may not applicable for the mobile (Android) platform, or its criteria is a not the responsibility of the mobile team. Still, take into account that those guidelines needs to be satisfied.

- [WCAG 2.4.5 Multiple Ways - Level AA](https://www.w3.org/WAI/WCAG22/quickref/#multiple-ways)

---

#### Sources

- [Google Support Page](https://support.google.com/accessibility/android)
- [Official Documentation](https://developer.android.com/guide/topics/ui/accessibility)

---

[← Operable principle](../../principles/operable_principle.md "Operable principle")










