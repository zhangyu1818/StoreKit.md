

- StoreKit
- AdvancedCommerceProduct
-  currentEntitlements 

Instance Property

# currentEntitlements

The transactions that entitle the customer to Advanced Commerce Items purchased using the generic product ID.

iOS 18.4+iPadOS 18.4+macOS 15.4+tvOS 18.4+visionOS 2.4+watchOS 11.4+

``` source
var currentEntitlements: Transaction.Transactions { get }
```

## See Also

### Getting transactions and entitlements

var allTransactions: Transaction.Transactions

All transactions associated with the generic product ID.

var latestTransaction: VerificationResult&lt;Transaction>?

The most recent transaction associated with the generic product ID, if it exists.

