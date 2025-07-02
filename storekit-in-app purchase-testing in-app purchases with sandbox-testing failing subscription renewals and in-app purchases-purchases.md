

- StoreKit
- In-App Purchase
- Testing In-App Purchases with sandbox
-  Testing failing subscription renewals and In-App Purchases 

Article

# Testing failing subscription renewals and In-App Purchases

Verify that your app handles failed subscription renewals that are in the billing retry or billing grace period states, as well as failed In-App Purchases.

## Overview

Payments can fail unexpectedly at any stage of the billing cycle, such as when a payment card expires. Test your app’s user experience to ensure it handles these unexpected events, and provides appropriate levels of service when billing issues occur.

In sandbox testing, you can simulate billing issues that cause In-App Purchases to fail, and auto-renewable subscriptions not to renew. You can also enable Billing Grace Period for the sandbox environment. Use these sandbox features to test how your app handles auto-renewable subscriptions with billing issues that do or don’t recover.

The sandbox environment sends App Store Server Notifications as you perform tests. For more information, see Enabling App Store Server Notifications.

The sandbox environment renews auto-renewable subscriptions up to 12 times. For more information about renewal rates in the sandbox environment, see Edit subscription renewal speed.

For more information about subscription state changes when billing issues occur, see Reducing Involuntary Subscriber Churn. For information about how apps determine access to subscription content, see Handling Subscriptions Billing.

### Configure the sandbox environment to simulate billing issues

Follow these steps on a test device running iOS 16 or iPadOS 16, or later:

1.  Sign in to the App Store using a Sandbox Apple Account.

2.  Choose Settings \> Developer \> Sandbox Account \> Manage \> Account Settings.

3.  Disable the Allow Purchases & Renewals setting.

Disabling this setting causes In-App Purchases to fail, and auto-renewable subscriptions to not renew in the sandbox environment.

Note

This setting applies to all devices that the Sandbox Apple Account signs in to, and to all active auto-renewable subscriptions belonging to that account.

This setting stays in a disabled state until you reenable it. Reenable it to simulate a customer resolving a billing issue.

### Enable Billing Grace Period in the sandbox environment

To enable Billing Grace Period in the sandbox environment, log in to App Store Connect, and do the following:

1.  From My Apps, select your app.

2.  In the sidebar under Features, click Subscriptions.

3.  In the Billing Grace Period section, click Set Up Billing Grace Period.

4.  Select a duration from the drop-down menu.

5.  Select whether to apply the grace period to all renewals or to only paid-to-paid renewals. For more information about the configurable settings, see Enable Billing Grace Period for auto-renewable subscriptions.

6.  Select Only Sandbox Environment to enable Billing Grace Period for testing only.

7.  Click Next.

8.  Click Confirm.

To test billing issues for subscriptions with Billing Grace Period, first, purchase an auto-renewable subscription, and then configure the setting to simulate billing issues (as described above in Configure the sandbox environment to simulate billing issues).

### Test subscriptions that enter a billing retry state

Auto-renewable subscriptions expire and enter a billing retry state when a subscription fails to auto-renew.

This test case assumes that Billing Grace Period is in a disabled state for the sandbox enviroment. To test subscriptions entering a billing retry state:

1.  Successfully purchase an auto-renewable subscription in your app.

2.  Set the environment to simulate billing issues, as described above in Configure the sandbox environment to simulate billing issues.

3.  Wait for the subscription period to renew. The renewal fails, and it enters a billing retry state.

4.  Check that your app recognizes the state. Subscriptions in a billing retry state that aren’t in a billing grace period are not entitled to service. StoreKit provides the isInBillingRetry value in the Product.SubscriptionInfo.RenewalState object.

### Test subscriptions that enter a billing grace period

Auto-renewable subscriptions enter a billing grace period when both of the following occur:

- Billing Grace Period is enabled for your app

- The subscription fails to auto-renew

To test subscriptions entering a billing grace period:

1.  Follow the steps as described above in Enable Billing Grace Period in the sandbox environment.

2.  Successfully purchase an auto-renewable subscription in your app.

3.  Set the environment to simulate billing issues, as described above in Configure the sandbox environment to simulate billing issues.

4.  Wait for the subscription period to renew. The subscription enters the billing grace period.

5.  Check that your app recognizes the state and provides service for the subscription during the billing grace period. StoreKit provides the grace period expiration date in the gracePeriodExpirationDate property of the Product.SubscriptionInfo.RenewalInfo object.

