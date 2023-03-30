 [🔼 Accessibility principles and examples](../../principles/accessibility_principles_and_examples.md  "Accessibility principles and examples") | [⬅️  Robust principle](../../principles/robust_principle.md "Robust principle")

# Robust guidelines for Android

Content must be robust enough that it can be interpreted by a wide variety of mobile devices, including those which use accessibility features.

## Compatible

Maximize compatibility with current and future devices, taking into account the accessibility features that they might be using.

### Parsing

:white_check_mark: **Success criteria**

All user-visible content should be grouped logically and with appropriately assigned identifiers.

#### Label elements

In most cases you can include a required description in the layout resource file as the element's `contentDescription`. It is recommended to use string resources for defining all required descriptions for easier localization.

Also, the app should be able to notify the user if the value of a presented view changes programmatically without any user input.

**Code example:**

```
<!-- The en-US value for the following string is "Inspect". -->
<ImageView
    ...
    android:contentDescription="@string/inspect" />
```

_Note:_ You should not provide descriptions for TextView elements because Android accessibility services automatically announce the text itself as the required description.

- Editable elements

When describing editable elements such as EditText objects, it is usually helpful to provide a text that gives examples of valid input in the element itself. That way, users who navigate through the app using screen readers could get more info about the required input when they focus on the editable element.

In these situations, it is recommended to use `android:hint` attribute.

**Code example:**

```
<!-- The hint text for en-US locale would be
     "Password". -->
<EditText
   android:id="@+id/passwordInputField"
   android:hint="@string/password_hint_text" ... />
```


- Elements in the collection

When working with collections, it is very important that provided labels are **unique for each item**. That way, the system accessibility services can refer to exactly one specific item when announcing the label.

This will help users to get a general idea when they've cycled through the complete UI of your app.

In particular, you should provide additional text or contextual information in elements within reused layouts, such as RecyclerView objects, so each child element is uniquely identified.

The described requests could be achieved by setting content descriptions as a part of adapter implementation.

**Code example:**

An example of defining content description in adapter is given in the following snippet:

```
class ShowsAdapter(private val shows: List<Show>):
        RecyclerView.Adapter<ShowsAdapter.ShowViewHolder>() {

    class ShowViewHolder(val showView: ShowView) :
            RecyclerView.ViewHolder(showView)

    override fun onBindViewHolder(holder: ShowViewHolder, position: Int) {
        val show = shows[position]
        holder.showView.contentDescription = "Show ${position}: ${show.title}"
    }
}
```

:no_entry_sign: **Failure criteria**

- There are relevant UI views with no description provided.

- Descriptions provided for the relevant views are not unique and are repeated shortly one after another.

- Descriptions provided for the relevant views are too long and too complex.

- Descriptions provided for the relevant views are hardcoded and are not localized properly.

#### Additional notes

This guideline covers point 4.1.1 Parsing – Level A of the WCAG standard.

---

#### Sources

- [Google Support Page](https://support.google.com/accessibility/android)
- [Official Documentation](https://developer.android.com/guide/topics/ui/accessibility)

---

[← Robust principle](../../principles/robust_principle.md "Robust principle")
