# [Robust principle](../../principles/robust_principle.md#robust-principle)

## [Compatible (WCAG 4.1)](../../principles/robust_principle.md#compatible-wcag-41)

### [Name, Role, Value (WCAG 4.1.2 - Level A)](../../principles/robust_principle.md#name-role-value-wcag-412---level-a)

#### ✅ Success technique(s)

Every user interface element should have an accessibility label that can be used by TalkBack. For Views, it can be set through
`android:contentDescription` attribute in XML or by using `View.setContentDescription(contentDescription)` function.
For Compose, contentDescription can be set as a semantics property.

When describing editable elements such as `EditText` or `TextField`, it is usually helpful to provide a text that gives examples of valid input in the element itself. That way, users who navigate through the app using screen readers could get more info about the required input when they focus on the editable element.
In these situations, it is recommended to use `android:hint` attribute for Views.

Example: setting a hint for `EditText` view

```
<!-- The hint text for en-US locale would be "Password". -->
<EditText
   android:id="@+id/passwordInputField"
   android:hint="@string/password_hint_text" ... />
  ```

For editable Compose components such as `TextField`, an example can be given by passing a `Text` composable through the `placeholder` parameter.

Example: setting a placeholder for `TextField` composable

```
<!-- The hint text for en-US locale would be "Password". -->
TextField(
    value = password,
    onValueChange = { },
    placeholder = {
        Text(text = stringResource(R.string.password_hint_text))
    }
)
```

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

### [Status messages (WCAG 4.1.3 - Level AA)](../../principles/robust_principle.md#status-messages-wcag-413---level-aa)

#### ✅ Success technique(s)

When an important thing on the screen changes, users should be notified about it.
This can be achieved in View system by setting `ViewCompat.setAccessibilityLiveRegion` which makes the accessibility service announce
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
