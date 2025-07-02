

- StoreKit
- In-App Purchase
- Testing In-App Purchases with sandbox
-  Testing win-back offers in the sandbox environment 

Article

# Testing win-back offers in the sandbox environment

Verify that your app receives and handles win-back offer transactions, including those made outside your app.

## Overview

After you set up win-back offers for auto-renewable subscriptions in App Store Connect, you can begin testing them in the sandbox environment. You can merchandise win-back offers in multiple ways, enabling customers to discover and redeem them in the App Store, in their Apple Account in Subscription settings, in your own marketing channels, and in your app. Within your app, you can merchandise win-back offers by using the win-back offer sheet, StoreKit views, or other StoreKit APIs for full customization.

You can use the sandbox testing environment to simulate redeeming win-back offers in these ways:

Outside the app  
Customers can redeem win-back offers in the App Store, through a direct link, or in the Subscription settings in their Apple Account. You can simulate redeeming win-back offers outside the app by using the Test Transactions feature in the sandbox Account Settings in iOS. The system applies the win-back offer if the test account is eligible for it.

In the app, using the win-back offer sheet  
To simulate redeeming a win-back offer in your app, turn on the Display Win-back Offer Sheet toggle in Account Settings in iOS. The system displays a win-back offer sheet, using the Message API’s winBackOffer reason, when you launch the app. The test account needs to be eligible for the offer in the sandbox environment. This option is only available to apps running in iOS 18 and iPadOS 18 and later.

In the app, using StoreKit views or your custom code  
Follow the steps to make the test account eligible for the offer in the sandbox environment. Exercise your app’s implementation that uses StoreKit views or your custom code using StoreKit APIs. StoreKit views automatically chooses an offer to display.

Handle the resulting transactions in your app. StoreKit delivers them through the updates asynchronous sequence in Transaction.

Note

In TestFlight testing, you can only test win-back offers if you implement them using StoreKit views or other StoreKit APIs. The win-back offer sheet and redemption through the App Store aren’t available for testing in TestFlight.

Other types of offers and transactions can also occur outside your app. For testing information, see Testing purchases made outside your app. You can also test win-back offers in Xcode, which doesn’t rely on App Store Connect configurations. For more information, see Testing win-back offers in Xcode.

### Set up win-back offer testing in App Store Connect and Account Settings

Before you begin testing in the sandbox environment, use App Store Connect to configure at least one auto-renewable subscription, and at least one win-back offer. Make a note of the product ID of the auto-renewable subscription and the corresponding win-back offer IDs to use in your tests.

Note

Changes that you make to product metadata in App Store Connect can take up to one hour to appear in the sandbox environment.

On the iOS device, set up the testing environment by opening Account Settings, as follows:

1.  Open Settings and select Developer.

2.  Select the Sandbox Apple Account. If you’re not yet signed in, see Sign in to the App Store with your Sandbox Apple Account to sign in. A popover appears.

3.  Select Manage on the popover. The Account Settings page appears.

4.  Check that the Allow Purchases & Renewals toggle remains on. If it’s off, all purchases fail, which represents a different test case. For more information, see Testing failing subscription renewals and In-App Purchases.

5.  Turn on or off the Win-Back Offer Sheet toggle. Turn it on to enable the Message API to display the win-back offer sheet when you launch the app. Turn it off to prevent the sheet from appearing, even if the customer is eligible for the offer. This toggle only affects sandbox testing. In either case, StoreKit delivers the new transaction to your app through the updates asynchronous sequence in Transaction.

### Prepare eligibility conditions

In the sandbox environment, test accounts are automatically eligible for win-back offers when they have an expired subscription. The account needs to have owned the subscription; having access through Family Sharing doesn’t qualify the account for a win-back offer. Also, the account can’t have any active subscriptions from the same subscription group.

To make your Sandbox Apple Account eligible for a win-back offer, follow these steps:

1.  Cancel any subscriptions that are from the same subscription group as the win-back offer’s subscription.

