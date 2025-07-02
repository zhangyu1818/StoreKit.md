

- StoreKit
- Ad network attribution
- SKAdNetwork
- SKAdNetwork release notes
-  SKAdNetwork 3 release notes 

Article

# SKAdNetwork 3 release notes

A version of SKAdNetwork available in iOS 14.6 and later.

## Overview

Use `“3.0”` as the version number when signing ads for this version.

You’re eligible to receive a version 3.0 postback if all three of the following conditions are met:

- The source app generates a signature for version 3.0.

- The source app is built with iOS 14.6 SDK or later.

- The advertised app is App Store-signed and is running on a device with iOS 14.6 or later.

### New features

New features include:

- Devices can now send install-validation postbacks to multiple ad networks that sign their ads using version 3.0. One ad network receives a postback with a `did-win` parameter value of `true` for the ad impression that wins the ad attribution. Up to five other ad networks receive a postback with a `did-win` parameter value of `false` if their ad impressions qualified for, but didn’t win, the attribution.

For more information about signing ads with version 3.0, see Signing and providing ads. For more information about your ad’s eligibility to receive an attribution or a non-winning postback, see Receiving ad attributions and postbacks. For details about the postback, see Verifying an install-validation postback.

## See Also

### SKAdNetwork versions

SKAdNetwork 4 release notes

A version of SKAdNetwork available in iOS 16.1 and later.

SKAdNetwork 2.2 release notes

A version of SKAdNetwork available in iOS 14.5 and later.

SKAdNetwork 2.1 release notes

A version of SKAdNetwork available in iOS 14 and later.

SKAdNetwork 2 release notes

A version of SKAdNetwork available in iOS 14 and later.

SKAdNetwork 1 release notes

A version of SKAdNetwork available in iOS 11.3 and later.

