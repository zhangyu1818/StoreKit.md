

- StoreKit
- Ad network attribution
- SKAdNetwork
- Generating the signature to validate StoreKit-rendered ads
-  Combining parameters to generate a signature for SKAdNetwork 1 

Article

# Combining parameters to generate a signature for SKAdNetwork 1

Generate signatures for apps compiled with earlier SDKs.

## Overview

Generate a signature using the parameters for version 1.0 if you compile your app with an iOS SDK version from 11.3 through 13.7.

To generate the signature, first combine the values of Ad network install-validation keys for the version 1.0.

The parameters required for a version 1.0 signature are:

SKStoreProductParameterAdNetworkIdentifier  
Your ad network identifier that you registered with Apple. Shown as `ad-network-id` in Combine the parameters for version 1.0.

SKStoreProductParameterAdNetworkCampaignIdentifier  
A campaign number you provide. Shown as `campaign-id` in Combine the parameters for version 1.0.

SKStoreProductParameterITunesItemIdentifier  
The App Store ID of the product to advertise. Shown as `itunes-item-id` in Combine the parameters for version 1.0.

SKStoreProductParameterAdNetworkNonce  
A unique `UUID` value that you provide for each ad impression. You must lowercase the string representation of the nonce in the signature. Shown as `nonce` in Combine the parameters for version 1.0.

SKStoreProductParameterAdNetworkTimestamp  
A timestamp you generate near the time of the ad impression. Shown as `timestamp` in Combine the parameters for version 1.0.

### Combine the parameters for version 1.0

Create the UTF-8 string for version 1.0 if you compile your app with an SDK prior to iOS 14.

Important

You must use lowercase for the string representation of the nonce: SKStoreProductParameterAdNetworkNonce.

Combine the values into a UTF-8 string with an invisible separator (`‘\u2063’`) between them, in the exact order shown:

```
ad-network-id + '\u2063' + campaign-id + '\u2063' + itunes-item-id + '\u2063' + nonce + '\u2063' + timestamp

```

Next, follow the instructions to sign the combined string, encode the signature, and use the generated signature string as described in Generating the signature to validate StoreKit-rendered ads.

## See Also

### Signatures for SKAdNetwork 1, 2, and 2.2–3

Combining parameters to generate signatures for SKAdNetwork 2.2 and 3

Generate signatures to sign your ad with versions 2.2 and 3.

Combining parameters to generate a signature for SKAdNetwork 2

Generate signatures to sign your ad with version 2.

