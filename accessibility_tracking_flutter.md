# Accessibility tracking Flutter

The [AccessibilityFeatures](https://api.flutter.dev/flutter/dart-ui/AccessibilityFeatures-class.html) class contains info about the accessibility setting on the underlying platform. Even though [textScaleFactor](https://api.flutter.dev/flutter/widgets/MediaQueryData/textScaleFactor.html) could be considered an accessibility setting, it is not a part of the `AccessibilityFeatures`.

The `AccessibilityFeatures` and `textScaleFactor` can be obtainded form `WidgetsBinding`.

```dart
class AccessibilityTrackingService with WidgetsBindingObserver {
  void init() {
    _track();
    // Start listening to changes
    WidgetsBinding.instance!.addObserver(this);
  }

  void dispose() {
    // Stop listening to changes
    WidgetsBinding.instance!.removeObserver(this);
  }

  @override
  void didChangeAccessibilityFeatures() {
    // Called when AccessibilityFeatures changes
    _track();
  }

  @override
  void didChangeTextScaleFactor() {
    // Called when textScaleFactor changes
    _track();
  }

  void _track() {
    final accessibilityFeatures = WidgetsBinding.instance!.accessibilityFeatures;
    final textScaleFactor = WidgetsBinding.instance!.platformDispatcher.textScaleFactor;
    // Send accessibilityFeatures and textScaleFactor to the tracking service (e.g., Firebase Analytics)
  }
}

void main() {
  // Add this line, if using `WidgetsBinding.instance` before calling the `runApp`
  WidgetsFlutterBinding.ensureInitialized();

  final accessibilityTracking = AccessibilityTrackingService();
  accessibilityTracking.init();

  runApp(MyApp());
}
```
