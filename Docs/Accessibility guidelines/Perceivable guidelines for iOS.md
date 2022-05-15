# Perceivable guidelines for iOS

Information and user interface components must be presentable to users in ways they can perceive.

## Text alternatives

Provide text alternatives for any non-text content so that it can be changed into other forms people need, such as large print, braille, speech, symbols or simpler language.

### Non-text content identification

When talking about elements of the screen, it is important to make information of all elements accessible and available. Some elements may not have text included by design or as a default user interface component. This can be seen in situations where buttons are used with icon only, images or other decorative elements.

Some users may have issues identifying elements functionality or description in general, and because of that it is important to define non-text elements by accessibility features.

#### Success techniques

##### Using accessibility labels

The most important technique is to define accessibility labels on non-text components, so they can be easily used with assistive technology and understandable by users.

```swift
addButton.accessibilityLabel = "Add"
```

When talking about group components or containers on the screen, it is a good approach to give them names as well to make navigating with assistive technology much easier and understandable.

Another important thing about labeling elements is the context. Some static elements like images provide a context, like image with alert or thick element. In that case, instead of setting the label as a "thick image" it can be defined as "successfull submission" to give the user a bit more information.

#### Using accessibility value and hint

Alongside accessibility label, iOS as a platform supports definition of the accessibility value and accessibility hint. If some elements can have and should provide specific values, accessibility value can be used alongside accessibility label. And when talking about element interactivity, accessibility hint can be used as well - but be aware, accessibility hint can be disabled by the user.

```swift
addButton.accessibilityHint = "Adds new task"
```

#### Failures

Sometimes it is not a good idea to give accessibility label to all elements of the screen. Some elements may be only defined as decorative elements that does not affect on the screen functionality (e.g. small elements like images used for screen decoration). In that case, labeling elements like that may be confusing for the user.

#### Additional notes

This guideline with provided techniques covers the 1.1.1 Non-text Content - Level A of the WCAG standard.

## Time-based Media

Provide alternatives for time-based media.

### Captions support for prerecorded media

Due some dissablities, some users may not be able to hear the content of the media which is provided by the application. Example of that can be prerecorded audio or video track. To make that content accessible to all users, in some cases, support for some accessibility features must be added.

#### Success techniques

##### Using AVPlayer with captions

One way of making the prerecorded media accessible is by adding captions. Most of the modern software supports adding captions to the video and `AVPlayer` from `AVFoundation` automatically supports it. User should enable accessibility feature called *Closed Captions* by going to *Settings > Accessibility > Subtitles & Captioning > Closed Captions + SDH*. When it is enabled, captions will be shown in the media which contains captions.

##### Custom solution with accessibility notifications

If other solution is used (instead of `AVPlayer`), status of the closed captioning can be checked via `UIAccessibility.isClosedCaptioningEnabled` or by subscribing to the notification `UIAccessibility.closedCaptioningStatusDidChange`.

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

To be able to provide the information for the users for both prerecorded audio and prerecorded video, one way of providing the information is by transcripts (text). If defined correctly, text on the screen can be read by VoiceOver for people with visibility issues, while people with hearing issues can read the transcript. This way, both scenarios are satisfied without a need to provide captions.

#### Additional notes

This guideline with provided techniques covers the 1.2.1 Audio-only and Video-only (Prerecorded) - Level A and 1.2.2 Captions (Prerecorded) - Level A of the WCAG standard.
