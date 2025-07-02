

- StoreKit
- Ad network attribution
- SKAdNetwork
- SKAdNetwork release notes
-  SKAdNetwork 2 release notes 

Article

# SKAdNetwork 2 release notes

A version of SKAdNetwork available in iOS 14 and later.

## Overview

Use `“2.0”` as the version number when signing ads for this version.

Ad networks are eligible to receive a version 2.0 postback if all three of the following conditions are met:

- The source app generates a signature for version 2.0.

- The source app is built with the iOS 14 SDK or later.

- The advertised app is App Store-signed and running on a device with iOS 14 or later.

When verifying an install-validation postback for version 2.0, use the following Apple P-192 public key:

```
MEkwEwYHKoZIzj0CAQYIKoZIzj0DAQEDMgAEMyHD625uvsmGq4C43cQ9BnfN2xslVT5V1nOmAMP6qaRRUll3PB1JYmgSm+62sosG
```

For more information, see Verifying an install-validation postback.

### New features

New features include:

- The advertised app can now provide conversion values. For more information, see updateConversionValue(_:).

- The install-validation postback now contains additional parameters, including the version number, conversion value, source app ID, and redownload value. For more information, see Verifying an install-validation postback.

## See Also

### SKAdNetwork versions

SKAdNetwork 4 release notes

A version of SKAdNetwork available in iOS 16.1 and later.

SKAdNetwork 3 release notes

A version of SKAdNetwork available in iOS 14.6 and later.

SKAdNetwork 2.2 release notes

A version of SKAdNetwork available in iOS 14.5 and later.

SKAdNetwork 2.1 release notes

A version of SKAdNetwork available in iOS 14 and later.

SKAdNetwork 1 release notes

A version of SKAdNetwork available in iOS 11.3 and later.

