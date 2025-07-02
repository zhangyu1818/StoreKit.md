

- StoreKit
- In-App Purchase
- Testing In-App Purchases with sandbox
-  Testing an auto-renewable subscription 

Article

# Testing an auto-renewable subscription

Verify that your app handles a subscription lapse properly using the accelerated time rates within the sandbox environment.

## Overview

Auto-renewable subscriptions behave differently in the sandbox environment and the production environment.

In the sandbox environment, subscription renewals happen at an accelerated rate, and auto-renewable subscriptions renew up to 12 times after the initial purchase. This enables you to test how your app handles a subscription renewal, a subscription lapse, and a subscription history that includes gaps.

You can choose a subscription renewal speed for each Sandbox Apple ID account in App Store Connect. For a complete list of subscription durations within the sandbox environment and more information, see Manage Sandbox Apple ID settings.

The accelerated expiration and renewal rates in the sandbox environment make it possible for subscriptions to expire before the system tries to renew them. When a subscription expires before the system tries to renew it, it results in a short lapse in the subscription period. These lapses are possible in production; verify that your app handles them appropriately.

## See Also

### Subscriptions

Testing resubscribing from the subscriptions page

Verify that your app can reactivate an expired subscription by receiving a transaction callback or inspecting an updated receipt.

Testing disabling auto-renew

Verify that your app receives subscription updates when a user cancels a subscription by verifying the receipt or receiving a notification.

