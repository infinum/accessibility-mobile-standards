# Android accessibility features overview

It is very important that the app you are developing is accessible to all users. Accessibility should be considered during whole development process. If properly implemented, accessibility features and services can significantly improve your app's usability especially for users with disabilities, but also in general. 

In this chapter we are going to introduce some of the most frequently used Android accessibility features. The whole list off all available accessibility features and services alongside with quick guide on how to use them could be found on official [Android Accessibility Help page](https://support.google.com/accessibility/android#topic=6007234).

Also, important thing to stress out is that only limited set of accessibility services could be supported from the implementation perspective. Others will work out of the box. Meaning, you can not add some custom implementation in order to make your app behave in different way when that specific feature is on. 

The services you could supports through app implementation will be marked with :green_circle:.

## Vision support features

### Screen readers

:green_circle: **Talkback**

The TalkBack is the Google screen reader available on Android devices that allows you to control your app eyes-free.

**How it works**

When you [turn on TalkBack on your android device](https://support.google.com/accessibility/android/answer/6007100), you will be able to explore your app using touches and swipes.

TalkBack is controlled entirely by only one finger. Gestures with two or more fingers will not be handled by TalkBack. They'll be sent directly to underlying view meaning you still can swipe using two fingers or pinch-to-zoom.

You could navigate through the app using TalkBack by swiping right or left. You are navigating forward by swiping from left to right. Navigating forward is in sense of text. Meaning, you will be moving right and eventually down. Alternatively, you could navigate backwards by swiping from right to left meaning you will be moving to the left and eventually up.

TalkBack provides audible information about the currently focused view whenever you click on it or change focus to it. Also, you can more rapidly explore the screen by using touch-and-drag.

You can interact with focused item mostly with double tap. Double tapping currently focused item will perform click. On the other hand, if you double tap and hold currently focused item that will perform long click.

Detailed description of all TalkBack configuration could be found on official [Android Accessibility Help - TalkBack page](https://support.google.com/accessibility/android/answer/6006598?hl=en&ref_topic=10601571).

### Text and display settings

:green_circle: **Font size**

The user has the ability to change the font size of the text that will be displayed on his Android device. The regular scale of font is 1.0. Maximum scale that Android devices support is 2.0 and the minimum is 0.8.

It is important that applications support font changes and its design to remain consistent after the changes are applied in order to help users with vision impairments. 

**Display size**

The user has ability to change size of his display (screen zoom in/out) in order to improve visibility of items on the screen. 

**Bold fonts**

The user has the ability to change weight of text, too. The weight of text is defined on scale from 100 to 1000. The default or regular weight is set to 400. 

**Color correction**

Color correction is Android 12 feature available for individual users with color vision deficiency that is also referred as color blindness. People that face these type of visual challenge are unable to distinguish certain color or shades of color. The rarest, but still possible case is when the person is completely color blind. 

Average color blind individual is able to distinguish around 20 color hues while people with normal vision can distinguish up to 100 different colors effortlessly. 

Color blindness is commonly divided into three types: 

1. Red-Green color blindness - a condition where an individual is unable to tell the difference between red and green and also the most common type of color blindness

2. Blue-Yellow color blindness - a condition where an individual finds it hard to differentiate between yellow and red, and likewise, blue and green

3. Total color blindness - a condition where an individual does not see color at all and also very rare type of color deficiency

User can, depending on the type of deficiency, choose appropriate option for color correction in phone settings. After choosing appropriate option color correction feature changes how colors are displayed in order to help users to more easily distinguish differences. 

:green_circle: **Color inversion and dark theme**

Some users find it easier to read light text on a dark background either in the long run or in some special conditions (example: when it is really bright outside). 

On Android version 10 and up there is an option to turn on Dark theme on your device. Enabling dark theme on your device will automatically convert existing system colors to their dark alternatives. This option does not apply to pictures to videos. Also, applications that do not support dark theme will also not be converted.

That is why there is another option with similar effect called color inversion. But in this case inversion of colors will be applied to everything on your device, including media.

**High contrast text**

High contrast has similar effect to text as dark theme to whole device UI. This feature changes the text color to either black or white, depending on the original text color. 

### Magnification

**How it works**



## Mobility support features

### Interaction controls

:green_circle: **Switch access**

The Switch Access application lets you interact with your Android device using one or more switches or a keyboard instead of the touchscreen. Switch Access is primarily designed to help users with limited dexterity.

**How it works**

The application works in a way that is scans the items on the screen, highlighting each item in a turn, until you make a selection.

In order to use Switch Access, you will need one or more switches.

There are three different types of switches:

1. external switch - This is a device that sends keystroke signal to your Android device. These devices connect to your Android device via Bluetooth or USB.

2. external keyboard - You could convert a standard USB or Bluetooth keyboard and use it as switch device by assigning one or more of its keys to actions

3. buttons on your device - You could also use built-in buttons on Android device, such as the volume up and down buttons, and set up that they trigger actions. This option is mainly intended for developers.

Detailed description of all Switch Access configuration could be found on official [Android Accessibility Help - Switch Access page](https://support.google.com/accessibility/android/answer/6122836?hl=en&ref_topic=6151780).