2.  If the test account has an active subscription through Family Sharing in the same subscription group, it’s ineligible for a win-back offer in that subscription group. To make the account eligible, leave the family group, or stop sharing the subscription with the family.

3.  Wait for the subscription to expire. By default, a monthly subscription expires in 5 minutes in the sandbox. For more information, see Manage Sandbox Apple Account settings .

4.  Subscribe to the auto-renewable subscription that has the win-back offer you’re testing.

5.  Cancel the subscription and wait for it to expire.

6.  Close the app.

The Sandbox Apple Account is now eligible for the win-back offer in the sandbox environment.

Repeat these steps to repeat a test.

### Test redeeming a win-back offer outside the app

To simulate a win-back offer redemption outside your app, follow these steps:

1.  Complete the steps in the preceding sections: Set up win-back offer testing in App Store Connect and Account Settings and Prepare eligibility conditions. Close your app.

2.  On the Account Settings page (Settings \> Developer \> Sandbox Apple Account \> Manage), select Test Transactions.

3.  Enter the auto-renewable subscription’s product ID and the bundle ID in the applicable text boxes.

4.  Enter the win-back offer ID in the Win-Back ID text box. The win-back offer ID needs to be a valid offer for the product, that you configure in App Store Connect.

5.  The system presents the App Store \[Sandbox\] payment sheet for the sandbox environment. Confirm the purchase.

6.  Launch your app. StoreKit provides the transaction in the updates asynchronous sequence.

7.  Check that your app receives and processes the win-back offer transaction.

Note

The sandbox environment doesn’t process actual payments. Instead, it returns transactions as if the system successfully processes them.

### Test redeeming an offer in your app using the win-back offer sheet

To simulate a win-back offer redemption in your app, follow these steps:

1.  Complete the steps in the preceding sections: Set up win-back offer testing in App Store Connect and Account Settings and Prepare eligibility conditions. Close the app.

2.  On the Account Settings page (Settings \> Developer \> Sandbox Apple Account \> Manage), turn on the Display Win-back Offer Sheet toggle.

3.  Launch your app. The system presents the win-back offer sheet.

4.  Accept the offer. The system presents the App Store \[Sandbox\] payment sheet for the sandbox environment. Confirm the purchase.

5.  Check that your app receives and processes the win-back offer transaction.

### Test redeeming an offer in your app through StoreKit views or your customized code

If you merchandise the win-back offer using StoreKit views or other StoreKit APIs to fully customize the experience, you can test your implementation in the sandbox environment. Follow these steps:

1.  Complete the steps in the preceding sections to ensure the test account is eligible for one or more win-back offers: Set up win-back offer testing in App Store Connect and Account Settings and Prepare eligibility conditions. Close the app.

2.  Optionally, on the Account Settings page (Settings \> Developer \> Sandbox Apple Account \> Manage), turn off the Display Win-back Offer Sheet toggle to prevent the win-back offer sheet from appearing.

3.  Launch your app. Open your app’s store and exercise the offer API.

4.  StoreKit views automatically chooses an offer to display. If there are multiple offers, your app indicates a preference using the preferredSubscriptionOffer(_:) API.

For more information about customizing your in-app experience, see Merchandising win-back offers in your app and Supporting win-back offers in your app.

### Restart or conclude a test

To repeat a test and redeem the same win-back offer, cancel the subscription and wait for it to expire. The test account in the sandbox environment is eligible for the same win-back offer after the subscription expires.

## See Also

### Payment transactions

Testing purchases made outside your app

Verify that your app receives and handles transactions that occur outside your app, such as subscription purchases, renewals, and offer and promo code redemptions.

Testing an interrupted purchase

Verify that your app handles an interrupted purchase by inspecting and invoking payment transactions.

Testing failing subscription renewals and In-App Purchases

Verify that your app handles failed subscription renewals that are in the billing retry or billing grace period states, as well as failed In-App Purchases.

Testing a payment request

Verify that requests for payment function properly in the sandbox environment by inspecting the calls to the payment transaction observer.

