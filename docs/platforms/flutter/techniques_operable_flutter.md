# [Operable principle](../../principles/operable_principle.md#operable-principle)

## [Keyboard Accessible (WCAG 2.1)](../../principles/operable_principle.md#keyboard-accessible-wcag-21)

## [Keyboard (WCAG 2.1.1 - Level A)](../../principles/operable_principle.md#keyboard-wcag-211---level-a)

#### ✅ Success technique(s)

##### Handle tab navigation

When the user is navigating through the app using the `Tab` key on the keyboard, the system passes focus based on the the order of elements appearing on the screen. This is why, if the order of the view elements on the screen is not entirely the same as the order defined in the file, you might need to manually specify the focus order.

If you want to manually change focus order, you can specify different Focus traversal policy. E.g. by using `OrderedTraversalPolicy` together with `FocusTraversalOrder` widgets.

```dart
FocusTraversalGroup(
      policy: OrderedTraversalPolicy(),
      child: Row(
        children: <Widget>[
          FocusTraversalOrder(
            order: NumericFocusOrder(2.0),
            child: TextButton(
              child: const Text('ONE'),
              onPressed: () {},
            ),
          ),
          FocusTraversalOrder(
            order: NumericFocusOrder(1.0),
            child: TextButton(
              child: const Text('TWO'),
              onPressed: () {},
            ),
          ),
          FocusTraversalOrder(
            order: NumericFocusOrder(3.0),
            child: TextButton(
              child: const Text('THREE'),
              onPressed: () {},
            ),
          ),
        ],
      ),
    )
```

More about focus traversal you can at [Controlling what gets focus](https://docs.flutter.dev/development/ui/advanced/focus#controlling-what-gets-focus) from Flutter documentation.

## [Enough Time (WCAG 2.2)](../../principles/operable_principle.md#enough-time-wcag-22)

### [Timing Adjustable (WCAG 2.2.1 - Level A)](../../principles/operable_principle.md#timing-adjustable-wcag-221---level-a)

#### ✅ Success technique(s)

All users should have the ability to interact with the content displayed on the screen even if there is a time limit defined for interaction with a specific view. Therefore, users should have the ability to turn off the defined time-limit, adjust it or extend it.

- In case of session inactivity, it is recommended to notify the user that they are about to be signed off with the ability to extend that time limit. The notification could be displayed in form of an AlertDialog or something similar. TalkBack service tells you about alerts and notifications so users using accessibility services would also be aware of the defined limit.

- In case of auto-updating content, it is recommended to allow the user to extend the defined time limit to at least ten times the length of the default setting so that they're able to process the displayed information.

#### 🚫 Failures

- logging out the user without prior warning and possibility to extend session

- define time-limited actions in the app with no ability to extend that limit

### [Pause, Stop, Hide (WCAG 2.2.2 - Level A)](../../principles/operable_principle.md#pause-stop-hide-wcag-222---level-a)

#### ✅ Success technique(s)

- When using auto-scrolling page views or carousels whose animation starts automatically, make sure to provide a way for user to pause, stop, or hide it.

- Loading screens doesn't require to meet this success criterion.

#### 🚫 Failures

- Using an auto-updating or auto-scrolling view that can't be paused/stopped.

## [Seizures and Physical Reactions (WCAG 2.3)](../../principles/operable_principle.md#seizures-and-physical-reactions-wcag-23)

### [Three Flashed or Below Threshold (WCAG 2.3.1 - Level A)](../../principles/operable_principle.md#three-flashed-or-below-threshold-wcag-231---level-a)

#### ✅ Success technique(s)

- Avoiding flashing content in general, if possible.

- If using flashing content - keep the flash of an element running for a minimum of 333ms ([more than three per second](https://www.w3.org/WAI/WCAG21/Understanding/three-flashes-or-below-threshold.html)).

- If the usage of an element that flashes more frequently is unavoidable - make sure that the flashing area is covering less than 25% within 10 degrees of a visual field.

#### 🚫 Failures

- Using rapidly flashing elements to catch user's attention

- Having a larger area of screen flashing more than three times per second

## [2.4 Navigable (WCAG 2.4)](../../principles/operable_principle.md#navigable-wcag-24)

### [Bypass Blocks (WCAG 2.4.1 - Level A)](../../principles/operable_principle.md#bypass-blocks-wcag-241---level-a)

#### ✅ Success technique(s)

- An element containing many elements should be created as semantics container. This way when navigatiing using with screen readers, the user will be able to choose if he wants to skip that block (bypass block) or go into that block.

Here's example image where user can choose if he want's to check stories or bypass that block altogether:

![](/resources/images/stories.png)

To accomplish this use `Semantics(container: true, label: 'Stories', child: ...)` widget and.

#### 🚫 Failures

Not providing a way for user to quickly skip over sections with numerous items.

### [Page Titled (WCAG 2.4.2 - Level A)](../../principles/operable_principle.md#page-titled-wcag-242--level-a)

#### ✅ Success technique(s)

Each screen should have a clear, descriptive and, if possible, unique title that describes the purpose of that screen that will be understandable to all users. Also, it is important to make sure that the title is the first element that will be read by screen reader when the user enters the screen. 

If you're setting AppBar in `Scaffold(appBar: ...)` then the title will be read before body. But if you have some custom design you can use `Semantics(sortKey: OrdinalSortKey(0), child: ...)` to make sure title is read first.

#### 🚫 Failures

- Leaving the title empty
- Using a custom title view or custom navigation bar without ensuring it's readable by screen reader

### [Link Purpose (WCAG 2.4.4 - Level A)](../../principles/operable_principle.md#link-purpose-wcag-244---level-a)

#### ✅ Success technique(s)

Links are also special elements for screen readers and user expects they will be read in an appropriate way. Note that we are not talking here about buttons, but about text links that are mostly found on the web.

Flutter doesn't have out-of-box support for hyperlinks, but it can be achieved with use of `RichText` and `TextSpans`, or using few of packages made for this.

Important piece here is that you should wrap the link with `Semantics(link: true, child...)`.

#### 🚫 Failures

- link is defined as unclear label or button and has no additional description provided

- link is part of the longer text and implemented using ClickableSpan so TalkBack users are not aware of link existence
