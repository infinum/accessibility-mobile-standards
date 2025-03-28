# [Operable principle](../../principles/operable_principle.md#operable-principle)

## [Keyboard Accessible (WCAG 2.1)](../../principles/operable_principle.md#keyboard-accessible-wcag-21)

## [Keyboard (WCAG 2.1.1 - Level A)](../../principles/operable_principle.md#keyboard-wcag-211---level-a)

#### ✅ Success technique(s)

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

#### 🚫 Failures

- Not defining custom order if the views in the layout file are not defined in the same order they should be presented to the user.

## [Enough Time (WCAG 2.2)](../../principles/operable_principle.md#enough-time-wcag-22)

### [Timing Adjustable (WCAG 2.2.1 - Level A)](../../principles/operable_principle.md#timing-adjustable-wcag-221---level-a)

#### ✅ Success technique(s)

All users should be able to interact with the content displayed on the screen, even if a time limit is defined for interaction with a specific view. Therefore, users should be able to turn off the defined time limit, adjust it or extend it up to 10 times the intended time.

- In case of session inactivity, it is recommended to notify the user that they are about to be signed off with the ability to extend that time limit. The notification could be displayed in the form of an AlertDialog or something similar. TalkBack service tells you about alerts and notifications so users using accessibility services would also be aware of the defined limit.

- In the case of auto-updating content, it is recommended to allow the user to extend the defined time limit to at least ten times the length of the default setting so that they're able to process the displayed information.

- **Exceptions may apply** to to real-time events or content that is updated frequently, such as stock market data or sports scores.

Most dominant time based UI is a snack bar or a toast message. In the case of a snack bar, you can extend the duration of the message by setting the duration to `Snackbar.LENGTH_LONG` and then setting the custom duration using the `setDuration()` method. The value of the duration should be able to be adjusted by the user in the Settings of the app.
```
val SNACK_BAR_DURATION = 10_000

// Snackbar with custom duration
Snackbar.make(
    view = view, 
    resId = R.string.action_completed,
    startIconResId = Snackbar.LENGTH_LONG,
    duration = SNACK_BAR_DURATION // Set custom duration
).show()
```

```kotlin
@Composable
fun CustomSnackbarExample() {
    val snackbarHostState = remember { SnackbarHostState() }
    val coroutineScope = rememberCoroutineScope()
    val context = LocalContext.current
    val SNACKBAR_DURATION = 10_000L // 10 seconds in milliseconds

    // Trigger to show the Snackbar with a custom duration
    LaunchedEffect(Unit) {
        coroutineScope.launch {
            snackbarHostState.showSnackbar(
                message = context.getString(R.string.action_completed),
                duration = SnackbarDuration.Indefinite // Keeps it visible until dismissed manually
            )
            delay(SNACKBAR_DURATION) // Wait for 10 seconds
            snackbarHostState.currentSnackbarData?.dismiss() // Dismiss manually after 10 seconds
        }
    }

    // Display the SnackbarHost to show the Snackbar
    SnackbarHost(hostState = snackbarHostState)
}
```

#### 🚫 Failures

- Logging out the user without prior warning and the possibility to extend the session.

- Define time-limited actions in the app with no ability to extend that limit.

### [Pause, Stop, Hide (WCAG 2.2.2 - Level A)](../../principles/operable_principle.md#pause-stop-hide-wcag-222---level-a)

#### ✅ Success technique(s)

- When auto-scrolling page views, whose animation starts automatically, make sure to provide a way for the user to pause, stop, or hide it.

- If there is no parallel content next to the moving, blinking, or scrolling content, there's no need to provide a pause, stop, or hide button.

- Loading screens don't require to meet this success criterion.

#### 🚫 Failures

- Using an auto-updating or auto-scrolling view that can't be paused/stopped.

## [Seizures and Physical Reactions (WCAG 2.3)](../../principles/operable_principle.md#seizures-and-physical-reactions-wcag-23)

### [Three Flashed or Below Threshold (WCAG 2.3.1 - Level A)](../../principles/operable_principle.md#three-flashed-or-below-threshold-wcag-231---level-a)

#### ✅ Success technique(s)

- Avoiding flashing content in general, if possible.

- If using flashing content, keep the flash of an element running for a minimum of 333ms.

- If using an element that flashes more frequently is unavoidable, make sure that the flashing area covers less than 25% within 10 degrees of a visual field.

#### 🚫 Failures

- Using rapidly flashing elements to catch the user's attention.

- Having a larger area of screen flashing more than three times per second.

