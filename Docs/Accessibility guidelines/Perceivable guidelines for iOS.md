# Perceivable guidelines for iOS

Information and user interface components must be presentable to users in ways they can perceive.

## Text alternatives

Provide text alternatives for any non-text content to be changed into other forms people need, such as large print, braille, speech, symbols, or more straightforward language.

### Non-text content identification

When talking about the screen elements, it is important to make information of all elements accessible and available. Some elements may not have text included by design or as a default user interface component. This can be seen when buttons are used with icons only, images, or other decorative elements.

Some users may have issues identifying elements’ functionality or description in general, and because of that, it is important to define non-text elements by accessibility features.

#### Success techniques

##### Using accessibility labels

The most important technique is to define accessibility labels on non-text components to be easily used with assistive technology and understandable by users.

```swift
addButton.accessibilityLabel = "Add"
```

When talking about group components or containers on the screen, it is an excellent approach to give them names and make navigating with assistive technology much easier and understandable.

Another important thing about labeling elements is the context. Some static elements like images provide a context, like an image with the alert or thick element. In that case, instead of setting the label as a "thick image”, it can be defined as “successful submission" to give the user a bit more information.

#### Using accessibility value and hint

Alongside the accessibility label, iOS as a platform supports the definition of the accessibility value and accessibility hint. If some elements can have and should provide specific values, accessibility value can be used alongside the accessibility label. And when talking about element interactivity, accessibility hint can be used as well - but be aware that the user can disable accessibility hint.

```swift
addButton.accessibilityHint = "Adds a new task"
```

#### Failures

Sometimes it is not a good idea to give accessibility labels to all screen elements. Some elements may only be defined as decorative elements that do not affect the screen functionality (e.g., small elements like images used for screen decoration). In that case, labeling elements like that may confuse the user.

#### Additional notes

This guideline with provided techniques covers the 1.1.1 Non-text Content - Level A of the WCAG standard.

## Time-based Media

Provide alternatives for time-based media.

### Captions support for prerecorded media

Due to some disabilities, some users may not be able to hear the content of the media provided by the application. An example of that can be prerecorded audio or video track. In some cases it is necessary to add support for some accessibility features to make this content accessible to all users.

#### Success techniques

##### Using AVPlayer with captions

One way of making the prerecorded media accessible is by adding captions. Most modern software supports adding captions to the video, and `AVPlayer` from `AVFoundation` automatically supports it.

To be able to see captions in media that contains it, user needs to have *Closed Captions* enabled. This accessibility feature can be toggled in *Settings > Accessibility > Subtitles & Captioning > Closed Captions + SDH*.

##### Custom solution with accessibility notifications

If another solution is used (instead of `AVPlayer`), the status of the closed captioning can be checked via `UIAccessibility.isClosedCaptioningEnabled` or by subscribing to the notification `UIAccessibility.closedCaptioningStatusDidChange`.

```swift
import UIKit

final class VideoViewController: UIViewController {

    var isClosedCaptioningEnabled: Bool {
        return UIAccessibility.isClosedCaptioningEnabled
    }

    override func viewDidLoad() {
        super.viewDidLoad()

        NotificationCenter.default.addObserver(
            self,
            selector: #selector(closedCaptioningStatusDidChanged),
            name: UIAccessibility.closedCaptioningStatusDidChangeNotification,
            object, nil
        )
    }

    deinit {
        NotificationCenter.default.removeObserver(self)
    }

    @objc
    func closedCaptioningStatusDidChanged(_ notification: Notification) {
        if isClosedCaptioningEnabled {
            // Show captions
        } else {
            // Hide captions
        }
    }
}
```

##### Using transcripts

Supplying transcripts is another way of providing users with information in prerecorded audio or video. If defined correctly, text on the screen can be read by VoiceOver for people with visibility issues, while people with hearing issues can read the transcript. This way, both scenarios are satisfied without a need to provide captions.

#### Additional notes

This guideline with provided techniques covers the 1.2.1 Audio-only and Video-only (Prerecorded) - Level A and 1.2.2 Captions (Prerecorded) - Level A of the WCAG standard.

## Adaptable

Create content that can be presented differently without losing information or structure.

### Element information and relationship

Every accessible element on the screen should hold information about itself, and it should be identifiable. From the web perspective, this is defined as a definition of the regions and elements on the page, while on the mobile side, this can be used to identify components or different areas of the page.

Moreover, when thinking about application screen, it is important to make the screen structure logical and easy to use. With that in mind, semantic views that use accessibility features like VoiceOver may improve user experience. With that in hand goes the definition of the relationship, or connected elements (via container) - to give the user more context.

#### Element information

Every accessibility element should hold information about itself, while its identification may be optional.

##### Success techniques

Most of `UIKit` elements are accessibility elements by default. Still, if some of the elements should not be accessible or used as an accessibility element, that can be changed by settings the `isAccessibilityElement` to `false`.

Another important thing is to define the `accessibilityLabel` to all accessibility elements on a particular screen. Also make sure to assign an accessibilityLabel on grouped or container views (e.g. form view). The important thing to mention here is also to add accessibility labels to, e.g., groups or container views that hold multiple elements (e.g., form view).

The final thing to identify the element is to setup its `accessibilityIdentifier`. The users do not see this property and are not used for accessibility features. Still, if component identification is needed for other purposes (like test automation), it can be set to identify different elements on the screen.

##### Failures

