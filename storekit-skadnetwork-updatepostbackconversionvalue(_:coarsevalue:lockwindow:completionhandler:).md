

- StoreKit
- SKAdNetwork
-  updatePostbackConversionValue(\_:coarseValue:lockWindow:completionHandler:) 

Type Method

# updatePostbackConversionValue(\_:coarseValue:lockWindow:completionHandler:)

Updates the fine and coarse conversion values and indicates whether to send the postback before the conversion window ends, and calls a completion handler if the update fails.

iOS 16.1+iPadOS 16.1+Mac Catalyst 16.1+

``` source
class func updatePostbackConversionValue(
    _ fineValue: Int,
    coarseValue: SKAdNetwork.CoarseConversionValue,
    lockWindow: Bool,
    completionHandler completion: (((any Error)?) -> Void)? = nil
)
```

``` source
class func updatePostbackConversionValue(
    _ fineValue: Int,
    coarseValue: SKAdNetwork.CoarseConversionValue,
    lockWindow: Bool
) async throws
```

## Parameters 

`fineValue`  

An unsigned 6-bit value `≥0` and `≤63`. The app or the ad network defines the meaning of the fine conversion value.

`coarseValue`  

An SKAdNetwork.CoarseConversionValue value of low, medium, or high. The app or the ad network defines the meaning of the coarse conversion value.

`lockWindow`  

A Boolean value that indicates whether to send the postback before the conversion window ends. Use `true` to tell the system to send the postback without waiting for the end of the conversion window. The default value is `false`.

`completion`  

An optional completion handler you provide to catch and handle any errors this method encounters when you update a conversion value. Set this value to `nil` if you don’t provide a handler.

## Mentioned in 

Receiving postbacks in multiple conversion windows

SKAdNetwork 4 release notes

Identifying the parameters in install-validation postbacks

Configuring an advertised app

Receiving ad attributions and postbacks

## Discussion

Call this method when the user first launches an app to register the app installation, and again to update conversion values as the user engages with the app. It’s up to your app to decide what the conversion values signify in your app, both the `fineValue` and the `coarseValue`.

This method supports ads signed with any verison of SKAdNetwork, and you can use it instead of calling updatePostbackConversionValue(_:completionHandler:) and updatePostbackConversionValue(_:coarseValue:completionHandler:). The system automatically determines the method’s behavior based on the ad’s version, as the following sections describe — the app doesn’t need to know the ad version. To take advantage of the multiple postbacks available starting in version 4, use this method or updatePostbackConversionValue(_:coarseValue:completionHandler:).

This method returns SKANError.Code.invalidConversionValue if the `fineValue` is outside of the allowed range.

Important

The system ignores calls to this method if the `fineValue` is outside of the valid range. Valid conversion updates your app sends before or after an invalid conversion remain available.

### Update conversion values for ads signed with SKAdNetwork 4 or later

For ads that ad networks sign using version 4 or later, calling this method behaves as follows:

- Both the `fineValue` and `coarseValue` represent conversion values. The method ignores the `fineValue` after the first conversion window.

- Setting the `lockWindow` parameter to `true` indicates a final update for the conversion value for the current conversion window. The system ignores additional calls to update the conversion value until the end of the conversion window.

- Setting the `lockWindow` parameter to `false` continues updating the conversion value throughout the conversion window.

For information about the data you may receive in postbacks, see Receiving postbacks in multiple conversion windows.

### Update conversion values for ads signed with SKAdNetwork 3 or earlier

For ads that ad networks sign using version 3 or earlier, calling this method behaves as follows:

- The `fineValue` represents the conversion value.

- The method ignores the `coarseValue` and `lockWindow` parameters.

- There’s a single conversion period that ends after a rolling 24-hour timer expires. The 24-hour timer restarts each time the app calls this method with a valid conversion value greater than the previous value. When the timer expires, the conversion value is final and subsequent calls to this method have no effect.

- The device sends the postback 0–24 hours after the timer expires.

- The postback contains the final conversion value only if the postback data tier contains the value.

For more information about SKAdNetwork versions, see SKAdNetwork release notes.

## See Also

### Providing conversion information

class func updatePostbackConversionValue(Int, coarseValue: SKAdNetwork.CoarseConversionValue, completionHandler: (((any Error)?) -> Void)?)

Updates the fine and coarse conversion values, and calls a completion handler if the update fails.

struct CoarseConversionValue

Coarse values to use for updating conversion values.

class func updatePostbackConversionValue(Int, completionHandler: (((any Error)?) -> Void)?)

Verifies the first launch of an advertised app and, on subsequent calls, updates the conversion value or calls a completion handler if the update fails.

