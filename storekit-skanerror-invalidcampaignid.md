

- StoreKit
- SKANError
-  invalidCampaignId 

Type Property

# invalidCampaignId

The campaign identifier that you provided is invalid.

iOS 15.4+iPadOS 15.4+Mac Catalyst 15.4+visionOS 1.0+

``` source
static var invalidCampaignId: SKANError.Code { get }
```

## Discussion

Check that the campaign identifier is a valid value. For more information, see SKStoreProductParameterAdNetworkCampaignIdentifier for StoreKit-rendered ads, and adCampaignIdentifier for view-through ads.

## See Also

### Getting Error Codes

static var adNetworkIdMissing: SKANError.Code

The ad network identifier in the ad impression doesn’t match the value in the information property list.

static var impressionMissingRequiredValue: SKANError.Code

A required value is missing from a view-through ad impression.

static var impressionNotFound: SKANError.Code

The system can’t find the ad impression.

static var impressionTooShort: SKANError.Code

static var invalidAdvertisedAppId: SKANError.Code

The App Store ID of the advertised app is invalid.

static var invalidConversionValue: SKANError.Code

The conversion value is invalid.

static var invalidSourceAppId: SKANError.Code

The App Store ID of the app displaying the ad is invalid.

static var invalidVersion: SKANError.Code

The SKAdNetwork version number is invalid.

static var mismatchedSourceAppId: SKANError.Code

The source app identifier in the ad impression doesn’t match the app identifier in the source app.

static var unknown: SKANError.Code

An unknown error occurred.

static var unsupported: SKANError.Code

Your app attempted to use functionality that isn’t supported in the specified version.

enum Code

Constants that indicate the type of error for an ad network attribution operation.