## [Navigable (WCAG 2.4)](../../principles/operable_principle.md#24-navigable-wcag-24)

### [Bypass Blocks (WCAG 2.4.1 - Level A)](../../principles/operable_principle.md#bypass-blocks-wcag-241---level-a)

#### ✅ Success technique(s)

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

#### 🚫 Failures

- The user of accessibility services has to navigate through all the items displayed on the screen with no possibility to fasten the navigation process.
    - No elements set as headings to separate bigger parts of text or groups in general.
    - Controls not being recognized as such. This can happen when, for example, using `TextView` instead of a `Button` or `ImageView` instead of a `Checkbox` or a `Switch` without any accessibility info modifications.

### [Page Titled (WCAG 2.4.2 - Level A)](../../principles/operable_principle.md#page-titled-wcag-242--level-a)

#### ✅ Success technique(s)

Each screen should have a clear, descriptive, and, if possible, unique title that describes the purpose of that screen that will be understandable to all users. Also, it is important to make sure that the title is the first element read when the user enters the screen. This could be achieved by following design guidelines or with the help of setting the `android:accessibilityTraversalBefore` attribute.

If the title is defined using a toolbar with custom behavior or another custom view, it is important to ensure that it will be read using accessibility services.

#### 🚫 Failures

- Screens have no titles defined, or the defined titles are not descriptive enough.

- Defined titles are not the first elements that are read when the user enters the screen and therefore users using accessibility services have no information about which screen they opened.

### [Focus Order (WCAG 2.4.3 - Level A)](../../principles/operable_principle.md#focus-order-wcag-243---level-a)

#### ✅ Success technique(s)

Order of the components that are displayed on the screen should have a logical traversal order. This is very important for people using accessibility services (such as TalkBack) to get a clearer picture of the content and possible actions on the current screen that is navigated through.

