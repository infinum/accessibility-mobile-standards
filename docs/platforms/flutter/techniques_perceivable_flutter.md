[⬅️ Principles](../../accessibility_principles.md)

 # [1. Perceivable principle](../../principles/perceivable_principle.md#1-perceivable-principle)

 ## [1.1 Text alternatives](../../principles/perceivable_principle.md#11-text-alternatives)

### [1.1.1 Non-text content (Level A)](../../principles/perceivable_principle.md#111-non-text-content-level-a)

#### ✅ Success technique(s)

Each UI element should include a description that describes it's purpose. It is important that all elements presented on the screen have the description provided, especially the ones that are important for the functionality of the screen on which they are presented. That way, screen readers such as TalkBack can announce these labels to users who rely on these services.

For this use wrap your widget with `Semantics` widget. Some widgets already wrap that and expose it as property. Here's the example of such image:

```dart
Image(image: AssetImage('assets/settings.png'), semanticLabel: 'Open settings')
```

#### 🚫 Failures

![](/resources/images/settings_icon.png)

- Without the semantic label, this element above is unnamed to screen readers, and for persons relying on screen readers it's impossible to understand it's purpose.

- Do not provide semantics of elements that only exist for a decorative person. This will make navigation with screen readers harder.

## [1.2 Time-based Media](../../principles/perceivable_principle.md#12-time-based-media)

### [1.2.1-1.2.2 Captions support for prerecorded media (Level A)](../../principles/perceivable_principle.md#121-122-captions-support-for-prerecorded-media-level-a)

#### ✅ Success technique(s)

If the app you are building includes media content such as video clips or audio recordings, it is suggested to provide an alternative for users with different types of accessibility needs in order for them to understand the material. The suggested practice would be to:

- include controls that allow users to pause and stop media, change volume and toggle subtitles (captions)

- if a video presents information that is vital to completing workflow, provide the same content in an alternative format, such as transcript

#### 🚫 Failures

- all media is presented to the user without the possibility to change some of the controls (slow down, pause, volume up etc.)

## [1.3 Adaptable](../../principles/perceivable_principle.md#13-adaptable)

### [1.3.1 Element information and relationship (Level A)](../../principles/perceivable_principle.md#131-element-information-and-relationship-level-a)

#### ✅ Success technique(s)

- **Groups of related content**

In the image below the name and score are related and should be grouped together, usually by using `MergeSemantics` widget.

Otherwise screen reader could read just "2345" which means nothing by itself.

![](/resources/images/score_row.png)

- **Headings within text**

It is also possible to use _headings_ to summarize groups of text that appear on the screen. To mark a view to be treated as heading you can set `Semantics(header: true, ...)` 

That way users of accessibility services can choose to navigate between headings instead of navigating between paragraphs or between words which can improve text navigation experience.

##### 🚫 Failures

- it is not clear which parts of the screen are contextually connected to each other

### [1.3.2 Meaningful sequence (Level A)](../../principles/perceivable_principle.md#132-meaningful-sequence-level-a)

#### ✅ Success technique(s)

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

### [1.3.3 Sensory characteristics (Level A)](../../principles/perceivable_principle.md#133-sensory-characteristics-level-a)

#### ✅ Success technique(s)

To make our app entirely understandable to the users, we should not rely only on one characteristic to show the user elements on the screen. You can find different ways to satisfy this aspect in the text below.

For example, the color. Use additional differentiation beside the color.

:no_entry_sign: **Failure criteria**

- important difference between elements is stressed only with colors

![](/resources/images/bill.png)

Here the person might not realize that discount is being reduced from the total price.

