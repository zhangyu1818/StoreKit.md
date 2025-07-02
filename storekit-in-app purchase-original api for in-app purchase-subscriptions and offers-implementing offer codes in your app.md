

- StoreKit
- In-App Purchase
- Original API for In-App Purchase
- Subscriptions and offers
-  Implementing offer codes in your app 

Article

# Implementing offer codes in your app

Provide subscription service for customers who redeem offer codes through the App Store or within an app that uses receipts.

## Overview

To help you acquire, retain, and win back subscribers, you can use offer codes.

Offer codes are alphanumeric codes that provide subscriptions at a discount or for free for a specific duration. Configure the offers and create offer codes in App Store Connect, and distribute them to your customers. Customers can redeem offer codes in the App Store, using offer code redemption URLs, or in your app if you’ve implemented one of the following APIs:

- offerCodeRedemption(isPresented:onCompletion:) or presentOfferCodeRedeemSheet(in:), which are available in iOS 16 and later and iPadOS 16 and later

- presentCodeRedemptionSheet(), which is available in iOS 14 and later and iPadOS 14 and later.

When customers redeem a valid offer code, your app receives a successful transaction on the payment queue, and you receive a server notification if you’ve enabled App Store Server Notifications. The receipt contains an `offer_code_ref_name` field that identifies the offer.

For information on subscription offer types and choosing the offer type to suit your business needs, see Providing subscription offers.

### Set up offer codes in App Store Connect

Configure offers and manage your offer codes in App Store Connect. You can have up to 10 active offers per subscription, and create codes for a maximum of 1,000,000 redemptions per app, per quarter. There are two types of offer codes: one-time use codes, and custom codes. The offer code redemption APIs support both.

Download the offer codes from App Store Connect to distribute them to your customers. For more information on creating and distributing offer codes, and to learn which type of offer code may work for your campaign, see Set up offer codes.

### Redeem offer codes in your app

To display the system sheet for customers to redeem offer codes within your app, call one of the redemption APIs, depending on your app’s UI implementation:

- Call offerCodeRedemption(isPresented:onCompletion:) if your app uses SwiftUI.

- Call presentOfferCodeRedeemSheet(in:) if your app uses UIKit.

- Call presentCodeRedemptionSheet() for apps running on devices prior to iOS 16 and iPadOS 16.

The redemption sheet takes care of the redemption flow, including alerting customers about invalid entries, as appropriate. Invalid entries may include, for example, expired offer codes, invalid codes, or codes that would result in a subscription downgrade.

Including the redemption sheet in your app is recommended, but optional. For more guidance on supporting offer code redemption within your app, see Human Interface Guidelines \> In-app purchase.

### Support offer codes redeemed outside your app

Customers may redeem subscription offer codes outside your app. If a customer doesn’t have your app, the App Store prompts them to download it as part of the redemption flow.

To handle offer codes — and other transactions that can occur outside of your app – you need to set up a transaction observer at app launch. For more information on this best practice, see Setting up the transaction observer for the payment queue. Check that your app’s customer-onboarding experience verifies the receipt and provides subscription service. Update your records if you keep a backend system to manage your subscribers.

### Identify subscriptions purchased with offer codes, in receipts

When a customer successfully redeems a subscription offer code, the receipt contains a transaction with the field: `offer_code_ref_name`. This field’s value is the offer reference name that you configured in App Store Connect. The field appears in the responseBody.Latest_receipt_info and responseBody.Pending_renewal_info objects for receipts, and in the unified_receipt.Latest_receipt_info and unified_receipt.Pending_renewal_info objects for server notifications.

### Provide subscription service to existing and new customers

When an existing customer redeems an offer code, your app receives a transaction on the payment queue (paymentQueue(_:updatedTransactions:) in the SKPaymentTransactionState.purchased state. This flow is the same as a typical subscription purchase flow, but the receipt contains the offer code reference. Your app follows these steps:

1.  Validates the receipt. For more information, see Validating receipts with the App Store.

2.  Looks for the `offer_code_ref_name` field in the receipt to determine if the subscription is from an offer code.

3.  Provides the subscription service based on the offer.

4.  Calls finishTransaction(_:).

When you acquire new customers with an offer code, they open your app for the first time already having a subscription. In addition to providing subscription service, you may need to update your backend system’s records. Your app follows these steps:

1.  When the app first launches, validate the receipt.

2.  In the receipt, look for a transaction with the `offer_code_ref_name` field to determine if the subscription is from an offer code.

3.  Provide the subscription service based on the offer.

4.  Guide the customer through your new-customer experience as needed. Update your backend system’s records.

5.  Call finishTransaction(_:).

