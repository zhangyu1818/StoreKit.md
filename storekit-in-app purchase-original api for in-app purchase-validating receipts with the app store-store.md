

- StoreKit
- In-App Purchase
- Original API for In-App Purchase
-  Validating receipts with the App Store 

Article

# Validating receipts with the App Store

Verify transactions with the App Store on a secure server.

## Overview

Important

The verifyReceipt endpoint is deprecated. To validate receipts on your server, follow the steps in Validating receipts on the device on your server. To validate in-app purchases on your server without using receipts, call the App Store Server API to get Apple-signed transaction and subscription information for your customers, or verify the AppTransaction and Transaction signed data that your app obtains. You can also get the same signed transaction and subscription information from the App Store Server Notifications V2.

An App Store receipt is a binary encrypted file signed with an Apple certificate. To read the contents of the encrypted file, you need to pass it through the verifyReceipt endpoint. The endpoint’s response includes a readable JSON body. Communication with the App Store is structured as JSON dictionaries, as defined in RFC 4627. Binary data is Base64-encoded, as defined in RFC 4648. Validate receipts with the App Store through a secure server. For information on establishing a secure network connection with the App Store, see Preventing Insecure Network Connections.

Warning

Don’t call the App Store server verifyReceipt endpoint from your app. You can’t build a trusted connection between a user’s device and the App Store directly because you don’t control either end of that connection, which makes it susceptible to a machine-in-the-middle attack.

### Fetch the receipt data

The app receipt is always present in the production environment on devices running macOS, iOS, and iPadOS. The app receipt is also always present in TestFlight on devices running macOS. In the sandbox environment and in StoreKit Testing in Xcode, the app receipt is present only after the tester makes the first in-app purchase. If the app calls SKReceiptRefreshRequest or restoreCompletedTransactions(), the app receipt is present only if the app has at least one in-app purchase.

To retrieve the receipt data from the app on the device, use the appStoreReceiptURL method of Bundle to locate the app’s receipt, and encode the data in Base64. Send this Base64-encoded data to your server.

- Swift
- Objective-C

```
// Get the receipt if it's available.
if let appStoreReceiptURL = Bundle.main.appStoreReceiptURL,
    FileManager.default.fileExists(atPath: appStoreReceiptURL.path) {

    do {
        let receiptData = try Data(contentsOf: appStoreReceiptURL, options: .alwaysMapped)
        print(receiptData)

        let receiptString = receiptData.base64EncodedString(options: [])

        // Read receiptData.
    }
    catch { print("Couldn't read receipt data with error: " + error.localizedDescription) }
}
```

```
/* Load the receipt from the app bundle. */
NSURL *receiptURL = [[NSBundle mainBundle] appStoreReceiptURL];
NSData *receipt = [NSData dataWithContentsOfURL:receiptURL];

if (!receipt) { 
    NSLog(@"no receipt");
    /* No local receipt -- handle the error. */ 
} else {
    /* Get the receipt in encoded format. */
    NSString *encodedReceipt = [receipt base64EncodedStringWithOptions:0];
}

/* ... Send the receipt data to your server ... */
```

### Send the receipt data to the App Store

On your server, create a JSON object with the `receipt-data`, `password`, and `exclude-old-transactions` keys detailed in requestBody.

Submit this JSON object as the payload of an HTTP POST request. Use the test environment URL `https://sandbox.itunes.apple.com/verifyReceipt` when testing your app in the sandbox and while your app is in review. Use the production URL `https://buy.itunes.apple.com/verifyReceipt` when your app is live in the App Store. For more information, see verifyReceipt.

Important

Verify your receipt first with the production URL; then verify with the sandbox URL if you receive a `21007` status code. This approach ensures you don’t have to switch between URLs while your app is in testing, in review by App Review, or live in the App Store.

### Parse the response

The App Store’s response payload is a JSON object that contains the keys and values detailed in responseBody.

The `in_app` array contains the non-consumable, non-renewing subscription, and auto-renewable subscription items that the user previously purchased. Check the values in the response for these in-app purchase types to verify transactions as needed.

For auto-renewable subscription items, parse the response to get information about the currently active subscription period. When you validate the receipt for a subscription, `latest_receipt` contains the latest encoded receipt, which is the same as the value for `receipt-data` in the request, and `latest_receipt_info` contains all the transactions for the subscription, including the initial purchase and subsequent renewals, but not including any restores.

You can use these values to check whether an auto-renewable subscription has expired. Use these values along with the expiration_intent subscription field to get the reason for expiration.

## See Also

### Related Documentation

App Store Receipts

Validate app and In-App Purchase receipts with the App Store.

Deprecated

### Purchase validation

Choosing a receipt validation technique

Select the type of receipt validation, on the device or on your server, that works for your app.

var appStoreReceiptURL: URL?

The file URL for the bundle’s App Store receipt.

class SKReceiptRefreshRequest

A request to the App Store to get the app receipt, which represents the customer’s transactions with your app.

Deprecated