Defining the content of the screen as described in the [Meaningful sequence guideline](guideline_percievable_android.md#meaningful-sequence-wcag-132---level-a) automatically results in appropriate traversal order when navigating through the screen.

#### 🚫 Failures

- Views displayed on the screen break consistency of the navigation.

### [Link Purpose (WCAG 2.4.4 - Level A)](../../principles/operable_principle.md#link-purpose-wcag-244---level-a)

#### ✅ Success technique(s)

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

#### 🚫 Failures

- The link is defined as an unclear label or button and has no additional description provided.

- The link is part of the longer text and implemented using ClickableSpan, so TalkBack users are not aware of the link’s existence.

### [Heading and Labels (WCAG 2.4.6 - Level AA)](../../principles/operable_principle.md#heading-and-labels-wcag-246---level-aa)

#### ✅ Success technique(s)

When the user chooses to navigate between headings instead of between paragraphs or between word, make sure that sections on screen are defined as headings so that users can "skim" through them to locate the specific content they need.

For Views, you can set the `android:accessibilityHeading` attribute to `true` for a view to be treated as a heading (requires minSdk >= 28). Alternatively, you can set `ViewCompat.setAccessibilityHeading(view, true)` or use `AccessibilityDelegateCompat` for older versions.

Example: setting a TextView as a heading via `AccessibilityDelegateCompat`:
```
 ViewCompat.setAccessibilityDelegate(
        personalData,
        object : AccessibilityDelegateCompat() {
            override fun onInitializeAccessibilityNodeInfo(host: View, info: AccessibilityNodeInfoCompat) {
                super.onInitializeAccessibilityNodeInfo(host, info)
                info.isHeading = true
            }
        },
    )
```

For Compose, you can use `heading()` semantics property to define a certain node as a heading.

Example: setting a Text composable as a heading:
```
Text(
    modifier = Modifier.semantics {
        heading()
    }
)
```

In general, try to make the headings and labels as descriptive as possible. Also, in addition to that, putting the most important information at the beginning of each heading helps users navigate through the content more easily.

#### 🚫 Failures

- Not providing a heading or label for the content that follows

- Providing a missing or incorrect heading or label

### [Focus Visibility (WCAG 2.4.7 - Level AA)](../../principles/operable_principle.md#focus-visibility-wcag-247---level-aa)

#### ✅ Success technique(s)

Even though the system automatically handles this, think about selection and focus on custom elements; make sure that the focus is visible in the correct way and that the user can see which element is currently selected, especially if the component contains "inner" elements.

#### 🚫 Failure examples
- There are too many nested focusable elements and it is difficult to determine which one is in focus. This primarily might call for a reconsideration in design, where the elements could be laid out in a different way.

### [Focus Not Obscured (Minimum) (WCAG 2.4.11 - Level AA)](../../principles/operable_principle.md#focus-not-obscured-minimum-wcag-2411---level-aa)

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

## [Input modalities (WCAG 2.5)](../../principles/operable_principle.md#input-modalities-wcag-25)

### [Label in Name (WCAG 2.5.3 - Level A)](../../principles/operable_principle.md#label-in-name-wcag-253---level-a)

#### ✅ Success technique(s)

A user should easily understand the information related to the focused label. To achieve this, the following steps should be taken:

- content description should match the visible label name, or

- include the text of the visible label as a part of the content description

For views, it can be set through `android:contentDescription` attribute in XML or by using `View.setContentDescription(contentDescription)` function.

For Compose, it can be set as a semantics property.

Example: setting contentDescription in Compose:
```
Text(
     modifier = Modifier.semantics {
            contentDescription = text
        },
     text = text,
```

**Important!** For most components like labels and buttons, accessibility service will handle things automatically. In case of a custom component, `contentDescription` label should be set manually.

#### 🚫 Failures

- Not including the text of the visible label as a part of the content description

- Words of visible label and content description not matching (e.g. not the same order)

### [Motion Actuation (WCAG 2.5.4 - Level A)](../../principles/operable_principle.md#motion-actuation-wcag-254---level-a)

#### ✅ Success technique(s)

Mobile apps that support interaction through motion actuation (e.g., shaking the device, tilting, or other motion-based gestures) must also provide an alternative input method, such as touch or on-screen controls. Users should be able to disable motion actuation and still interact with the app effectively.

Example: If your app allows users to shake their phone to refresh content, you should also provide an on-screen refresh button as an alternative.

#### 🚫 Failures

An app that requires motion actuation (e.g., shaking or tilting) for core functions without offering a touch-based or alternative method of input would fail this criterion. Additionally, if motion-based controls cannot be disabled or cause unintended actions due to accidental motion, it would also be considered a failure.

Example: A mobile app that only allows form submission by shaking the device, with no button for submission, would fail this criterion.

### [Dragging Movements (WCAG 2.5.7 - Level AA)](../../principles/operable_principle.md#dragging-movements-wcag-257---level-aa)

#### ✅ Success technique(s)

Mobile apps that require dragging movements (such as swiping or dragging objects across the screen) should also offer an alternative method for performing the same function. This could include taps, buttons, or keyboard inputs that achieve the same result without relying on dragging gestures.

Example: In a photo-editing app that allows users to adjust sliders by dragging, provide the option to use + and - buttons or direct numerical input for precision.

#### 🚫 Failures

An app that relies solely on dragging movements to complete important actions (e.g., moving an item into a folder, adjusting sliders) without offering an alternative input method would fail this criterion. If dragging movements are the only means of interaction, users with motor impairments or those using assistive technology would face accessibility barriers.

Example: A to-do list app where the only way to reorder tasks is by dragging items, without an option to move tasks via buttons, would fail this criterion.

### [Target Size (Minimum) (WCAG 2.5.8 - Level AA)](../../principles/operable_principle.md#target-size-minimum-wcag-258---level-aa)

#### ✅ Success technique(s)

The application must provide enough space for the elements to be easily operable by touch.

As per official Android documentation, the recommended minimum touch target size is 48x48 dp for each interactive UI element, though larger sizes can further improve usability.

**Code example:**

- In xml layout file:
```
<ImageButton ...
    android:paddingLeft="4dp"
    android:minWidth="40dp"
    android:paddingRight="4dp"

    android:paddingTop="8dp"
    android:minHeight="32dp"
    android:paddingBottom="8dp" />
```

- In Compose:
```kotlin
IconButton(
    modifier = Modifier
        .padding(start = 4.dp, end = 4.dp, top = 8.dp, bottom = 8.dp)
        .defaultMinSize(minWidth = 40.dp, minHeight = 32.dp),
    // Add your onClick or other parameters here
) {
    // Content of the IconButton goes here
}
```

In the previous examples, the target size is calculated as the sum of minimal width/height (since those properties define the minimal size of the content area of the view) and paddings. More implementation details can be found in the [official Android documentation](https://developer.android.com/guide/topics/ui/accessibility/apps#large-controls).

More about success criterion, and also some **exceptions** regarding this rule, can be found on the [official WCAG page](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html).

_Important to note is that this guideline primarily depends on accessible design._

#### 🚫 Failures

- Interactive UI elements are too small to be easily tapped.
