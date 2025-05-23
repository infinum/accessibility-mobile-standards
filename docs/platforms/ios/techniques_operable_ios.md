# [Operable principle](../../principles/operable_principle.md#operable-principle)

## [Enough Time (WCAG 2.2)](../../principles/operable_principle.md#enough-time-wcag-22)

### [Timing Adjustable (WCAG 2.2.1 - Level A)](../../principles/operable_principle.md#timing-adjustable-wcag-221---level-a)

#### ✅ Success technique(s)

- Session inactivity timeout: Display a warning message that the user is about to be signed out with an extension option. Or allow the user to increase the default kick-out timeout time of inactivity ten times (e.g. from 30s to 5 min) so they have enough time to process content.

- Auto-updating content (like news page): allow the user to extend the time limit to 10 times longer.

- Real-time exception: time limit cannot be disabled/extended for a real-time event (e.g. an auction, booking movie tickets, watching live stream).

- In case you're using a custom modal presentation or a custom modal view, make sure that UIAccessibility is notified about the screen change.

#### 🚫 Failures

- Logging a user out of their session with no prior warning.
- Not providing enough time or time extensions to react to an incoming action in the app.

### [Pause, Stop, Hide (WCAG 2.2.2 - Level A)](../../principles/operable_principle.md#pause-stop-hide-wcag-222---level-a)

#### ✅ Success technique(s)

- When using auto-scrolling page views (carousels) which animation starts automatically, make sure to provide a way for the user to pause, stop, or hide it.
- If there is no parallel content next to the moving, blinking, or scrolling content, there's no need to provide a pause, stop, or hide button.
- Loading screens doesn't require meeting this success criterion.

#### 🚫 Failures

- Using an auto-updating or auto-scrolling view that can't be paused/stopped.

## [Seizures and Physical Reactions (WCAG 2.3)](../../principles/operable_principle.md#seizures-and-physical-reactions-wcag-23)

### [Three Flashed or Below Threshold (WCAG 2.3.1 - Level A)](../../principles/operable_principle.md#three-flashed-or-below-threshold-wcag-231---level-a)

#### ✅ Success technique(s)

- Avoid flashing content altogether if possible.
- If using flashing content – make sure that any flashing elements have a period of at least 333 ms.
- If you do have an element that flashes more frequently – ensure that the flashing area is less than 25% of 10 degrees of the visual field.

#### 🚫 Failures

- Using rapidly flashing elements to catch the user's attention.
- Having a larger area of screen flashing more than three times per second.

## [2.4 Navigable (WCAG 2.4)](../../principles/operable_principle.md#navigable-wcag-24)

### [Bypass Blocks (WCAG 2.4.1 - Level A)](../../principles/operable_principle.md#bypass-blocks-wcag-241---level-a)

#### ✅ Success technique(s)

- VoiceOver: A section of a screen containing numerous items should have those items grouped and an accessibility label with a quick summary of the contents. This way, if they are relevant to the user, the user may swipe up or down to iterate through each item, and in case they are not, the user may use a left or right swipe to skip them.

- An element containing many labels or buttons should also have a summary accessibility label so it takes fewer swipes to skip over it.

    **Example**: VoiceOver In Instagram main feed - Instagram stories are contained inside an "adjustable" accessibility group named "Stories Tray".

    1. User arrives to the "Stories Tray" by tapping or using the right swipes.
    2. VoiceOver announces the group’s name and quick summary with an "adjustable" hint at the end.
    3. User can then iterate through items (adjust) by swiping up and down.
    4. Once done reviewing stories, the user can read right-swipe to skip to the next element on the screen.

    If you want to try this out for yourself, we've prepared an [example project](https://github.com/infinum/ios-accessibility-demo) where we've recreated this exact behavior.

- Using rotors: In case when user needs to navigate through different elements of the screen, a custom rotor can be a nice way of changing the type of block the user wants to navigate through. Custom rotors are a great way to deal with filtering and changing the state of the screen (if needed).

    **Example**: VoiceOver rotor for navigating through different elements of the screen:

```swift
    func setupRotors() {
        let rotor = UIAccessibilityCustomRotor(name: "My custom rotor") { predicate in
            // Return the next element (e.g. elements that needs to be focused) based on the predicate
            return UIAccessibilityCustomRotorItemResult(targetElement: nextElement, targetRange: nil)
        }
        self.accessibilityCustomRotors = [rotor]
    }
```