When thinking about accessibility information every application page will provide, it is bad to define all elements as accessibility elements. At the same time, some of them are not being used at all.

Also, as mentioned in "Non-text content identification" ﹣ not all elements need to have a label nor be accessible by the user.

#### Element relationship

Many UI components should work together to create a context for the user. For example, if there is a list of components with two labels inside, one with a title and another for the value, it may be good to read those two labels as one sentence to give more context.

##### Success techniques

In iOS, we can use semantic views or, in other words, the accessibility container technique to create a relationship or give a better context of some (custom) component that may contain more components inside itself.

```swift
import UIKit

final class CarDetailsTableViewCell: UITableViewCell {

    // Subview of `self`
    @IBOutlet private var contentView: UIView!
    // Subview of `contentView`
    @IBOutlet private weak var titleLabel: UILabel!
    // Subview of `contentView`
    @IBOutlet private weak var modelLabel: UILabel!
    // Subview of `contentView`
    @IBOutlet private weak var yearLabel: UILabel!

    func configureCell(...) {
        ...
        configureAccessibility()
    }

    private func configureAccessibility() {
        contentView.isAccessibilityElement = true

        // Scenario: 
        //   - titleLabel.text = "Car model"
        //   - modelLabel.text = "Porsche Carrera"
        //   - yearLabel.text = "2020"
        contentView.accessibilityLabel = "This \(titleLabel.text) is a \(modelLabel.text) from year \(yealLabel.text)."
    }
}
```

In this example, when the user goes through cells, there will be no need to go inside the cell to get detailed information. The sentence "This car model is a Porsche Carrera from year 2020." will be read.

Also, if there is a need to define actions or gestures inside components like this, it is important to change the state of the `isAccessibilityElement`. In this case, the value for the cell should be set to `false`, while the action or a gesture (as a child) element should set that value to `true`. One other thing needed for this to work is to define `accessibilityElements` on the cell level.

#### Failures

By not connecting or adding context to the elements or inner elements of the component, there is a chance to create a bad user experience and confusion in the app usage.

### Meaningful sequence

In iOS, screen elements are consumed from the top left to the bottom right. This is a standard way in which most screens work correctly in most scenarios. Still, we should always provide the best experience to the user, even if elements are not structured in a preferred way.

#### Success techniques

As mentioned in the "Element relationship", we can define sequences on the same or parent-child level to get the element’s context. We provide a better user experience and more information to the user by doing that.

Still, sometimes, we need to provide an exact order of the elements on some screen or inside some component. To define that should be used an array of` accessibilityElements`. All elements defined in the array will be accessed in the order of how they are specified in the array.

```swift
final class SomeViewController: UIViewController {

    // ____________________
    // | (d)              |
    // |              (i) |
    // |_(v)______________|
    //

    // Positioned at (i)
    @IBOutlet private weak var infoButton: UIButton!
    // Positioned at (d)
    @IBOutlet private weak var descriptionLabel: UILabel!
    // Positined at(v)
    @IBOutlet private weak var valueLabel: UILabel!
    

    override var accessibilityElements: [Any]? {
        return [
            descriptionLabel,
            valueLabel,
            infoButton
        ]
    }
}
```

In this example, we changed the order of how elements will be read, and we’ve forced to read the button information last instead of the value label, which is the last element on the view.

#### Failures

Even if we as developers control the order of the elements, try not to make sequences that are not logical or to produce "jumps" between UI components.

### Sensory characteristics

Instructions provided for understanding and operating content do not rely solely on sensory characteristics of components such as shape, color, size, visual location, orientation, or sound.

#### Success techniques

To make our app entirely understandable to the users, we should not rely only on one characteristic to show the user elements on the screen. You can find different ways to satisfy this aspect in the text below.

##### Differentiate without a color

When talking about color, it is important to know that not all people see the colors in the same way, or they don't see colors at all. Because of that, on iOS, there is a feature in the system settings called "Differentiate without a color". By supporting this, and if the application’s design supports it, we can dynamically change the appearance of the elements based on the user preference.

```swift
import UIKit

final class BankAccountDetailsViewController: UIViewController {

    var shouldDifferentiateWithoutColor: Bool {
        return UIAccessibility.shouldDifferentiateWithoutColor
    }

    override func viewDidLoad() {
        super.viewDidLoad()

        NotificationCenter.default.addObserver(
            self,
            selector: #selector(differentiateWithoutColorDidChange),
            name: UIAccessibility.differentiateWithoutColorDidChangeNotification,
            object, nil
        )
    }

    deinit {
        NotificationCenter.default.removeObserver(self)
    }

    @objc
    func differentiateWithoutColorDidChange(_ notification: Notification) {
        if shouldDifferentiateWithoutColor {
            // Show "+" or "-" sign before the amount (+ color)
        } else {
            // Add the color to the label (e.g. show bank balance in red if below zero or green if zero or more.)
        }
    }
}
```

##### Button shapes

In the same way as "Differentiate without a color" can be used, "Button shapes" is another option in the system settings. To get the current status, you can use `UIAccessibility.buttonShapesEnabled` or add an observer for notification `UIAccessibility.buttonShapesEnabledStatusDidChangeNotification`.

You can define button shapes or different appearances of the buttons based on the provided designs.

#### Failures

Some of the failures regarding this aspect are:

* Creating elements that are not identifiable by design (e.g., a label and a button without a shape)
* Not applying design changes when user preferences change in system settings
