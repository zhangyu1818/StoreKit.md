

- StoreKit
- Product
- Product.SubscriptionInfo
- Product.SubscriptionInfo.RenewalState
-  expired 

Type Property

# expired

The subscription expired.

iOS 15.0+iPadOS 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+watchOS 8.0+

``` source
static let expired: Product.SubscriptionInfo.RenewalState
```

## See Also

### Getting the renewal state

static let subscribed: Product.SubscriptionInfo.RenewalState

The customer is currently subscribed.

static let inBillingRetryPeriod: Product.SubscriptionInfo.RenewalState

The subscription is in a billing retry period.

static let inGracePeriod: Product.SubscriptionInfo.RenewalState

The subscription is in a billing grace period state.

static let revoked: Product.SubscriptionInfo.RenewalState

The App Store has revoked the customer’s access to the subscription group.

