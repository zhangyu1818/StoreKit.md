

- StoreKit
- Product
- Product.SubscriptionInfo
-  winBackOffers 

Instance Property

# winBackOffers

An array of available win-back offers for the auto-renewable subscription that you configured in App Store Connect.

iOS 18.0+iPadOS 18.0+macOS 15.0+tvOS 18.0+visionOS 2.0+watchOS 11.0+

``` source
let winBackOffers: [Product.SubscriptionOffer]
```

## Mentioned in 

Merchandising win-back offers in your app

## Discussion

This list of win-back offers doesn’t take customer eligibility into account, and includes the available offers you’ve configured for the subscription. The customer may not be eligible for all the win-back offers in this array. To get the win-back offers that the customer is eligible for, use eligibleWinBackOfferIDs in the subscription renewal information.

For more information about win-back offers, see Supporting win-back offers in your app.

