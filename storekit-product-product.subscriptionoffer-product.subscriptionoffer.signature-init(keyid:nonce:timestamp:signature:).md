

- StoreKit
- Product
- Product.SubscriptionOffer
- Product.SubscriptionOffer.Signature
-  init(keyID:nonce:timestamp:signature:) 

Initializer

# init(keyID:nonce:timestamp:signature:)

Creates a subscription offer signature instance.

iOS 17.4+iPadOS 17.4+macOS 14.4+tvOS 17.4+visionOS 1.1+watchOS 10.4+

``` source
init(
    keyID: String,
    nonce: UUID,
    timestamp: Int,
    signature: Data
)
```

## Parameters 

`keyID`  

A string that identifies the private key you use to generate the signature. You set up this key in App Store Connect. For more information, see Generate keys for in-app purchases.

`nonce`  

A one-time UUID value that your server generates. Generate a new nonce for each signature. The string representation of the nonce you use in the signature must be lowercase.

`timestamp`  

A timestamp your server generates in UNIX time format, in milliseconds. The timestamp keeps the offer active for 24 hours.

`signature`  

The cryptographic signature your server generates to sign the promotional offer.

