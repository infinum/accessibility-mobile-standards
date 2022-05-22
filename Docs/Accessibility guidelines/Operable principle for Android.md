# Operable guidelines for Android 

_User interface components and navigation must be operable._

In this section we will describe guidelines and define examples of implementation that will help in making your application more operable. 

## Enough time



## Navigable 

// TO-DO add sections before 

### Traversal order 

Order of the components that are displayed on the screen should have logical traversal order. That is very important for people using accessibility services such as TalkBack to get clearer picture of the content and possible actions on the current screen they are navigating through.

The best solution would be to redesign the screen to create logical traversal order. But if that is not an option, setting `android:accessibilityTraversalBefore` or `android:accessibilityTraversalAfter` attributes could help create new order of the displayed views that will make a bit more sense to TalkBack users.

The example of using `android:accessibilityTraversalBefore` or `android:accessibilityTraversalAfter` attributes is given down below:

// TO - DO add screenshot of real app and set the attributes 

_Note 1. Always make sure to define `android:accessibilityTraversalBefore` or `android:accessibilityTraversalAfter` attributes ina a way that does not create any loops or traps that will prevent users to interact with all relevant views displayed on the screen._

//TO-DO check versioning
_Note 2. _ 

Example: 



### Link purpose 

All the links that are displayed in the application's components and screens should explain its unique purpose. This is important because based on the provided descriptions users would get a better idea if they want to follow provided link or not. 

If the context of the text is not self-explanatory and clear, users of accessibility services could try to find more information of the provided link in its surroundings. 

Some of the recommended techniques that could improve clarifying the context of the provided link are listed down below: 

- pair the link with descriptive text element that provide more context of the link itself - Screenshot 1.

- set accessibility description (content description) for the link item that will provide more information about it - Screenshot 2.

- define self-explanatory link text labels - Screenshot 3. 


Situations that should be avoided when working with links:

- defining links as part of the longer text where not all the content is related to the link - Screenshot 1. 

If the link is defined in a way that it is only a small part of longer text then it is impossible to distinguish it from the rest of the text. If no `contentDescription` is provided accessibility service would read it as regular text. On the other hand, if we set `contentDescription`, even if it is only for the, for example ClickableSpan that is used for opening provided link, then only provided `contentDescription` will be read and all the other part of the text will be ignored.  

**Solution proposals:**

- define text containing link as separate section - Screenshot 2.

If you define text containing link as separate section then you will be able to set `contentDescription` that will provide more information about the link and where it should navigate. That way, both users that use accessibility services and the ones that don't will have enough information to decide if they want to open the link or not.

| <img src="https://imgur.com/xKXqPgj.png" width="50%"> | <img src="https://imgur.com/nu99Q3S.png" width="50%"> |
|:--:|:--:|
| **Screenshot 1.** Text containing link is part of a longer text | **Screenshot 2.** Text containing link is separated from rest of the text |

:white_check_mark: **Success criteria**

- it is clear which part of the UI is link

- defined description of the link view or link itself is providing enough information about its purpose

:no_entry_sign: **Failure criteria**

- link is only visually distinguished from other labels and has no additional description provided

- link is part of the longer text and no additional description of its purpose is provided









