# Accessibility guidelines

As mentioned before, mobile devices and mobile platforms support many accessibility features. Still, with those features, it is unclear what to do and how to implement accessibility features to cover different cases when using mobile applications.

To define and make clearer accessibility scenarios, [W3C](https://www.w3.org/) created a standard called Web Content Accessibility Guidelines or shorter [WCAG](https://www.w3.org/TR/WCAG21/).

As the name says, this standard was created for the web (initially developed in the 90s and ‘00s). At that time, mobile devices were not primarily used as they are today. Because of that, WCAG had some updates and changes over the years, but the most important thing this standard has defined are principles for covering cases for application accessibility.

There are four main principles:

* [Perceivable](principles/perceivable_principle.md)
* [Operable](principles/operable_principle.md)
* [Understandable](principles/understandable_principle.md)
* [Robust](principles/robust_principle.md)

## 1. Perceivable

This principle covers the application content and how users can access every part of the application.

## 2. Operable

The [operable chapter in the WCAG standard](https://www.w3.org/WAI/WCAG21/quickref/?currentsidebar=%23col_overview&levels=aa%2Caaa&technologies=smil%2Cpdf%2Cflash%2Csl#principle2) describes how disabilities might make it hard for some users to interact with the app. It contains information about how they alter the way users perform in-app actions and how to ensure users with nonstandard input devices can operate all parts of the app.

#### Keyboard Accessible

The app should be fully functional for users whose only input device is the keyboard. Operating via the keyboard should be concise and possible without requiring specific timing for individual keystrokes. Navigating into and out of different parts of the app should be possible without getting stuck. Document unconventional keyboard navigation methods. For keyboard shortcuts that only require pressing a single letter or number, the user should be able to turn the shortcut off or remap it.

#### Enough Time

Some users might have trouble grasping and interacting with the content that is available only for a limited time or is auto-updating. If possible, there should be a way to extend, pause or disable the timing.

#### Seizures and Physical Reactions

For some users, excessive flashing might cause seizures. As a general rule, avoid content that flashes more than three times in any one-second period.

#### Navigable

The app's navigation structure should be concise and easy to understand. Users should have an indication of where they are located and how their actions will affect their location. There should be a way to bypass content that is repeated on multiple screens. The focus order should be clear and predictable.

#### Input Modalities

Some users might have trouble moving the device themselves or performing complex gestures. Strive for the app to be operable using a variety of input methods. If possible, the user should have a way to undo the interaction and disable the input methods he might trigger accidentally.

## 3. Understandable

## 4. Robust


-- OLD

Another fundamental principle is **understandable**:

> Information and the operation of the user interface must be understandable.

This principle covers the aspect of distinctiveness, readability, and ease of use.

The last principle is **robust**, which is defined as:

> Content must be robust enough that it can be interpreted by a wide variety of user agents, including assistive technologies.

The main idea of this principle is to make your application compatible with assistive technologies.

Beyond just defining principles, WCAG defines **guidelines**, **success criteria**, and **techniques** on how to satisfy or implement guidelines for every principle.

Another important thing about WCAG is the definition of levels – A, AA, and AAA. The most basic one is A, while the AAA defines that all guidelines should be implemented.

In the following chapters, every principle with its guidelines will be described in more detail.

⎯

[← Intriduction](introduction.md)
|
[Checklist →](accessibility_checklist.md)
