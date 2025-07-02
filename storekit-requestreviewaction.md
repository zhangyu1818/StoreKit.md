

- StoreKit
-  RequestReviewAction 

Structure

# RequestReviewAction

An instance that tells StoreKit to request an App Store rating or review, if appropriate.

StoreKitSwiftUIiOS 16.0+iPadOS 16.0+Mac Catalyst 16.0+macOS 13.0+visionOS 1.0+

``` source
@MainActor
struct RequestReviewAction
```

## Overview

Read the requestReview environment value to get an instance of this structure for a given Environment. Call the instance to tell StoreKit to ask the user to rate or review your app, if appropriate. You call the instance directly because it defines a callAsFunction() method that Swift calls when you call the instance.

When you call this API in your shipping app and the system displays a rating and review request view, the system handles the entire process for you. Although you normally call this method when it makes sense in the user experience flow of your app, App Store policy governs the actual display of a rating and review request view. When your app calls this API, StoreKit uses the following criteria:

- If the person hasn’t rated or reviewed your app on this device, StoreKit displays the ratings and review request a maximum of three times within a 365-day period.

- If the person has rated or reviewed your app on this device, StoreKit displays the ratings and review request if the app version is new, and if more than 365 days have passed since the person’s previous review.

Note

Because this API may not present an alert, don’t call it in response to a button tap or other user action.

It’s up to your app to decide on the best timing for requesting reviews. For design guidance, see Human Interface Guidelines \> Ratings and reviews.

### Test review requests

When your app calls this method while it’s in development mode, StoreKit always displays the rating and review request view, so you can test the user interface and experience. However, this method has no effect in apps that you distribute for beta testing using TestFlight.

### Provide a persistent link to your product page (optional)

People can review your app at any time on the App Store. To make it easier for people to leave reviews, you may include a persistent link to your App Store product page in your app’s settings or configuration screens. Append the query parameter `action=write-review` to your product page URL to automatically open the App Store page where users can write a review.

## Topics

### Call as function

func callAsFunction()

Tells StoreKit to ask the user to rate or review your app, if appropriate.

### Environment value

var requestReview: RequestReviewAction { get }

## Relationships

### Conforms To

- Sendable

## See Also

### Reviews

Requesting App Store reviews

Implement best practices for prompting users to review your app in the App Store.

class SKStoreReviewController

An object that controls the process of requesting App Store ratings and reviews from customers.

Deprecated

