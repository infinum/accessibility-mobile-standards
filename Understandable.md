# Understandable

Information and the operation of the user interface must be understandable.

## Readable

Make text content readable and understandable.

### Language of Page

The default human language of an App can be programmatically determined.

#### Success technique(s)

Specify the default language of the application in the headers of the API calls. This would allow for the app language to be changed dynamically by any back-end response, which would for example allow users from a certain location to get the app in their own language even if they want to keep using their device in a different language. We should also provide an option for the user to choose this option in the in-app settings, or maybe even display a popup reminding them that the app uses a default language based on their location/region settings, and that if they want to override this setting they can do so in the in-app setting. Users should also be able to allow the app to follow the device settings for the language preference.

#### Failures

Hard-coding a language code inside an app should be avoided. Also, every app should be developer as a localizable app, even if it seems like it makes no sense at the start, or all of the intended audience speak a single language, it can still happen that some users will not be able to use that language and there is always a possibility that your app will scale to different language regions or that parts of your code will be reused on different projects which _do_ use localization.

#### Additional notes

This guideline covers point 3.1.1 Language of Page - Level A of the WCAG standard.

---

## Predictable

Make mobile apps appear and operate in predictable ways.

### On Focus & On Input

Receiving focus on or interacting with any component should not initiate a change of context unless previously announced.

#### Success technique(s)

Users need to be able to consume content without any sudden interruptions and/or changes of context. Interacting with any UI component doesn't automatically cause a change of context unless the user has been previously advised of the behavior _before_ using the component.

#### Failures

Showing programmatically pre-planned popups, modals, or any unusual navigation not directly initiated by the user is considered a change of context.

#### Additional notes

This technique covers points 3.2.1 On Focus - Level A & 3.2.2 On Input - Level A of the WCAG standard.

---

## Input Assistance

Help users avoid and correct mistakes when interacting with the app.

### Error Identification

If an input error is automatically detected, the item that is in error is identified and the error is clearly described to the user in text.

#### Success technique(s)

If a form contains fields for which information from the user is mandatory the app should provide text descriptions to help identify those fields which are not sufficiently filled-out. The app should be able to validate and present a human-understandable error to the user even without needing to reach a remote endpoint.

Information provided by the user which is required to be in a specific format or contain certain values this should be clearly communicated to the user and the error messages must be even more descriptive, providing concrete information regarding the required format or the range of values that an input needs to satisfy.

When data is successfully entered in such a form on the other hand, some success feedback should be given to the user so that they know they've completed the action.

#### Failures

Preventing some action or flow from continuing because an error was detected but not communicating to the user how/when the error was made and/or what needs to be done to correct it.

#### Additional notes

This technique covers point 3.3.1 Error Identification - Level A of the WCAG standard.

### Labels or Instructions

Labels or instructions are provided when content requires user input.

#### Success technique(s)

Descriptive labels should be applied to user interface elements, especially those that the user is expected to interact with.

Elements should be grouped into logical groups to help users distinguish between different parts of the user interface and switch between contexts quickly and easily.

#### Failures

User enters some data into a user interface element without knowing what the end result is and/or triggering an unannounced change of context in the process.

#### Additional notes

This technique covers point 3.3.2 Labels or Instructions - Level A of the WCAG standard.

