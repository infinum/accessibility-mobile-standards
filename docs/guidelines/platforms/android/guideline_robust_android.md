[🔼 Accessibility principles and examples](../../principles/accessibility_principles_and_examples.md  "Accessibility principles and examples") | [⬅️ Robust principle](../../principles/robust_principle.md "Robust principle")

# Robust guidelines for Android

Content must be robust enough that it can be interpreted by a wide variety of mobile devices, including those which use accessibility
features.

## Compatible (WCAG 4.1)

Maximize compatibility with current and future devices, taking into account the accessibility features that they might be using.

### Name, Role, Value (WCAG 4.1.2 - Level A)

User interface elements should be clearly defined by their
name ([content description](https://developer.android.com/reference/android/view/View.html#attr_android:contentDescription) & [accessibility action](https://developer.android.com/reference/android/view/accessibility/AccessibilityNodeInfo.AccessibilityAction)),
the role that they have (
AccessibilityNodeInfoCompat's [class name](https://developer.android.com/reference/androidx/core/view/accessibility/AccessibilityNodeInfoCompat#setClassName(java.lang.CharSequence)) & [role description](https://developer.android.com/reference/androidx/core/view/accessibility/AccessibilityNodeInfoCompat#setRoleDescription(java.lang.CharSequence))),
and the value they carry(e.g. progress value, checked state, ...). The app should be able to notify the user if any of these parameters
change programmatically without user input (or the changes should be reflected in the element's accessibility attributes) so that the user
remains aware of what this element does at all times.

> This guideline covers point *4.1.2 Name, Role, Value - Level A of the WCAG standard.*

#### ✅ Success technique(s)

Every user interface element should have an accessibility label that can be used by TalkBack. For Views, it can be set through
`android:contentDescription` attribute in XML or by using `View.setContentDescription(contentDescription)` function.
For Compose, contentDescription can be set as a semantics property.

Accessibility action can be defined for Views via `AccessibilityDelegateCompat`'s `addAction` function.
In the example below, talkback service will notify the user that performing click option on FAB will open payment options.

Example: setting a click action with description to FAB:

```
 ViewCompat.setAccessibilityDelegate(
        binding.paymentOptionsFab,
        object : AccessibilityDelegateCompat() {
            override fun onInitializeAccessibilityNodeInfo(host: View, info: AccessibilityNodeInfoCompat) {
                super.onInitializeAccessibilityNodeInfo(host, info)
                val customClick = AccessibilityNodeInfoCompat.AccessibilityActionCompat(
                    AccessibilityNodeInfoCompat.ACTION_CLICK,
                    R.string.open_payment_options,
                )
                info.addAction(customClick)
            }
        },
    )
```

For Compose, accessibility actions can be defined more precisely by overriding labels for default actions. This can be done by setting the
appropriate SemanticsActions function.

Example: setting a click action with description to card:

```
<!-- Label text for en-US locale would be "Open settings" -->
 Card(
    modifier = Modifier
        .semantics {
            onClick(
             label = openSettingsLabel,
                action = {
                    openSettings() // action to be performed
                    true           // return true to indicate that the action was handled
                }
            )
        }
 ) {
  ...
 }
```

For users of switch control, actions like drag-and-drop can be challenging. To make this functionality more accessible, custom action can be
defined.

Example: setting a custom action for drag-and-drop to add favourites:

```
<!-- Label text for en-US locale would be "Add to favourites" -->
 Card(
    modifier = Modifier
        .semantics {
            customActions = listOf(
                // your custom action
                CustomAccessibilityAction(label = addToFavouritesLabel) {
                    // Add to favourite logic
                    true
                }
            )
        }
 ) {
  ...
 }
```

To help users understand the purpose of an element, roles should be added to the elements.
In View system, roles can be defined through `AccessibilityDelegateCompat` with `setRoleDescription`, however, using `setClassName` should
be preferred as it is multilingual by default.

Example: setting button role to a card view

```
 ViewCompat.setAccessibilityDelegate(
        loginCard,
        object : AccessibilityDelegateCompat() {
            override fun onInitializeAccessibilityNodeInfo(host: View, info: AccessibilityNodeInfoCompat) {
                super.onInitializeAccessibilityNodeInfo(host, info)
                info.roleDescription = "Button"
                info.className = Button::class.java.name
            }
        },
    )
```

In Compose, roles can be defined through `role` semantics property. List of available roles can be
found [here](https://developer.android.com/reference/kotlin/androidx/compose/ui/semantics/Role)

Example: Setting button role to a Box composable

```
 Box(
    modifier = Modifier
        .semantics {
            role = Role.Button
        }
 ) 
```

#### 🚫 Failures

Not providing accessibility identifiers for user interface elements.

Not providing names for all parts of multi-part field (e.g. phone number).

Implementing custom controls that are unfamiliar to the users and don't carry the necessary accessibility identifying information as defined
in this guideline.

Changing the value or role of a user interface element without adjusting its identifier programmatically.

### Status messages (WCAG 4.1.3 - Level AA)

The guideline states that status messages should be programmatically determinable by the user.
This means that the user should be able to know the status of the app at any given time without having to interact with it.

On mobile this means that the user should be able to know if the current state has been changed - which is especially important for users who rely on screen readers.

> This guideline covers point *4.1.3 Status messages - Level AA of the WCAG standard.*

#### ✅ Success technique(s)

When an important thing on the screen changes, users should be notified about it.
This can be achieved in View system by by setting `ViewCompat.setAccessibilityLiveRegion` which makes the accessibility service announce
changes to the view.
To interrupt ongoing speech and start the announcement, use `ACCESSIBILITY_LIVE_REGION_ASSERTIVE`. To wait for ongoing speech, use `ACCESSIBILITY_LIVE_REGION_POLITE`.

Example: Implement assertive announcements for shopping cart updates

In a shopping app, we can add assertive announcements of the number of items in the shopping cart after the user has added or removed an item, such as  "1 item added to your cart. Total: 3 items," which can keep users updated on their cart status.

```
ViewCompat.setAccessibilityLiveRegion(shoppingCartView, ViewCompat.ACCESSIBILITY_LIVE_REGION_ASSERTIVE)
```

In Compose, the same can be achieved by setting the `liveRegion` semantics property.

Example: Implement assertive announcements for remaining cooking time

In a cooking app, we can provide real-time updates by announcing, "Your meal will be ready in 5 minutes.", allowing users to stay informed without checking their phones.

```
CookingCountdownTimer(
    modifier = Modifier.semantics {
        liveRegion = LiveRegionMode.Assertive
    }
)
```

#### 🚫 Failures

Not providing a way for the user to know the current status of the application at any given time.

Using assertive live region mode for content which is not important and time-sensitive. 

---

#### Sources

- [Google Support Page](https://support.google.com/accessibility/android)
- [Official Documentation](https://developer.android.com/guide/topics/ui/accessibility)

---

[← Robust principle](../../principles/robust_principle.md "Robust principle")