6.  Wait for the billing grace period to expire. The subscription remains in the billing retry state.

7.  Check that your app recognizes the billing retry state. Subscriptions aren’t entitled to service after the billing grace period expires.

Note

Auto-renewable subscriptions in a billing grace period state are entitled to service.

### Test billing problem messaging after a subscription enters a billing retry state

Auto-renewable subscriptions expire and enter a billing retry state when a subscription fails to auto-renew. The system displays a Billing Problem message when your app launches, unless your app chooses to delay the billingIssue message. Use these steps to trigger the message and test how your app responds to the message in various views. For more information about managing these system messages, see Message.

To test when the system presents the Billing Problem sheet after subscriptions enter the billing retry state:

1.  Successfully purchase an auto-renewable subscription in your app.

2.  Set the environment to simulate billing issues, as described above in Configure the sandbox environment to simulate billing issues.

3.  Wait for the subscription period to renew. The renewal fails, and enters a billing retry state.

4.  The App Store sends the billingIssue message. Launch the app or bring it to the foreground.

5.  If your app doesn’t implement messages, the system presents the Billing Problem sheet.

6.  If your app implements messages and delays the message, perform the steps your app requires for it to call display(in:). As long as the billing issue is still active, the system presents the Billing Problem sheet. If you resolve the billing issue before the app calls display(in:), the system doesn’t present the sheet.

You may perform this test with or without Billing Grace Period enabled.

### Test subscriptions that recover from billing issues

A subscription is *recovered* when a billing retry succeeds. It exits a billing retry or billing grace period state, and is active again.

To test recovered auto-renewable subscriptions, follow these steps:

1.  Start with a subscription in the billing retry state, as described above in Test subscriptions that enter a billing retry state.

2.  Choose Settings \> Developer \> Sandbox Account \> Manage \> Account Settings, and enable the Allow Purchases & Renewals setting, which causes the next subscription renewal attempt to succeed.

3.  Check that your app recognizes the active subscription state, which is entitled to service.

Repeat the test starting with a subscription in the billing grace period, as described above in Test subscriptions that enter a billing grace period.

The subscription billing cycle for a subscription that recovers from a billing retry state starts on the recovery date. The billing cycle for a subscription that recovers during a billing grace period doesn’t change.

### Test subscriptions that don’t recover from billing issues

Subscriptions exit a billing retry state when any of the following happens:

- The billing retry period expires without recovering the subscription.

- The customer cancels the subscription.

- The subscription is recovered because billing succeeds.

To test subscriptions that expire and don’t recover, follow these steps:

1.  Start with a subscription in a billing retry state, as described above in Test subscriptions that enter a billing retry state.

2.  Wait for the billing retry period to expire — don’t enable the Allow Purchases & Renewals setting.

3.  Check that your app recognizes the subscription state. The subscription is inactive and not entitled to service.

To test a subscription that a customer cancels, follow these steps:

1.  Start with a subscription in a billing grace period, as described above in Test subscriptions that enter a billing grace period.

2.  Cancel the subscription by managing subscriptions in Settings, or by using your app’s implementation of showManageSubscriptions(in:). For more information about managing subscriptions in Settings, see If you want to cancel a subscription from Apple.

3.  The system immediately cancels the subscription.

4.  Check that your app recognizes the subscription state. The subscription is inactive and not entitled to service.

Repeat the test starting with a subscription in the billing retry state, as described above in Test subscriptions that enter a billing retry state.

### Test a failed In-App Purchase

To test a failed purchase attempt, follow these steps:

1.  Set the environment to simulate billing issues, as described above in Configure the sandbox environment to simulate billing issues.

2.  In your app, attempt to buy an In-App Purchase product. The system displays an error message for the sandbox environment that shows the purchase failed.

3.  To continue testing billing issues, select OK. Alternatively, to simulate a user resolving a billing issue, select Settings to return to Account Settings, where you can enable Allow Purchases & Renewals.

## See Also

### Payment transactions

Testing purchases made outside your app

Verify that your app receives and handles transactions that occur outside your app, such as subscription purchases, renewals, and offer and promo code redemptions.

Testing win-back offers in the sandbox environment

Verify that your app receives and handles win-back offer transactions, including those made outside your app.

Testing an interrupted purchase

Verify that your app handles an interrupted purchase by inspecting and invoking payment transactions.

Testing a payment request

Verify that requests for payment function properly in the sandbox environment by inspecting the calls to the payment transaction observer.

