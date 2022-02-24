# Accessibility features Flutter

## Determining accessibility

Flutter provides a way to view the accessibility features of the underlying platform. We can obtain [AccessibilityFeatures](https://api.flutter.dev/flutter/dart-ui/AccessibilityFeatures-class.html) class from the `window` top-level property and listen to its changes with `WidgetsBindingObserver`. 

```dart
final accessibilityFeatures = window.accessibilityFeatures;

accessibilityFeatures.accessibleNavigation;
accessibilityFeatures.boldText;
accessibilityFeatures.disableAnimations;
//...
```

Some accessibility features (`boldText`, `highContrast`...) are only supported on iOS.

There are some discrepancies between platforms:
* `accessibleNavigation`: on iOS checks whether VoiceOver or Switch Control are enabled. on Android it checks if the user enabled an accessibility app that provides `touchExploration`, meaning that with TalkBack, the property will be `true`, but `false` when using Switch Access.
* When reduce motion is enabled on iOS, `reduceMotion` in Flutter is `true` and `disableAnimation` is `false`. When animations are disabled on Android, `reduceMotion` is `false`, and `disableAnimations` is `true`.

Another accessibility setting, the [textScaleFactor](https://api.flutter.dev/flutter/widgets/MediaQueryData/textScaleFactor.html), is not provided in `AccessibilityFeatures`. We can instead, obtain it from the `MediaQuery`.

```dart
MediaQuery.of(context).textScaleFactor;

// Some accessibility features can also be obtained from MediaQuery.
MediaQuery.of(context).accessibleNavigation;
```

## Accessibility in Flutter

Use the [Semantics](https://api.flutter.dev/flutter/widgets/Semantics-class.html) widget to describe a part of the widget tree. Accessibility tools rely on the provided properities to assist the user.

```dart
// Child described as a "Welcome header".
Semantics(
  label: 'Welcome',
  header: true
  button: false,
  image: false,
  child: // ...
)
```

Most of the built-in Flutter widgets automatically provide semantic information or have a property for describing it.

```dart
// ElevatedButton does not need to be wrapped with Semantics, as this is already done under the hood.
ElevatedButton(
  // ...
)

/// Some widgets have a shorthand for descibing semantics.
Image.asset(
  // ...
  semanticLabel: 'Profile image'
)
```

Under the hood, the semantic properties get stored in [SemanticsNodes](https://api.flutter.dev/flutter/semantics/SemanticsNode-class.html). The `Semantics` widget is a way to give the properties to the node. By default, the `Semantics` widget does not create a new node, so properties from different Semantics widgets might get merged.


Use `container` property to explicitly create a new node. VoiceOver will read the example as "Colors red, green".
```dart
Semantics(
  label: 'Colors',
  container: true,
  child: Row(children: [Text('red'), Text('green')]),
)
```

Use `explicitChildNodes` property to prevent automatic merging. VoiceOver will read the example as "Colors" then the user can move to the next node "red" and the next node "green".

```dart
Semantics(
  label: 'Colors',
  container: true,
  explicitChildNodes: true
  child: Row(children: [Text('red'), Text('green')]),
)
```

Use `MegeSemantics`, to explicitly group semantic information. To combine widgets that semantically represent the same thing. VoiceOver will read the example as "Dark mode, switch on". Without `MergeSemantics`, VoiceOver would read it as two separate things "Switch on"  and "DarkMode".

```dart
MergeSemantics(
  child: Row(
    children: [
      Switch(value: true, onChanged: (value) {}),
      Text('Dark mode'),
    ],
  ),
)
```

Use `ExcludeSemantics`, to mark the sub-tree as not having any semantic importance, such as when using images just for decoration. In the example, VoiceOver will not announce the image.

```dart
ExcludeSemantics(
  child: Image.asset('...'),
)
```

Use `BlockSemantics` to semantically hide widgets below it. In the example, VoiceOver will not annouce the Add Button, since it is overlayed by the Card.

```dart
Stack(
  children: [
    ElevatedButton(child: Text('Add'), onPressed: () {}),
    BlockSemantics(
      child: Card(child: Text('Overlay')),
    )
  ],
);
```

Use `OrdinalSortKeys` to change the semantic order. In the example, VoiceOver will first announce the Remove button, then the Add Button.

```dart
Column(
  children: [
    Semantics(
      sortKey: OrdinalSortKey(1),
      child: ElevatedButton(child: Text('Add'), onPressed: () {}),
    ),
    Semantics(
      sortKey: OrdinalSortKey(0),
      child: ElevatedButton(child: Text('Remove'), onPressed: () {}),
    )
  ],
);
```

Use semantic actions to provide a convenient way for people with disabilities to perform certain tasks.
In the example, the user can use a specially configured hardware button to perform the increase task. VoiceOver will also announce custom actions.

```dart
Semantics(
  onIncrease: () {
    // Perform increase task
  },
  customSemanticsActions: {
    CustomSemanticsAction(label: 'My task'): () {
      // Perform my task
    },
  },
  child: Container(),
);
```

## Testing accessibility

Flutter provides a way to test some of the accessibility guidelines.

```dart
testWidgets('Test contrast', (tester) async {
  await tester.pumpWidget(MyWidget());
  await expectLater(tester, meetsGuideline(textContrastGuideline));
});
```

We can use semantic properties to find widgets. With `matchesSemantics` we can ensure semantic properties meet our expectations.

```dart
testWidgets('Test semantics', (tester) async {
  await tester.pumpWidget(MyWidget());
  final finder = find.bySemanticsLabel('Add');
  final semantics = tester.getSemantics(finder);
  expect(semantics, matchesSemantics(isButton: true, hasEnabledState: true));
});
```