 [🔼 Accessibility principles and examples](a../../principles/accessibility_principles_and_examples.md  "Accessibility principles and examples") | [⬅️ Perceivable principle](../../principles/perceivable_principle.md "Perceivable principle")

# Perceivable guidelines for iOS

Information and user interface components must be presentable to users in ways they can perceive.

## [Text alternatives (WCAG 1.1)](#wcag-11)

Provide text alternatives for any non-text content to be changed into other forms people need, such as large print, braille, speech, symbols, or more straightforward language.

### [Non-text content identification (WCAG 1.1.1 - Level A)](#wcag-111)

When talking about the screen elements, it is important to make information about all elements accessible and available. Some elements may not have text included by design or as a default user interface component. This can be seen when buttons are used with icons only, images, or other decorative elements.

Some users may have issues identifying an element's functionality or description in general, and because of that, it is important to define non-text elements by accessibility features.

> This guideline with provided techniques covers the *1.1.1 Non-text Content - Level A of the WCAG standard.*

#### ✅ Success technique(s)

##### Using accessibility labels

The most important technique is to define accessibility labels on non-text components to be easily used with assistive technology and understandable by users.

```swift
addButton.accessibilityLabel = "Add"
```

When talking about group components or containers on the screen, it is an excellent approach to give them names and make navigating with assistive technology much easier and more understandable.

Another important thing about labeling elements is the context. Some static elements, like images, provide a context, like an image with the alert or check element. In that case, instead of setting the label as a "check icon", it can be defined as "successful submission" to give the user more information.

#### Using accessibility value and hint

Alongside the accessibility label, iOS as a platform supports the definition of an accessibility value and accessibility hint. If some elements can have and should provide specific values, accessibility value can be used alongside the accessibility label. And when talking about element interactivity, accessibility hints can be used as well – but be aware that the user can disable them.

```swift
addButton.accessibilityHint = "Adds a new task"
```

#### 🚫 Failures

Sometimes it is not a good idea to give accessibility labels to all screen elements. Some elements may only be defined as decorative elements that do not affect the screen functionality (e.g. small elements like images used for screen decoration). In that case, labeling elements like that may confuse the user.

## [Time-based Media (WCAG 1.2)](#wcag-12)

Provide alternatives for time-based media.

### [Captions support for prerecorded media (WCAG 1.2.1 and 1.2.2 - Level A)](#wcag-121-and-122)

Due to some disabilities, some users may not be able to hear the content of the media provided by the application. An example of that can be a prerecorded audio or video track. In some cases, it is necessary to add support for some accessibility features to make this content accessible to all users.

> This guideline with provided techniques covers the *1.2.1 Audio-only and Video-only (Prerecorded) - Level A and 1.2.2 Captions (Prerecorded) - Level A of the WCAG standard.*

#### ✅ Success technique(s)

##### Using AVPlayer with captions

One way of making the prerecorded media accessible is by adding captions. Most modern software supports adding captions to the video, and `AVPlayer` from `AVFoundation` automatically supports it.

To be able to see captions in media that contains it, the user needs to have *Closed Captions* enabled. This accessibility feature can be toggled in *Settings > Accessibility > Subtitles & Captioning > Closed Captions + SDH*.

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

