 [🔼 Accessibility principles and examples](../../principles/accessibility_principles_and_examples.md  "Accessibility principles and examples") | [⬅️ Operable principle](../../principles/operable_principle.md "Operable principle")

# Operable

User interface components and navigation must be operable.

## Enough Time (WCAG 2.2)

Provide users enough time to read and use the content.

### Timing Adjustable (WCAG 2.2.1 - Level A)

The user can turn off, adjust, or extend each time limit set by the content.

> This guideline covers point **2.2.1 Timing Adjustable - Level A of the WCAG standard.**

#### ✅ Success technique(s)

- Session inactivity timeout: Display a warning message that the user is about to be signed out with an extension option. Or allow the user to increase the default kick-out timeout time of inactivity ten times (e.g. from 30s to 5 min) so they have enough time to process content.

- Auto-updating content (like news page): allow the user to extend the time limit to 10 times longer.

- Real-time exception: time limit cannot be disabled/extended for a real-time event (e.g. an auction, booking movie tickets, watching live stream).

- In case you're using a custom modal presentation or a custom modal view, make sure that UIAccessibility is notified about the screen change.

#### 🚫 Failures

- Logging a user out of their session with no prior warning.
- Not providing enough time or time extensions to react to an incoming action in the app.


### Pause, Stop, Hide (WCAG 2.2.2 - Level A)

Moving, blinking, or scrolling, or auto-updating content in the app.

> This guideline covers point **2.2.2 Pause, Stop Hide - Level A of the WCAG standard.**

#### ✅ Success technique(s)

- When using auto-scrolling page views (carousels) which animation starts automatically, make sure to provide a way for the user to pause, stop, or hide it.
- If there is no parallel content next to the moving, blinking, or scrolling content, there's no need to provide a pause, stop, or hide button.
- Loading screens doesn't require meeting this success criterion.

#### 🚫 Failures

- Using an auto-updating or auto-scrolling view that can't be paused/stopped.

## Seizures and Physical Reactions (WCAG 2.3)

Do not design content in a way known to cause seizures or physical reactions.

### Three Flashed or Below Threshold (WCAG 2.3.1 - Level A)

Apps should not contain any element that flashes more than three times in one second.

> This guideline covers point **2.3.1 - Level A of the WCAG standard.**

#### ✅ Success technique(s)

- Avoid flashing content altogether if possible.
- If using flashing content – make sure that any flashing elements have a period of at least 333 ms.
- If you do have an element that flashes more frequently – ensure that the flashing area is less than 25% of 10 degrees of the visual field.

#### 🚫 Failures

- Using rapidly flashing elements to catch the user's attention.
- Having a larger area of screen flashing more than three times per second.

## Navigable (WCAG 2.4)

_Provide ways to help users navigate, find content, and determine where they are._

### Bypass Blocks (WCAG 2.4.1 - Level A)

A skip mechanism is available to bypass blocks of content that are repeated in the app.

> This guideline covers point **2.4.1 Bypass Blocks - Level A of the WCAG standard.**

#### ✅ Success technique(s)

- VoiceOver: A section of a screen containing numerous items should have those items grouped and an accessibility label with a quick summary of the contents. This way, if they are relevant to the user, the user may swipe up or down to iterate through each item, and in case they are not, the user may use a left or right swipe to skip them.

- An element containing many labels or buttons should also have a summary accessibility label so it takes fewer swipes to skip over it.

    **Example**: VoiceOver In Instagram main feed - Instagram stories are contained inside an "adjustable" accessibility group named "Stories Tray".

    1. User arrives to the "Stories Tray" by tapping or using the right swipes.
    2. VoiceOver announces the group’s name and quick summary with an "adjustable" hint at the end.
    3. User can then iterate through items (adjust) by swiping up and down.
    4. Once done reviewing stories, the user can read right-swipe to skip to the next element on the screen.

    If you want to try this out for yourself, we've prepared an [example project](https://github.com/infinum/ios-accessibility-demo) where we've recreated this exact behavior.

#### 🚫 Failures

Not providing a way for the user to quickly skip over sections with numerous items.

### Page Titled (WCAG 2.4.2 - Level A)

Screens have a clear, descriptive, and possibly unique title that describes the topic or purpose and is easily understood by all users.

> This guideline covers point **2.4.2 Page Titled - Level A of the WCAG standard.**

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

### Focus Order (WCAG 2.4.3 - Level A)

VoiceOver: Ensure that information is read in an order consistent with the meaning and content.

> This guideline covers point **2.4.3 Focus Order - Level A of the WCAG standard.**

#### ✅ Success technique(s)

- VoiceOver: When designing a new screen, make sure to test it with VoiceOver and see whether the elements are read in the right, logical order. The easiest way to achieve a correct focus order is to layout elements inside a `UIStackView`. VoiceOver will read elements in the same order as in the interface builder document outline.
Keep in mind: when placed outside a stack view, elements positioned closer to the top are read first. If elements are near the same vertical position, leading-side elements are read first.

– To change focus order, create an array of subviews and assign it to their parent container's `accessibilityElements`.

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

### Action Purpose (WCAG 2.4.4 - Level A)

The purpose of a button or link action is clear and easily understandable by all users

> This guideline covers point **2.4.4 Link Purpose (In Context) - Level A of the WCAG standard.**

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

⎯

[← Perceivable principle](../../principles/operable_principle.md "Operable principle")
