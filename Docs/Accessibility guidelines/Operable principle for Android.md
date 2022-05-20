# Operable guidelines for Android 

// TO-DO add better description 

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

### Link purpose 

All the links that are displayed on the components and screens in the application should explain its unique purpose. 





