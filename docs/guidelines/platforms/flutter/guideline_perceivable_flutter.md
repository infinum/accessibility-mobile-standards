
 [🔼 Accessibility principles and examples](../../principles/accessibility_principles_and_examples.md  "Accessibility principles and examples") | [⬅️ Perceivable principle](../../principles/perceivable_principle.md "Perceivable principle")

# Operable guidelines for Flutter

User interface components and navigation must be operable.

## Text alternatives

Provide text alternatives for any non-text content to be changed into other forms people need, such as large print, braille, speech, symbols, or more straightforward language.

*This guideline covers point 1.1.1 Non-text Content - Level A of the WCAG standard.*

### Non-text content identification

:white_check_mark: **Success criteria**

Each UI element should include a description that describes it's purpose. It is important that all elements presented on the screen have the description provided, especially the ones that are important for the functionality of the screen on which they are presented. That way, screen readers such as TalkBack can announce these labels to users who rely on these services.

For this use wrap your widget with `Semantics` widget. Some widgets already wrap that and expose it as property. Here's the example of such image:

```dart
Image(image: AssetImage('assets/settings.png'), semanticLabel: 'Open settings')
```

:no_entry_sign: **Failure criteria**

![](/resources/images/settings_icon.png)

- Without the semantic label, this element above is unnamed to screen readers, and for persons relying on screen readers it's impossible to understand it's purpose.

- Do not provide semantics of elements that only exist for a decorative person. This will make navigation with screen readers harder.

---

## Time-based Media

Provide alternatives for time-based media.

*This guideline covers point 1.2 Time-Based Media - Level A of the WCAG standard.*

:white_check_mark: **Success criteria**

If the app you are building includes media content such as video clips or audio recordings, it is suggested to provide an alternative for users with different types of accessibility needs in order for them to understand the material. The suggested practice would be to:

- include controls that allow users to pause and stop media, change volume and toggle subtitles (captions)

- if a video presents information that is vital to completing workflow, provide the same content in an alternative format, such as transcript

:no_entry_sign: **Failure criteria**

- all media is presented to the user without the possibility to change some of the controls (slow down, pause, volume up etc.)

---

## Adaptable

### Info and Relationships

Information, structure, and relationships conveyed through presentation are available in text.

*This guideline covers point 1.3.1 Info and Relationships - Level A of the WCAG standard.*

:white_check_mark: **Success criteria**

- **Groups of related content**

In the image below the name and score are related and should be grouped together, usually by using `MergeSemantics` widget.

Otherwise screen reader could read just "2345" which means nothing by itself.

![](/resources/images/score_row.png)

- **Headings within text**

It is also possible to use _headings_ to summarize groups of text that appear on the screen. To mark a view to be treated as heading you can set `Semantics(header: true, ...)` 

That way users of accessibility services can choose to navigate between headings instead of navigating between paragraphs or between words which can improve text navigation experience.

:no_entry_sign: **Failure criteria**

- it is not clear which parts of the screen are contextually connected to each other

---

### Meaningful sequence

*This guideline covers point 1.3.2 Meaningful sequence - Level A of the WCAG standard.*

:white_check_mark: **Success criteria**

If the order of the content displayed on the screen is crucial for the understanding, it is very important to make sure it will be presented in the same order when using accessibility services. That way users of accessibility services (such as TalkBack) can get clearer picture of the content and possible actions on the current screen that is being navigated through.

Use `OrdinalSortKeys` to change the semantic order. In the example, VoiceOver will first announce the Remove Button, then the Add Button.


![](/resources/images/podium.png)

```dart
Row(
  children: [
    Semantics(
      sortKey: OrdinalSortKey(1),
      child: PodiumPlace('2nd place: John'),
    ),
    Semantics(
      sortKey: OrdinalSortKey(0),
      child: PodiumPlace('1st place: Mark'),
    ),
    Semantics(
      sortKey: OrdinalSortKey(2),
      child: PodiumPlace('3rd place: Tony'),
    ),
  ],
);
```

---

### Sensory characteristics

Instructions provided for understanding and operating content do not rely solely on sensory characteristics of components such as shape, color, size, visual location, orientation, or sound.

*This guideline covers point 1.3.3 Sensory characteristics - Level A of the WCAG standard.*
#### ✅ Success technique(s)

To make our app entirely understandable to the users, we should not rely only on one characteristic to show the user elements on the screen. You can find different ways to satisfy this aspect in the text below.

For example, the color. Use additional differentiation beside the color.

:no_entry_sign: **Failure criteria**

- important difference between elements is stressed only with colors

![](/resources/images/bill.png)

Here the person might not realize that discount is being reduced from the total price.

⎯

[← Perceivable principle](../../principles/perceivable_principle.md "Perceivable principle")

