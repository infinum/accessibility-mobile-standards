# Understandable guidelines for Android 

## Readable

### Language of page

## Predictable 

_Make mobile apps appear and operate in predictable ways._

### On Focus & On Input

The user should be able to navigate through the app without constant context switching. Also, interacting with the view should not case change of context. If view interaction changes the context that should be signalized to the user **before** the interaction. 

If the content that is displayed on the screen is designed and implemented following [Perceivable guidelines] these requirements should be met by default.

:white_check_mark: **Success criteria**

- the content is grouped and labeled following [Perceivable guidelines]

:no_entry_sign: **Failure criteria**

- the content is not grouped based on context relationships and has no meaningful labels defined

## Input assistance

_Help users avoid and correct mistakes._

### Error identification

### Labels or instruction

When the accessibility services user focuses some sort of input view (for example in the form or login screen or something else) it is important to give him enough information about the type of input that is expected from him to provide.

- Pairs od elements where one describes the other

It is common case that given EditText has corresponding View that describes the content that the user should enter within the EditText element. This relationship between elements could be achieved by setting `android:labelFor` attribute on that specific View.

That way, services such as TalkBack will read defined relationship to the user to give him a bit more context when EditText is in focus.

An example of labeling such element pair is given in the following snippet:

```
<!-- Label text for en-US locale would be "Username:" -->
<TextView
   android:id="@+id/usernameLabel" ...
   android:text="@string/username"
   android:labelFor="@+id/usernameEntry" />

<EditText
   android:id="@+id/usernameEntry" ... />
```

In the given example, services such as TalkBack will read - "EditBox for username" when user sets focus to EditText.

:white_check_mark: **Success criteria**

-- input views are paired with other description in a way that they provide meaningful information about required input type

:no_entry_sign: **Failure criteria**

-- input views have no additional descriptions provided about required input type 







