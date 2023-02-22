# Android accessibility features overview

It is very important that the app you are developing is accessible to all users. Accessibility should be considered during the whole development process. If properly implemented, accessibility features and services can significantly improve your app's usability, especially for users with disabilities, but also in general.

In this chapter, we'll introduce some of the most frequently used Android accessibility features. The whole list of all available accessibility features and services alongside with a quick guide on how to use them could be found on the official [Android Accessibility Help page](https://support.google.com/accessibility/android#topic=6007234).

Also, an important thing to stress is that only a limited set of accessibility services could be supported from the implementation perspective. Other sets will work out of the box. In other words, you can not add some custom implementation in order to make your app behave in a different way when that specific feature is on.

The services you could support through the app implementation will be marked with :green_circle:.

## Vision support features

### Screen readers

:green_circle: **Talkback**

The TalkBack is a Google screen reader available on Android devices that allows you to control your app eyes-free.

**>> How it works <<**

You can explore your app using touches and swipes when you [turn on TalkBack on your Android device](https://support.google.com/accessibility/android/answer/6007100).

TalkBack is controlled entirely by only one finger. Gestures with two or more fingers will not be handled by TalkBack. They'll be sent directly to the underlying view meaning you still can swipe using two fingers or pinch-to-zoom.

You could navigate through the app using TalkBack by swiping right or left. You're navigating forward in a text by swiping from left to right, moving right and down accordingly. Alternatively, you could navigate backward by swiping from right to left, meaning you will be moving to the left and eventually up.

TalkBack provides audible information about the currently focused view whenever you click on it or change focus to it. Also, you can explore the screen more rapidly by using touch-and-drag.

You can interact with a focused item, mostly with a double tap. Double-tapping the currently focused item will perform a click. On the other hand, to perform a long click, you can double-tap and hold the currently focused item.

Detailed description of all TalkBack configuration could be found on the official [Android Accessibility Help - TalkBack page](https://support.google.com/accessibility/android/answer/6006598?hl=en&ref_topic=10601571).

### Text and display settings

:green_circle: **Font size**

The user has the ability to change the font size of the text that will be displayed on their Android device. The regular scale of font is 1.0. The maximum scale that Android devices support is 2.0, and the minimum is 0.8.

Applications must support font changes and their design to remain consistent after the changes are applied in order to help users with vision impairments.

**Display size**

The user has the ability to make items on the screen smaller or larger in order to improve their visibility.

**Bold fonts**

The user has the ability to change the weight of the text, too. The weight of the text is defined on a scale from 100 to 1000. The default or regular weight is set to 400.

**Color correction**

Color correction is an Android 12 feature available for individual users with color vision deficiency, also called color blindness. People who face this type of visual challenge are unable to distinguish a certain color or shades of a color. The rarest, but still a possible scenario, is when the person is completely color blind.

An average color-blind individual is able to distinguish around 20 color hues, while people with normal vision can distinguish up to 100 colors effortlessly.

Color blindness is commonly divided into three types:

1. Red-green color blindness – a condition where an individual is unable to tell the difference between red and green. This is also the most common type of color blindness.

2. Blue-yellow color blindness – a condition where an individual finds it hard to differentiate between yellow and red, and likewise, blue and green.

3. Total color blindness – a condition where an individual does not see colors at all. This is also a very rare type of color deficiency.

Depending on the deficiency type, the user can choose an appropriate color correction option in phone settings. After choosing an appropriate option, the color correction feature changes how colors are displayed in order to help users distinguish more easily between the differences.

:green_circle: **Color inversion and dark theme**

Some users find it easier to read light text on a dark background in the long run or in some special conditions (for example, when it is really bright outside).

On Android version 10 and up, there is an option to turn on the Dark theme on your device. Enabling a dark theme on your device will automatically convert the existing system colors to their dark alternatives. This option does not apply to pictures and videos. **Also, applications that do not support dark theme will not be converted.**

That is why there is another option with a similar effect called color inversion. However, in this case, the inversion of colors will be applied to everything on your device, including media.

**High contrast text**

High contrast has a similar effect on text as a dark theme to the whole device UI. This feature changes the text color to either black or white, depending on the original text color.

### Magnification

This feature allows you to zoom in on the content displayed on your screen temporarily or in a more permanent way, based on the option the user has chosen in the Settings of the phone.

**>> How it works <<**

If the chosen option is to zoom in temporarily, the user will be able to touch and hold to zoom in on a specific part of the screen. Once the user releases the press, the content will be zoomed out to the initial state.

If the chosen option is to zoom in more permanently, the user will be able to touch anywhere on the screen to zoom in. Also, the user will be able to move around a screen with two fingers or pinch with two fingers to adjust zoom.

## Mobility support features

### Interaction controls

:green_circle: **Switch access**

The Switch Access application lets you interact with your Android device using one or more switches or a keyboard instead of a touchscreen. Switch Access is primarily designed to help users with limited dexterity.

**>> How it works <<**

The application works in a way that allows item scanning on the screen, highlighting each item in turn until you make a selection.

In order to use Switch Access, you will need one or more switches.

There are three different types of switches:

1. External switch – This device sends a keystroke signal to your Android device. These devices connect to your Android device via Bluetooth or USB.

2. External keyboard – You could convert a standard USB or Bluetooth keyboard and use it as a switch device by assigning one or more of its keys to actions.

3. Buttons on your device – You could also use built-in buttons on your Android device, such as the volume up and down buttons, and set up that they trigger actions. This option is mainly intended for developers.

A detailed description of all Switch Access configurations can be found on the official [Android Accessibility Help - Switch Access page](https://support.google.com/accessibility/android/answer/6122836?hl=en&ref_topic=6151780).




