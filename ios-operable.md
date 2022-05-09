
# Operable

User interface components and navigation must be operable.

## 2.2 Enough Time

_Provide users enough time to read and use content._

### Timing Adjustable

For each time limit set by the content, user can turn off, adjust, or extend it.

#### Success technique(s)

Session inactivity timeout: Display a warning message that user is about to be signed out with extension option. Or allow user to increase default kick-out timeout time of inactivity ten times (e.g. from 30s to 5 min) so they have enough time to process content.

Auto-updating content (like news page): allow user to extend the time limit to 10 times longer.

Real-time exception: time limit cannot be disabled/extended for a real-time event (e.g. an auction, booking movie tickets, watching live stream)

#### Failures

Logging user out of their session with no prior warning.
Not providing enough time or time extensions to react on an incoming action in the app.

#### Additional notes

This guideline covers point 2.2.1 Timing Adjustable - Level A of the WCAG standard.

---

### Pause, Stop, Hide

Moving, blinking, or scrolling, or auto-updating content in the app

#### Success technique(s)

When using auto-scrolling page views (carousels) whose animation starts automatically make sure to provide a way for user to pause, stop, or hide it.
If there is no parallel content next to the moving, blinking, or scrolling content there's no need to provide a pause, stop or hide button.
Loading screens doesn't require to meet this success criterion.

#### Failures

Using an auto-updating or auto-scrolling view that can't be paused/stopped.

#### Additional notes

This guideline covers point 2.2.2 Pause, Stop Hide - Level A of the WCAG standard.

---


## 2.3 Seizures and Physical Reactions

_Do not design content in a way that is known to cause seizures or physical reactions._

### Three Flashed or Below Treshold

Apps should not contain any element that flashes more than three times in any one second period.

#### Success technique(s)

Avoid flashing content altogether if possible. 
If not, make sure that any flashing elements have a period of at least 333 ms.
If you do have an element that flashes more frequently - ensure that the flashing area is less than 25% of 10 degrees of visual field.

#### Failures

Using rapidly flashing elements to catch user's attention.
Having a larger area of screen flashing more than three times per second.

#### Additional notes

This guideline covers point 2.3.1 - Level A of the WCAG standard.

---

## 2.4 Navigable

_Provide ways to help users navigate, find content, and determine where they are._

### Bypass Blocks

A skip mechanism is available to bypass blocks of content that are repated in the app.

#### Success technique(s)

VoiceOver: A section of a screen containing numerous items should have those items grouped and an accessibility label with quick summary of the contents. This way if they are relevant to the user, user may swipe up or down to iterate through each item, and in case they are not user may use left or right swipe to skip them.

An element containing many labels or buttons should also have a summary accessibility label so it takes less swipes to skip over it.

#### Failures

Not providing a way for user to quickly skip over sections with numerous items.

#### Additional notes

This guideline covers point 2.4.1 Bypass Blocks - Level A of the WCAG standard.

---


### Page Titled

Screens have a clear, descriptive, and possibly unique title that describes topic or purpose and is easily understood by all users.

#### Success technique(s)

Make sure that each screen in the app has a title at or near the top.
VoiceOver: when user requests entire screen to be read from the top, make sure that the title is one of the first things user will hear so they know whether they are on the right page or step.
If using custom navigation bar, make sure that the title can be ready correctly by VoiceOver.

#### Failures

Leaving the title empty
Using a custom navigation bar without ensuring it's readable by VoiceOver.
In document-editor screens: using a default title such as "Untitled Document" or "No Title", as well as just using file name like "report.pdf" or "DSC_0123.jpeg"
Placeholder text like "Enter title..."

#### Additional notes

This guideline covers point 2.4.2 Page Titled - Level A of the WCAG standard.

---


### Focus Order

VoiceOver: Ensure that information is read in an order consistent with the meaning and content.

#### Success technique(s)

VoiceOver: When designing a new screen, make sure to test it with VoiceOver and see whether the elements are being read out in right, logical order. 

In case of multiple text fields displayed, make sure that tapping "next" leads to the expected one.

#### Failures

VoiceOver: Elements are being read out in the wrong order, or some elements are skipped.

Focus is trapped within the modal and cycles between the elements.

#### Additional notes

This guideline covers point 2.4.3 Focus Order - Level A of the WCAG standard.

---


### Link Purpose

Purpose of a button or link is clear and easily understable by all users

#### Success technique(s)

Create button with content that helps people instantly understand what it does. 
Use short, concise titles that succinctly describe buttons purpose.
Start the title with a verb where possible.

When using toggle buttons, avoid relying solely on color to communicate its state - add a background shape or change the button’s content too.

#### Failures

Using custom shaped buttons that do not look like buttons.
Generic button titles like "OK", or "Yes" and "No"
Button titles with unclear result like "Ready to publish?"

#### Additional notes

This guideline covers point 2.4.4 Link Purpose (In Context) - Level A of the WCAG standard.

---



