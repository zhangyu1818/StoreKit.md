

- StoreKit
- In-App Purchase
- Testing In-App Purchases with sandbox
-  Testing disabling auto-renew 

Article

# Testing disabling auto-renew

Verify that your app receives subscription updates when a user cancels a subscription by verifying the receipt or receiving a notification.

## Overview

Customers can manage their active subscriptions, as well as their expired subscriptions for up to a year after expiry, in the Subscriptions page on iOS, tvOS, iPadOS, and macOS. In this test scenario, the customer cancels a subscription, which disables auto-renew.

To set up for this test, purchase an auto-renewable subscription for the Sandbox Apple Account.

### Begin testing

To test disabling auto-renew:

1.  On the test iOS device, open Settings \> Developer.

2.  In the Sandbox Account section, tap your highlighted Sandbox Apple Account, and tap Manage.

3.  In the sandbox Subscriptions page, select the subscription product that you want to cancel.

4.  Tap the Cancel Subscription button.

Verify the change in the subscription status using either of these two methods:

- If you’ve configured App Store Connect settings to receive App Store server notifications, your server receives the notification_type `DID_CHANGE_RENEWAL_STATUS` each time the subscription’s auto-renew status changes. For more information, see Enabling App Store Server Notifications.

- Verify the receipt by calling verifyReceipt with the latest receipt. Check that the auto_renew_status property of the responseBody.Pending_renewal_info object changes to `0`. The `auto_renew_status_change_date_ms` property of `responseBody` contains the timestamp of the change.

### Test reenabling the subscription renewal

After disabling auto-renew, reenable the subscription on the same Manage Subscriptions page by tapping the subscription and confirming payment.

Verify the change in the subscription status using either of these two methods:

- If you’ve configured App Store Connect settings to receive App Store server notifications, your server receives the notification_type `DID_CHANGE_RENEWAL_STATUS` each time the subscription’s auto-renew status changes. For more information, see Enabling App Store Server Notifications.

- Verify the receipt by calling verifyReceipt with the latest receipt. Check that the auto_renew_status property of the responseBody.Pending_renewal_info object changes to `1`. The `auto_renew_status_change_date_ms` property of `responseBody` contains the timestamp of the change.

## See Also

### Subscriptions

Testing an auto-renewable subscription

Verify that your app handles a subscription lapse properly using the accelerated time rates within the sandbox environment.

Testing resubscribing from the subscriptions page

Verify that your app can reactivate an expired subscription by receiving a transaction callback or inspecting an updated receipt.

