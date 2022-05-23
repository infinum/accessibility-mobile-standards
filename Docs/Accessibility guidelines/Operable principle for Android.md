# Operable guidelines for Android 

_User interface components and navigation must be operable._

In this section we will describe guidelines and define examples of implementation that will help in making your application more operable. 

## Enough time

_Provide users enough time to read and use content._

All the users should have ability to interact with the content displayed on the screen even if there is time limit defined for interaction with that specific view. Therefore, users should have the ability to turn off defined time-limit, adjust it or extend it.

:white_check_mark: **Success criteria**

- In case of session inactivity it is recommended to notify the user that he is about to be signed off with ability to extend that time-limit. The notification could be displayed in form of Alert or something similar. TalkBack service tells you about alerts and notifications so users using accessibility services would also be aware of the defined limit. 

// TO-DO add example

- In case of auto-updating content it is recommended to allow user to extend the defined time-limit to at least ten times the length of the default setting for everyone to be able to process the displayed information. 


:no_entry_sign: **Failure criteria**

// TO-DO

## Navigable 

_Provide ways to help users navigate, find content, and determine where they are._

### Bypass Blocks

The app should be implemented in a way that it is possible to relatively easy skip the content that is repeated on the screen or  the content that is irrelevant to the user.

This is feature is based on well on a good implementation of grouping the views that are displayed in the app. // TO-DO add link to section Adaptable in Perceivable guidelines

- Headings within text

It is also possible to use _headings_ to summarize groups of text that appear on the screen. To mark some view to be treated as heading you can set `android:accessibilityHeading` to true.

That way users of accessibility services can choose to navigate between headings instead of between paragraphs or between words which can improve text navigation experience.

// ADD SNIPPETS OF IMPLEMENTATION and example

:white_check_mark: **Success criteria**

// TO-DO

:no_entry_sign: **Failure criteria**

// TO-DO

### Page Titles

Each screen should have clear, descriptive, if possible unique title that describes purpose of that screen that will be understandable to all users.

:white_check_mark: **Success criteria**

// TO-DO

:no_entry_sign: **Failure criteria**

// TO-DO

### Traversal Order 

Order of the components that are displayed on the screen should have logical traversal order. That is very important for people using accessibility services such as TalkBack to get clearer picture of the content and possible actions on the current screen they are navigating through.

The best solution would be to redesign the screen to create logical traversal order. But if that is not an option, setting `android:accessibilityTraversalBefore` or `android:accessibilityTraversalAfter` attributes could help create new order of the displayed views that will make a bit more sense to TalkBack users.

The example of using `android:accessibilityTraversalBefore` or `android:accessibilityTraversalAfter` attributes is given down below:

// TO - DO add screenshot of real app and set the attributes 

_Note 1. Always make sure to define `android:accessibilityTraversalBefore` or `android:accessibilityTraversalAfter` attributes ina a way that does not create any loops or traps that will prevent users to interact with all relevant views displayed on the screen._

//TO-DO check versioning
_Note 2. _ 

Example: 



### Link Purpose 

All the links that are displayed in the application's components and screens should explain its unique purpose. This is important because based on the provided descriptions users would get a better idea if they want to follow provided link or not. 

If the context of the text is not self-explanatory and clear, users of accessibility services could try to find more information of the provided link in its surroundings. 

Some of the recommended techniques that could improve clarifying the context of the provided link are listed down below: 

- Pair the link with descriptive text element that provide more context of the link itself. - **Screenshot 1.**

- Set accessibility description (content description) for the link item that will provide more information about it. - **Screenshot 2.**

- Define self-explanatory link text labels. - **Screenshot 3.**

- If link is defined as part of the longer text **avoid using clickable spans** instead **use URLSpan** for adding link to specific part of text. That way accessibility service such as TalkBack will recognized there is link set somewhere in the text and user will know that he is able to perform action if he is interested in following link. - **Screenshot 4.**  

|:--:|:--:|
| <img src="https://imgur.com/b833Hol.png" width="50%"> | <img src="https://imgur.com/6mI8z8W.png" width="50%"> |
| **Screenshot 1.** Text containing link is part of a longer text | **Screenshot 2.** If link item is implemented as regular TextView or Button, additional contentDescription should be provided that will stress that user is leaving the app |
| <img src="https://imgur.com/6mI8z8W.png" width="50%"> | <img src="https://imgur.com/b833Hol.png" width="50%"> |
| **Screenshot 3.** If the label is implemented using URLSpan no additional contentDescription should be provided | **Screenshot 4.** Link as part of longer text should be implemented using URLSpan |

:white_check_mark: **Success criteria**

- it is clear which part of the UI is link

- defined description of the link view or link itself is providing enough information about its purpose

:no_entry_sign: **Failure criteria**

- link is only visually distinguished from other labels and has no additional description provided

- link is part of the longer text and no additional description of its purpose is provided

// TO DO check ClickableLinks









