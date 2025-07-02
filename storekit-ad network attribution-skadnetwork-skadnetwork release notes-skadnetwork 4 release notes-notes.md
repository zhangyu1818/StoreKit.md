

- StoreKit
- Ad network attribution
- SKAdNetwork
- SKAdNetwork release notes
-  SKAdNetwork 4 release notes 

Article

# SKAdNetwork 4 release notes

A version of SKAdNetwork available in iOS 16.1 and later.

## Overview

Use `“4.0”` as the version number when signing ads for this version.

You’re eligible to receive a version 4 postback if all participants meet the following conditions:

- The ad network generates an ad signature for version 4.

- For ads that appear in an app, the app is built with iOS 16.1 SDK or later. For web ads, the ad appears in Safari 16.1 or later.

- The advertised app is App Store-signed and is running on a device with iOS 16.1 or later.

Advertised apps built with iOS 16.1 SDK or later can register up to three conversions that result in postbacks for the winning ad impression. Apps built with earlier SDKs can register only one conversion, resulting in one winning postback.

### New features

- Multiple postbacks. SKAdNetwork now supports multiple conversions in three conversion windows. When you call the new methods updatePostbackConversionValue(_:coarseValue:completionHandler:) and updatePostbackConversionValue(_:coarseValue:lockWindow:completionHandler:), the app can update conversion values in three separate conversion windows. The app may send up to three postbacks for the winning ad attribution.

You can lock a conversion during a conversion window to receive the postback sooner by calling updatePostbackConversionValue(_:coarseValue:lockWindow:completionHandler:) and setting the lock to `true`. Otherwise, the system sends postbacks after the conversion window closes. For more information about postback timing, see Receiving ad attributions and postbacks. For more information about multiple postbacks, see Receiving postbacks in multiple conversion windows.

- Coarse conversion values. The conversion value that you send can include both a fine-grained value and a coarse-grained value. For information about coarse conversion values, see SKAdNetwork.CoarseConversionValue. You provide the fine and coarse conversion values in the new methods updatePostbackConversionValue(_:coarseValue:completionHandler:) and updatePostbackConversionValue(_:coarseValue:lockWindow:completionHandler:).

- Hierarchical source identifiers. Ad networks can now provide hierarchical source identifiers when they sign an ad, which replaces and expands on campaign identifiers. The source identifer is a four-digit integer, which you indicate in sourceIdentifier for view-through ads and in SKStoreProductParameterAdNetworkSourceIdentifier for StoreKit-rendered ads. Winning postbacks contain two, three, or four digits of the source identifier, depending on the ad impression’s privacy threshold tier.

- Attributed ads on the web. SKAdNetwork for Web Ads supports attributed ads that you initiate on Safari web pages.

## See Also

### SKAdNetwork versions

SKAdNetwork 3 release notes

A version of SKAdNetwork available in iOS 14.6 and later.

SKAdNetwork 2.2 release notes

A version of SKAdNetwork available in iOS 14.5 and later.

SKAdNetwork 2.1 release notes

A version of SKAdNetwork available in iOS 14 and later.

SKAdNetwork 2 release notes

A version of SKAdNetwork available in iOS 14 and later.

SKAdNetwork 1 release notes

A version of SKAdNetwork available in iOS 11.3 and later.

