

- StoreKit
- SKPaymentQueue
-  presentCodeRedemptionSheet() Deprecated

Instance Method

# presentCodeRedemptionSheet()

Displays a sheet that enables customers to redeem subscription offer codes that you configure in App Store Connect.

iOS 14.0–18.0DeprecatediPadOS 14.0–18.0DeprecatedMac Catalyst 14.0–18.0DeprecatedvisionOS 1.0–2.0Deprecated

``` source
func presentCodeRedemptionSheet()
```

Deprecated

Use presentOfferCodeRedeemSheet(in:) or offerCodeRedemption(isPresented:onCompletion:) instead. For more information, see Supporting subscription offer codes in your app.

## Mentioned in 

Testing In-App Purchases in Xcode

Implementing offer codes in your app

Supporting subscription offer codes in your app

## Discussion

The presentCodeRedemptionSheet() function displays a system sheet where customers can enter and redeem subscription offer codes. If you generate subscription offer codes in App Store Connect, call this function to enable customers to redeem the offer. For information on implementing subscription offer codes, see Implementing offer codes in your app.

Note

For apps with more than one scene, and on iOS 16 or later and iPadOS 16 or later, use offerCodeRedemption(isPresented:onCompletion:) or presentOfferCodeRedeemSheet(in:) instead.

When your app calls presentCodeRedemptionSheet(), the system determines where to display the screen. Use presentCodeRedemptionSheet() to support devices running iOS 14 through iOS 15, and iPadOS 14 through iPadOS 15.

Important

Set up subscription offer codes in App Store Connect before calling this API. Customers can only redeem these offers in your app through the redemption sheet; don’t use a custom UI. For information on configuring and generating subscription offer codes, see Set up offer codes.

This method applies to subscription offer codes only; it doesn’t apply to promo codes for apps or in-app purchases. For more information on promo codes, see Request and manage promo codes.

This function doesn’t affect Mac apps built with Mac Catalyst.

