# Android accessibility features overview

Accessibility is very important part of any app and it should be considered during whole development process. If properly implemented, accessibility features and services can significantly improve your app's usability especially for users with disabilities, but also in general. In this chapter we are going to introduce available Android accessibility features.

## Vision support features

### TalkBack

**Overview**

The TalkBack is the Google screen reader available on Android devices that allows you to control your app eyes-free.

**How it works**

When you [turn on TalkBack on your android device](https://support.google.com/accessibility/android/answer/6007100), you will be able to explore your app using touches and swipes.

TalkBack is controlled entirely by only one finger. Gestures with two or more fingers will not be handled by TalkBack. They'll be sent directly to underlying view meaning you still can swipe using two fingers or pinch-to-zoom.

You could navigate through the app using TalkBack by swiping right or left. You are navigating forward by swiping from left to right. Navigating forward is in sense of text. Meaning, you will be moving right and eventually down. Alternatively, you could navigate backwards by swiping from right to left meaning you will be moving to the left and eventually up.

TalkBack provides audible information about the currently focused view whenever you click on it or change focus to it. Also, you can more rapidly explore the screen by using touch-and-drag.

You can interact with focused item mostly with double tap. Double tapping currently focused item will perform click. On the other hand, if you double tap and hold currently focused item that will perform long click.

Detailed description of all TalkBack configuration could be found on official [Android Accessibility Help - TalkBack page](https://support.google.com/accessibility/android/answer/6006598?hl=en&ref_topic=10601571).

### Display size and font size

**Overview**

**How it works**

### Magnification

**Overview**

**How it works**

### Contrast and color options

**Overview**

**How it works**

## Mobility support features

### Switch Access

**Overview**

The Switch Access application lets you interact with your Android device using one or more switches or a keyboard instead of the touchscreen. Switch Access is primarily designed to help users with limited dexterity.

**How it works**

The application works in a way that is scans the items on the screen, highlighting each item in a turn, until you make a selection.

In order to use Switch Access, you will need one or more switches.

There are three different types of switches:

- external switch - This is a device that sends keystroke signal to your Android device. These devices connect to your Android device via Bluetooth or USB.

- external keyboard - You could convert a standard USB or Bluetooth keyboard and use it as switch device by assigning one or more of its keys to actions

- buttons on your device - You could also use built-in buttons on Android device, such as the volume up and down buttons, and set up that they trigger actions. This option is mainly intended for developers.

Detailed description of all Switch Access configuration could be found on official [Android Accessibility Help - Switch Access page](https://support.google.com/accessibility/android/answer/6122836?hl=en&ref_topic=6151780).

### Voice Access

**Overview**



**How it works**