Please check more information about custom rotors in [this](https://developer.apple.com/videos/play/wwdc2020/10116/) WWDC video.

#### 🚫 Failures

Not providing a way for the user to quickly skip over sections with numerous items.

### [Page Titled (WCAG 2.4.2 - Level A)](../../principles/operable_principle.md#page-titled-wcag-242--level-a)

#### ✅ Success technique(s)

- VoiceOver: When the user requests the entire screen to be read from the top, make sure that the title is one of the first things the user will hear so they know whether they are on the right page or step.

    **Example**: Setting view controller's title in `viewDidLoad`:

```swift
    func viewDidLoad() {
        super.viewDidLoad()
        title = "Home"
        navigationItem.title = "Home" // Another way
    }
```

- When using custom title view, make sure to configure its accessibility label.

    **Example**: using custom titleView:

```swift
    func setupTitleView() {
        navigationItem.titleView = UIImageView(image: .init(named: "header.png"))
        navigationItem.titleView?.accessibilityLabel = "Home"
    }
```

- If using custom navigation bar, make sure that the title can be read correctly by VoiceOver.

#### 🚫 Failures

- Leaving the title empty
- Using a custom title view or custom navigation bar without ensuring it's readable by VoiceOver.
- In document-editor screens, avoid using:
  - default titles like "Untitled Document" or "No Title"
  - file names like "report.pdf" or "DSC_0123.jpeg"
  - placeholder text like "Enter title..." or "Search..."

### [Focus Order (WCAG 2.4.3 - Level A)](../../principles/operable_principle.md#focus-order-wcag-243---level-a)

#### ✅ Success technique(s)

- VoiceOver: When designing a new screen, make sure to test it with VoiceOver and see whether the elements are read in the right, logical order. The easiest way to achieve a correct focus order is to layout elements inside a `UIStackView`. VoiceOver will read elements in the same order as in the interface builder document outline.
Keep in mind: when placed outside a stack view, elements positioned closer to the top are read first. If elements are near the same vertical position, leading-side elements are read first.

- To change focus order, create an array of subviews and assign it to their parent container's `accessibilityElements`.

   **Example:** Setting accessibility elements on container views:

```swift
    infoView.accessibilityElements = [titleLabel, priceLabel, buyButton]
```

- In case of multiple text fields displayed, make sure that tapping "next" leads to the expected one.

    **Example:** Switching to the next text field via view tag:

```swift
    func textFieldShouldReturn(_ textField: UITextField) -> Bool {
        guard let nextResponder = textField.superview?.viewWithTag(textField.tag + 1) else {
            textField.resignFirstResponder() // No upcoming text field, hide keyboard.
            return true
        }
        nextResponder.becomeFirstResponder() // Switch to next text field.
        return true
    }
```

#### 🚫 Failures

- VoiceOver: Elements are being read out in the wrong order, or some elements are skipped.

- Focus is trapped within the modal and cycles between the elements. For example: In forms, the focus is switching between input fields but never onto a call-to-action button.

    **Example:** Trapped cycling between title and subtitle fields:

```swift
    func textFieldShouldReturn(_ textField: UITextField) -> Bool {
        if textField === titleField {
            subtitleField.becomeFirstResponder()
        } else {
            titleField.becomeFirstResponder()
        }
        return true
    }
```

### [Link Purpose (WCAG 2.4.4 - Level A)](../../principles/operable_principle.md#link-purpose-wcag-244---level-a)

#### ✅ Success technique(s)

- Create a button with content or title that helps people instantly understand what it does. I.e. try to use both icons and labels in buttons.
- Use short, concise titles that succinctly describe buttons purpose. Pair the button with descriptive text element that provides more information. For example; prefer `Visit` instead of `Tap here to visit www.google.com`
- Start the title of a button or link with a verb where possible.
- In attributed text, make sure to highlight any links. Avoid relying solely on a different color to highlight it – underscore and bold the link as well.

- When using custom elements that have a value that is not represented by its label (e.g., sliders, switches, etc.), make sure to configure its `accessibilityValue` property each time the value changes. Provide `accessibilityHint` where useful.

    **Example:** Updating accessibility value on a toggle-like button:

```swift
    class MuteButton: UIButton {
        override var isSelected: Bool {
            didSet {
                accessibilityValue = isSelected ? "Muted" : "Unmuted"
                accessibilityHint = "Double tap to " + (isSelected ? "unmute" : "mute")
            }
        }

        func setup() {
            accessibilityLabel = "Mute Switch"
            setImage(UIImage(named: "unmuted.png"), for: .normal)
            setImage(UIImage(named: "muted.png"), for: .normal)
        }
    }
```

- When using toggle buttons, avoid relying solely on color to communicate its state, i.e. whether it's disabled or selected:
  - Add a background shape
  - Change the button’s content too – e.g., change label text, opacity or size, or gray out the icon.
  - Add `accessibilityValue` and `accessibilityHint`. Disabled buttons are read out as "...dimmed button" out of the box.

- In dialogs, avoid using generic button titles like "Yes" and "No". Try to repeat verbs used in the question, for example: _Are you sure you want to delete this message? ▸ Delete  ▸ Cancel_
- In dialogs that confirm a canceling action, avoid using the verb "Cancel" again: _Are you sure you want to cancel your booking? This action is irreversible. ▸ Cancel Booking  ▸ Keep Booking_

#### 🚫 Failures

- Using custom-shaped buttons that do not look like buttons.
- Using generic and confusing button titles for canceling actions, for example: _"Are you sure you want to cancel your booking? This action is irreversible" ▸ OK  ▸ Cancel_
- Button titles with an unclear result like "Ready to publish?"

### [Heading and Labels (WCAG 2.4.6 - Level AA)](../../principles/operable_principle.md#heading-and-labels-wcag-246---level-aa)

#### ✅ Success technique(s)

- VoiceOver: When the user requests the entire screen to be read from the top, make sure that the title is one of the first things the user will hear so they know whether they are on the right page or step.

    **Example**: Setting view controller's title in `viewDidLoad`:

```swift
    func viewDidLoad() {
        super.viewDidLoad()
        title = "Sign up"
        // or
        navigationItem.title = "Sign up"
    }
```

In general, try to make the titles and labels as descriptive as possible. Also, in addition to that, you can always use an accessibility hint to provide more information about the element.

#### 🚫 Failures

The following should be avoided:

- Not providing a title or label for the content that follows
- Providing a missing or incorrect title or label

### [Focus Visibility (WCAG 2.4.7 - Level AA)](../../principles/operable_principle.md#focus-visibility-wcag-247---level-aa)

#### ✅ Success technique(s)

Even though, the system automatically handles this, think about selection and focus on custom elements; make sure that the focus is visible in a correct way and that the user can see which element is currently selected, especially if the component contains "inner" elements.

### [Focus Not Obscured (Minimum) (WCAG 2.4.11 - Level AA)](../../principles/operable_principle.md#focus-not-obscured-minimum-wcag-2411---level-aa)

#### ✅ Success technique(s)

When creating a view or a screen, think about the visibility of the focus and make sure that the user can see which element is currently selected.

To satisfy this guideline, check the following:

- The content is scrollable (when needed)
- The element is not obscured by other elements
- The element is (at least) partially visible when focused/used

#### 🚫 Failures

The following should be avoided:

- The focus is obscured by other elements
- Element is hidden due to inability to scroll or another element of the screen (e.g. sticky footer or floating element)

## [Input modalities (WCAG 2.5)](../../principles/operable_principle.md#input-modalities-wcag-25)

### [Label in Name (WCAG 2.5.3 - Level A)](../../principles/operable_principle.md#label-in-name-wcag-253---level-a)

#### ✅ Success technique(s)

A user should be able to understand and get the information about the label on which is focused. And to satisfy this criterion, the following should be done:

- an accessibility label should match the visible label name, or
- include the text of the visible label as a part of the accessibility label

```swift
let label = UILabel(frame: .zero)
label.text = "First name"
label.accessibilityLabel = "First name"
```

#### 🚫 Failures

As a failure to this criterion, the following should be avoided:

- not including the text of the visible label as a part of the accessibility label
- words of visible label and accessibility label not matching (e.g. not the same order)

### [Motion Actuation (WCAG 2.5.4 - Level A)](../../principles/operable_principle.md#motion-actuation-wcag-254---level-a)

#### ✅ Success technique(s)

To satisfy this criterion, the application should provide an alternative way to perform the action that is not based on device motion. In this case, this would be a component on the user interface that will give to the user the same functionality. For example, if the application uses a shake gesture to undo an action, it should also provide an undo button.

#### 🚫 Failures

The application should avoid using only one way of input to perform an action - in case when that is not a standard way of input (e.g. device motion).

### [Dragging Movements (WCAG 2.5.7 - Level AA)](../../principles/operable_principle.md#dragging-movements-wcag-257---level-aa)

#### ✅ Success technique(s)

To support this criterion, the application should provide an alternative way to perform the action that is not based on dragging movements. For this scenarios, on iOS, accessibility custom actions are introduced to provide an alternative way to perform the action. With a custom action, the user gets additional context menu which shows available actions for the element.

```swift
let addToCardAction = UIAccessibilityCustomAction(name: "Add to card") { _ in
    self?.addProductToCard(product)
    return true
}

self.accessibilityCustomActions = [addToCardAction]
```

Examples for custom actions can be found in applications like Mail where the user can delete, reply, or forward an email by dragging the element right or left. And to provide an alternative way to perform the action, the user can use the context menu due to custom action implementation.

#### 🚫 Failures

If the application does not provide an alternative way to perform the action that is not based on dragging movements, it will fail to satisfy this criterion.

### [Target Size (Minimum) (WCAG 2.5.8 - Level AA)](../../principles/operable_principle.md#target-size-minimum-wcag-258---level-aa)

#### ✅ Success technique(s)

Even though this is mostly a design guideline, it is important that from the development side, the application provides enough space for the elements to be easily operable by touch. The minimum target size is set to 48x48 points.

Still, there are some exceptions to this rule:

- **Spacing**: Undersized targets (those less than 48 by 48 points pixels) are positioned so that if a 48-point diameter circle is centred on the bounding box of each, the circles do not intersect another target or the circle for another undersized target;
- **Equivalent**: The function can be achieved through a different control on the same page that meets this criterion;
- **Inline**: The target is in a sentence or its size is otherwise constrained by the line-height of non-target text;
- **User agent control**: The size of the target is determined by the user agent and is not modified by the author;
- **Essential**: A particular presentation of the target is essential or is legally required for the information being conveyed.
