

- StoreKit
- Ad network attribution
- SKAdNetwork
- SKAdNetwork release notes
-  SKAdNetwork 2.2 release notes 

Article

# SKAdNetwork 2.2 release notes

A version of SKAdNetwork available in iOS 14.5 and later.

## Overview

Use `“2.2”` as the version number when signing ads for this version.

Ad networks are eligible to receive a version 2.2 postback if all three of the following conditions are met:

- The source app generates a signature for version 2.2.

- The source app is built with iOS 14.5 SDK or later.

- The advertised app is App Store-signed and running on a device with iOS 14.5 or later.

### New features

New features include:

- You can now create view-through ads using the new APIs SKAdImpression , startImpression(_:completionHandler:), and endImpression(_:completionHandler:).

- You can now indicate whether an ad is a view-through ad or a StoreKit-rendered ad by using the new `fidelity-type` parameter. The `fidelity-type` value is `0` for view-through ads, and `1` for StoreKit-rendered ads. You include this parameter when you sign an ad, and receive it in the postback.

For more information about view-through ads and `fidelity-type`, see Signing and providing ads and Generating the signature to validate view-through ads. For more information about the postback, see Verifying an install-validation postback.

## See Also

### SKAdNetwork versions

SKAdNetwork 4 release notes

A version of SKAdNetwork available in iOS 16.1 and later.

SKAdNetwork 3 release notes

A version of SKAdNetwork available in iOS 14.6 and later.

SKAdNetwork 2.1 release notes

A version of SKAdNetwork available in iOS 14 and later.

SKAdNetwork 2 release notes

A version of SKAdNetwork available in iOS 14 and later.

SKAdNetwork 1 release notes

A version of SKAdNetwork available in iOS 11.3 and later.

