

- StoreKit
- In-App Purchase
- Original API for In-App Purchase
-  Handling refund notifications 

Article

# Handling refund notifications

Respond to notifications about customer refunds for consumable, non-consumable, and non-renewing subscription products.

## Overview

The App Store server sends near real-time notifications when customers receive refunds for in-app purchases. If you offer content across multiple platforms, for example gems or coins for games, and you update player account balances on your server, receiving refund notifications is important. Respond to refund notifications by interpreting and handling the refund information, and informing customers in the app of any actions you take as a result of the refund.

To enable notifications, see Enabling App Store Server Notifications and App Store Server Notifications.

### Receive notifications of customer refunds for one-time purchases

Customers request refunds in several ways, such as:

- Contacting Apple Customer Support and asking for a refund

- Logging in and using Apple’s self-service tool, reportaproblem.apple.com, to request a refund

- Asking their payment method issuer for a refund

When the App Store processes a refund, the App Store server sends a `REFUND` notification to your server, at the URL you configure. Your server must respond to the post with a 200 response code. The `REFUND` notification applies to consumable, non-consumable, and non-renewing subscriptions only. To detect refunds for auto-renewable subscriptions, see Detect a Refund.

### Interpret and handle the refund notification

Your server is responsible for parsing and interpreting all notifications from the App Store server. For the `REFUND` notification, identify the specific transaction, product ID, and relevant dates from the response:

- Find the most recent transaction for the `product_id i`n the `unified_receipt.latest_receipt_info` by checking the `purchase_date` to select the most recent transaction.

- The date when App Store issued the refund is in the `cancellation_date_ms` field for the transaction.

For more information about the response, see App Store Server Notifications.

You’re responsible to store, monitor, and take appropriate action for each refunded transaction when you receive a `REFUND` notification. For example, you might build your own in-game currency-rebalancing logic that handles refunded transactions by linking a notification to a player account or session.

Inform customers by presenting contextual messaging in the app for any actions you take as a result of the refund.

### Identify refund abuse

Reduce refund abuse and identify repeated refunded purchases by mapping `REFUND` notifications to the player accounts on your server. Monitor and analyze your data to identify suspicious refund activity.

If you offer content across multiple platforms, keep the balances for user accounts up to date on your server. Use App Store Server Notifications to get near real-time status updates for the transactions that affect your customers.

## See Also

### Refunds

Testing refund requests

Test your app’s implementation of refund requests, and your app’s and server’s handling of approved and declined refunds.

