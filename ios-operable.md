# Operable

User interface components and navigation must be operable.

## 2.2 Enough Time

_Provide users enough time to read and use content._

### Timing Adjustable

For each time limit set by the content, user can turn off, adjust, or extend it.

#### ✅ Success technique(s)

- Session inactivity timeout: Display a warning message that user is about to be signed out with extension option. Or allow user to increase default kick-out timeout time of inactivity ten times (e.g. from 30s to 5 min) so they have enough time to process content.

- Auto-updating content (like news page): allow user to extend the time limit to 10 times longer.

- Real-time exception: time limit cannot be disabled/extended for a real-time event (e.g. an auction, booking movie tickets, watching live stream).

- In case you're using a custom modal presentation or a custom modal view, make sure that UIAccessibility is notified about the screen change.

#### 🚫 Failures

- Logging user out of their session with no prior warning.
- Not providing enough time or time extensions to react on an incoming action in the app.

#### Additional notes

This guideline covers point 2.2.1 Timing Adjustable - Level A of the WCAG standard.

---

### Pause, Stop, Hide

Moving, blinking, or scrolling, or auto-updating content in the app.

#### ✅ Success technique(s)

- When using auto-scrolling page views (carousels) whose animation starts automatically make sure to provide a way for user to pause, stop, or hide it.
- If there is no parallel content next to the moving, blinking, or scrolling content there's no need to provide a pause, stop or hide button.
- Loading screens doesn't require to meet this success criterion.

#### 🚫 Failures

- Using an auto-updating or auto-scrolling view that can't be paused/stopped.

#### Additional notes

This guideline covers point 2.2.2 Pause, Stop Hide - Level A of the WCAG standard.

---


## 2.3 Seizures and Physical Reactions

_Do not design content in a way that is known to cause seizures or physical reactions._

### Three Flashed or Below Treshold

Apps should not contain any element that flashes more than three times in any one second period.

#### ✅ Success technique(s)

- Avoid flashing content altogether if possible. 
- If using flashing content - make sure that any flashing elements have a period of at least 333 ms.
- If you do have an element that flashes more frequently - ensure that the flashing area is less than 25% of 10 degrees of visual field.

#### 🚫 Failures

- Using rapidly flashing elements to catch user's attention.
- Having a larger area of screen flashing more than three times per second.

#### Additional notes

This guideline covers point 2.3.1 - Level A of the WCAG standard.

---

## 2.4 Navigable

_Provide ways to help users navigate, find content, and determine where they are._

### Bypass Blocks

A skip mechanism is available to bypass blocks of content that are repated in the app.

#### ✅ Success technique(s)

- VoiceOver: A section of a screen containing numerous items should have those items grouped and an accessibility label with quick summary of the contents. This way if they are relevant to the user, user may swipe up or down to iterate through each item, and in case they are not user may use left or right swipe to skip them.

- An element containing many labels or buttons should also have a summary accessibility label so it takes less swipes to skip over it.

    **Example**: VoiceOver In Instagram main feed - Instagram stories are contained inside an "adjustable" accessibility group named "Stories Tray".
    
    1. User arrives to the "Stories Tray" by either tapping it or using right swipes.
    2. VoiceOver announces the name and quick summary of this group, with "adjustable" hint at the end.
    3. User can then iterate through items (adjust) by swiping up and down.
    4. Once done reviewing stories, user can then right swipe to skip onto the next element on the screen.
       
    
    If you want to try this out for yourself, we've prepared an [example project](https://github.com/infinum/ios-accessibility-demo) where we've recreated this exact behavior.

#### 🚫 Failures

Not providing a way for user to quickly skip over sections with numerous items.

#### Additional notes

This guideline covers point 2.4.1 Bypass Blocks - Level A of the WCAG standard.

---


### Page Titled

Screens have a clear, descriptive, and possibly unique title that describes topic or purpose and is easily understood by all users.

#### ✅ Success technique(s)

- VoiceOver: when user requests entire screen to be read from the top, make sure that the title is one of the first things user will hear so they know whether they are on the right page or step.

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
- In document-editor screens avoid using:
  - default titles like "Untitled Document" or "No Title"
  - file names like "report.pdf" or "DSC_0123.jpeg"
  - placeholder text like "Enter title..." or "Search..."

#### Additional notes

This guideline covers point 2.4.2 Page Titled - Level A of the WCAG standard.

---


### Focus Order

VoiceOver: Ensure that information is read in an order consistent with the meaning and content.

#### ✅ Success technique(s)

- VoiceOver: When designing a new screen, make sure to test it with VoiceOver and see whether the elements are being read out in right, logical order. Easiest way to achieve correct focus order is to layout elements inside a `UIStackView`. VoiceOver will read elements in the same order as in interface builder document outline. 
Keep in mind: when placed outside a stack view, elements positioned closer to the top are read first. If elements are near same vertical position, leading-side elements are read first.

- To change focus order, create an array of subviews and assign it to their parent container's `accessibilityElements`.

   **Example:** Setting accessibility elements on container views:
```swift
    infoView.accessibilityElements = [titleLabel, priceLabel, buyButton]
```

- In case of multiple text fields displayed, make sure that tapping "next" leads to the expected one.

    **Example:** Switching to next text field via view tag:
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

- Focus is trapped within the modal and cycles between the elements. For example: In forms, focus is switching between input fields but never onto an call-to-action button.

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
#### Additional notes

This guideline covers point 2.4.3 Focus Order - Level A of the WCAG standard.

---


### Action Purpose

Purpose of a button or link action is clear and easily understandable by all users

#### ✅ Success technique(s)

- Create button with content or title that helps people instantly understand what it does. I.e. try to use both icons and labels in buttons.
- Use short, concise titles that succinctly describe buttons purpose. Pair the button with descriptive text element that provides more information. For example; prefer `Visit` instead of `Tap here to visit www.google.com`
- Start the title of a button or link with a verb where possible.
- In attributed text, make sure to highlight any links. Avoid relying solely on a different color to highlight it - underscore and bold the link as well.

- When using custom elements that have a value that is not represented by its label (e.g. sliders, switches etc) make sure to configure its `accessibilityValue` property each time value changes. Provide `accessibilityHint` where useful.

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

- When using toggle buttons, avoid relying solely on color to communicate its state, i.e. whether it's disabled, or selected:
    - Add a background shape
    - Change the button’s content too - e.g. change label text, opacity or size, or gray out icon.
    - Add `accessibilityValue` and `accessibilityHint`. Disabled button are read out as "...dimmed button" out of the box.

- In dialogs, avoid using generic button titles like "Yes" and "No". Try to repeat verbs used in the question, for example:
*Are you sure you want to delete this message? 
▸ Delete  ▸ Cancel*
- In dialogs that confirm a cancelling action, avoid using the verb "Cancel" again:
*Are you sure you want to cancel your booking? This action is ireversible.
▸ Cancel Booking  ▸ Keep Booking*

#### 🚫 Failures

- Using custom shaped buttons that do not look like buttons.
- Using generic and confusing button titles for cancelling actions, for example: 
*"Are you sure you want to cancel your booking? This action is ireversible" 
▸ OK  ▸ Cancel*
- Button titles with unclear result like "Ready to publish?"

#### Additional notes

This guideline covers point 2.4.4 Link Purpose (In Context) - Level A of the WCAG standard.

---