The details about adding captions to the `AVPlayer` (from `AVFoundation`) can be found in the [documentation](https://developer.apple.com/documentation/avfoundation/media_assets_playback_and_editing/adding_subtitles_and_alternative_audio_tracks).

### [Audio Description or Media Alternative (WCAG 1.2.3 - Level A)](#wcag-123)

People that have vision disability may have issues with understanding the content of a video. To make the video accessible to all users, it is important to provide an audio description of the video content.

> This guideline with provided techniques covers the *1.2.3 Audio Description or Media Alternative (Prerecorded) - Level A of the WCAG standard.*

#### ✅ Success technique(s)

To satisfy this guideline, there are two ways of providing an audio description:

* provide an audio description of the video content
* provide a text alternative for synchronized media

##### Using audio description

When talking about the audio description, it is important to provide a description of the video content. This can be done by:

* adding a separate audio track to the video that describes the video content
* providing a video version file with audio description
* providing a video with extended audio description

##### Using text alternative

As a text alternative, a transcript of the video content can be provided with additional description added. This way, users can read the content of the video if they are not able to see it.
In cases when "talking-head" video is used, a static text alternative can be provided as a description.

##### Using transcripts

Supplying transcripts is another way of providing users with information in prerecorded audio or video. If defined correctly, text on the screen can be read by VoiceOver for people with visibility issues, while people with hearing issues can read the transcript. This way, both scenarios are satisfied without a need to provide captions.

#### 🚫 Failures

If none of provided success criteria are met, the user may have issues understanding the content of the video. This can lead to a bad user experience and a lack of information, and in the end, the failure of this guideline.

### [Captions support for live media (WCAG 1.2.4 - Level AA)](#wcag-124)

In some cases, live media is used in the application. To make this content accessible to all users, it is important to provide captions for the live media.

> This guideline with provided techniques covers the *1.2.4 Captions (Live) - Level AA of the WCAG standard.*

#### ✅ Success technique(s)

For every live media that is used in the application, we should provide captions through the user interface. This can be archived as:

* live captions that are embedded in the real-time media
* live captions that are available in the real-time media stream (can be programmatically added to the video)

The second approach is much more customizable, and can provide much more than embedded captions. Still, this approach requires work on the client side to make it work. Please check documentation mentioned in the [Captions support for prerecorded media (WCAG 1.2.1 and 1.2.2 - Level A)](#wcag-121-and-122) and [here](https://developer.apple.com/streaming/) for more information about HTTP live streaming on Apple platforms.

### [Audio Description for Prerecorded Media (WCAG 1.2.5 - Level AA)](#wcag-125)

As a part of this guideline, it is important to provide an audio description for prerecorded video content.

> This guideline with provided techniques covers the *1.2.5 Audio Description (Prerecorded) - Level AA of the WCAG standard.*

#### ✅ Success technique(s)

This guideline is closely related to the [Audio Description or Media Alternative (WCAG 1.2.3 - Level A)](wcag-123) guideline, which basically says that the video content should be described in an audio track, without any alternative (as described in the previous guideline).

This can be done in the main track (media) or by providing an additional audio track that describes the video content.

*Note: Based on the guideline itself, if all of the information in the video track is already provided in the audio track, no audio description is necessary. This applies to both guidelines (1.2.3 and 1.2.5).*

## [Adaptable (WCAG 1.3)](#wcag-13)

Create content that can be presented differently without losing information or structure.

### [Element information and relationship (WCAG 1.3.1 - Level A)](#wcag-131)

Every accessible element on the screen should hold information about itself, and it should be identifiable. From the web perspective, this is defined as a definition of the regions and elements on the page, while on the mobile side, this can be used to identify components or different areas of the page.

Moreover, when thinking about a given part of an application, it is important to make the layout structure logical and easy to use. With that in mind, semantic views that use accessibility features like VoiceOver may improve user experience. With that in hand goes the definition of the relationship, or connected elements (via container) – to give the user more context.

> This guideline with provided techniques covers the *1.3.1 Info and Relationships - Level A of the WCAG standard.*

#### Element information

Every accessibility element should hold information about itself, while its identification may be optional.

##### ✅ Success technique(s)

Most `UIKit` elements are accessibility elements by default. Still, if some of the elements should not be accessible or used as an accessibility element, that can be changed by setting the `isAccessibilityElement` to `false`.

Another important thing is to define the `accessibilityLabel` on all accessibility elements on a particular screen. Also, make sure to assign an accessibilityLabel on grouped or container views (e.g. form view). The important thing to mention here is to also add accessibility labels to groups or container views that hold multiple elements (e.g. form view).

The final thing to define an element is to set up its `accessibilityIdentifier`. The users do not see this property, and it's not used for accessibility features. Still, if component identification is needed for other purposes (like test automation), it can be set to identify different elements on the screen.

##### 🚫 Failures

When thinking about the accessibility information every application page will provide, it is bad practice to define all elements as accessibility elements. At the same time, some of them are not being used at all.

Also, as mentioned in "Non-text content identification" – not all elements need to have a label or be accessible by the user.

#### Element relationship

Many UI components should work together to create a context for the user. For example, if there is a list of components with two labels inside, one with a title and another for the value, it may be suitable to read those two labels as one sentence to give more context.

##### ✅ Success technique(s)

On iOS, we can use semantic views or, in other words, the accessibility container technique to create a relationship or give a better context of some (custom) component that may contain more components inside itself.

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

In this example, when the user goes through cells, there will be no need to go inside the cell to get detailed information. The sentence "This car model is a Porsche Carrera from the year 2020." will be read.

Also, if there is a need to define actions or gestures inside components like this, it is important to change the state of the `isAccessibilityElement`. In this case, the value for the cell should be set to `false`, while the action or a gesture (as a child) element should set that value to `true`. Another thing needed for this to work is to define `accessibilityElements` on the cell level.

#### 🚫 Failures

By not connecting or adding context to the elements or inner elements of the component, there is a chance to create a bad user experience and confusion in the app usage.

### [Meaningful sequence (WCAG 1.3.2 - Level A)](#wcag-132)

On iOS, screen elements are consumed from the top left to the bottom right. This is a standard way in which nearly all screens work correctly in most scenarios. Still, we should always provide the best experience to the user, even if elements are not structured in a preferred way.

> This guideline with provided techniques covers the *1.3.2 Meaningful Sequence - Level A of the WCAG standard.*

#### ✅ Success technique(s)

As mentioned in the "Element relationship", we can define sequences on the same or parent-child level to get the element’s context. We provide a better user experience and more information to the user by doing that.

Still, sometimes, we need to provide an exact order of the elements on some screen or inside some component. To define that, an array of `accessibilityElements` should be used. All elements defined in the array will be accessed in the order in which they are specified in the array.

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
    // Positioned at(v)
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

In this example, we changed the order of how elements will be read, and we’ve forced the system to read the button information last instead of the value label, which is the last element on the view.

#### 🚫 Failures

Even if we, as developers, control the order of the elements, try not to make sequences that are not logical or to produce "jumps" between UI components.

### [Sensory characteristics (WCAG 1.3.3 - Level A)](#wcag-133)

Instructions for understanding and operating content do not rely solely on sensory characteristics of components such as shape, color, size, visual location, orientation, or sound.

> This guideline with provided techniques covers the *1.3.3 Sensory characteristics - Level A of the WCAG standard.*

#### ✅ Success technique(s)

To make our app entirely understandable to the users, we should not rely only on one characteristic to show the user elements on the screen. You can find different ways to satisfy this aspect in the text below.

##### Differentiate without a color

When talking about color, it is important to know that not all people see colors in the same way, or don't see them at all. Because of that, on iOS, there is a feature in the system settings called "Differentiate without a color". By supporting this, and if the application’s design supports it, we can dynamically change the appearance of the elements based on user preference.

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

#### 🚫 Failures

Some of the failures regarding this aspect are:

* Creating elements that are not identifiable by design (e.g., a label and a button without a shape)
* Not applying design changes when user preferences change in system settings

### [Orientation (WCAG 1.3.4 - Level AA)](#wcag-134)

Content should not be restricted to operation in a single display orientation, such as portrait or landscape, unless a specific display orientation is essential.

> This guideline with provided techniques covers the *1.3.4 Orientation - Level AA of the WCAG standard.*

#### ✅ Success technique(s)

When talking about the orientation of the screen, it is important to make the application work in both portrait and landscape mode. This can be done by defining the supported orientations in the application settings (*project-target > General > Deployment Info > Device Orientation*).

Programmatically, this can be achieved on two levels; on the view controller level and on the application level. For the view level, the orientation can be defined by overriding the `supportedInterfaceOrientations` method, and setting the `shouldAutorotate` property to `true`.

From the application level, the orientation can be defined in the `AppDelegate` class by setting the `supportedInterfaceOrientationsFor` method.

#### 🚫 Failures

While thinking about orientation, the following implementations can be considered as failures:

* not supporting both horizontal and vertical orientations
* forcing user to re-orient the device to use it normally (e.g. usage of alert)

### [Identify input purpose (WCAG 1.3.5 - Level AA)](#wcag-135)

In forms, every input field should indicate a purpose of the input for ease of use. With this guideline, the autocomplete feature should be added to the input fields, but the mobile platforms does not support that.

Still, to support this as much as possible, every input should at least define type of input (e.g., email, password, phone number, etc.).

> This guideline with provided techniques covers the *1.3.5 Identify Input Purpose - Level AA of the WCAG standard.*

#### ✅ Success technique(s)

To support type of the input and different keyboard state, always define the `keyboardType` (`UIKeyboardType`) for every text field to support easier input from users. With that defined, the keyboard will show the correct layout for the user to input the data. In addition to that, try to define a `returnKeyType` (`UIReturnKeyType`) to support the user in the form completion.

#### 🚫 Failures

If the wrong input layout (e.g., keyboard type) is used for the input field, the user may have issues with entering the data. This can lead to a bad user experience and a failure of this guideline.

## [Distinguishable (WCAG 1.4)](#wcag-14)

Make it easier for users to see and hear content including separating foreground from background.

### [Resizeable text (WCAG 1.4.4 - Level AA)](#wcag-144)

The text should be resizeable up to 200% without loss of content or functionality. This applies to every text content on the screen except captions and images of text.

> This guideline with provided techniques covers the **1.4.4 Resizeable Text - Level AA of the WCAG standard.*

#### ✅ Success technique(s)

To support this guideline, the application should support the dynamic type. If a system font is used, this is already supported by default.

In case when a custom font is used, it is important to support the dynamic type by setting the `adjustsFontForContentSizeCategory` property to `true`, which will affect the label to change its font size based on changes in accessibility setting. Also, the custom font should be scaled, and that is done by setting the `UIFontMetrics` object to the font.

```swift
label.font = UIFontMetrics(forTextStyle: .body).scaledFont(for: customFont)
label.adjustFontForContentSizeCategory = true
```

It is important that we can limit the font size (when custom font is used) to a specific value, but the minimum enlargement of 200% of the font size should be supported. This can be done by setting the `maximumContentSizeCategory` to the specific value. Read more about content size categories [here](https://developer.apple.com/documentation/uikit/uicontentsizecategory).

#### 🚫 Failures

As a part of this guideline, the following failures can be considered:

* Not supporting the dynamic type
* The content is not resizable up to 200%

### [Images of text (WCAG 1.4.5 - Level AA)](#wcag-145)

Where components with image of text are used, they cannot satisfy the other guidelines due to image constraints. E.g., the text in the image cannot be resized which breaks the guideline 1.4.4. To avoid that, use of images of text should be avoided, or at least a text alternative should be provided.

This does not affect components which are essential for the functionality of the application, like logos or branding images.

> This guideline with provided techniques covers the *1.4.5 Images of Text - Level AA of the WCAG standard.*

#### ✅ Success technique(s)

Try to use text instead of images of text to make the component more flexible and easier to use. If that is not possible, provide a text alternative for the image of text. This can be done by setting the `accessibilityLabel` to the image view.

#### 🚫 Failures

If the image of text is used without a text alternative, that will result in a failure of this guideline.

### [Reflow (WCAG 1.4.10 - Level AA)](#wcag-1410)

The reflow is basically another name to responsible design in this context. The content should be able to reflow from one screen size to another without losing information or functionality.

> This guideline with provided techniques covers the *1.4.10 Reflow - Level AA of the WCAG standard.*

#### ✅ Success technique(s)

Every component on the screen should be able to reflow from one screen size to another. This can be achieved by using the auto layout and size classes in the storyboard. Also, the dynamic type should be supported to make the text reflowable.

This should not be done only on the screen level, but also on the component level. Every component should be able to reflow from one size to another without losing information or functionality (e.g., buttons, labels, images, etc.). The simple example of this would be a broken text (label), wrong size of the button, etc.

#### 🚫 Failures

If the content is not responsible to different sizes, it may be broken and not usable on some screen sizes. This can lead to a bad user experience and a failure of this guideline. This could be highly visible when the user changes the system font size or when the user changes the device orientation.

## [Other perceivable guidelines](#other-perceivable-guidelines)

This section contains guidelines that may not applicable for the mobile (iOS) platform, or its criteria is a not the responsibility of the mobile team. Still, take into account that those guidelines needs to be satisfied.

* [WCAG 1.4.1 Use of Color - Level A](https://www.w3.org/WAI/WCAG22/quickref/#use-of-color)
* [WCAG 1.4.2 Audio Control - Level A](https://www.w3.org/WAI/WCAG22/quickref/#audio-control)
* [WCAG 1.4.3 Contrast (Minimum) - Level AA](https://www.w3.org/WAI/WCAG22/quickref/#contrast-minimum)
* [WCAG 1.4.11 Non-text Contrast - Level AA](https://www.w3.org/WAI/WCAG22/quickref/#non-text-contrast)
* [WCAG 1.4.12 Text Spacing - Level AA](https://www.w3.org/WAI/WCAG22/quickref/#text-spacing)
* [WCAG 1.4.13 Content on Hover or Focus - Level AA](https://www.w3.org/WAI/WCAG22/quickref/#content-on-hover-or-focus)

⎯

[← Perceivable principle](../../principles/perceivable_principle.md "Perceivable principle")
