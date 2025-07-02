

- StoreKit
- In-App Purchase
- Original API for In-App Purchase
-  Persisting a purchase 

Article

# Persisting a purchase

Keep a persistent record of a purchase to continue making the product available as needed.

## Overview

After making a product available, your app needs to make a persistent record of the purchase. Your app uses that persistent record to continue making the product available on launch and to restore purchases. Your app’s persistence strategy depends on the type of products you sell:

- For non-consumable products and auto-renewable subscriptions, use the app receipt as your persistent record. If the app receipt isn’t available, use the user defaults system or iCloud to keep a persistent record.

- For non-renewing subscriptions, use iCloud or your own server to keep a persistent record.

- For consumable products, your app updates its internal state to reflect the purchase. Ensure that the updated state is part of an object that supports state preservation (in iOS) or that you manually preserve the state across app launches (in iOS or macOS).

When using the user defaults system or iCloud, your app can store a value, such as a number or Boolean value, or a copy of the transaction receipt. In macOS, users can edit the user defaults system using the `defaults` command. Storing a receipt requires more application logic, but protects the persistent record from tampering.

Note

When persisting with iCloud, your app’s persistent record syncs across devices, but your app is responsible for downloading any associated content on other devices.

### Persist purchases using the app receipt

The app receipt contains a record of the user’s purchases, cryptographically signed by Apple. For more information, see Choosing a receipt validation technique.

The system adds information about consumable products to the receipt when the user purchases them, and it remains in the receipt until you finish the transaction. After you finish the transaction, the system removes this information the next time it updates the receipt, such as the next time the user makes a purchase.

The system adds information about all other kinds of purchases to the receipt when the user purchases the products, and it remains in the receipt indefinitely.

### Persist a value in user defaults or iCloud

To store information in user defaults or iCloud, set the value for a key.

- Swift
- Objective-C

```
#if USE_ICLOUD_STORAGE
let storage = NSUbiquitousKeyValueStore.default
#else
let storage = UserDefaults.standard
#endif

storage.set(true, forKey: "enable_rocket_car")
storage.set(highestUnlockedLevel, forKey: "highest_unlocked_level")

```

```
#if USE_ICLOUD_STORAGE
NSUbiquitousKeyValueStore *storage = [NSUbiquitousKeyValueStore defaultStore];
#else
NSUserDefaults *storage = [NSUserDefaults standardUserDefaults];
#endif

[storage setBool:YES forKey:@"enable_rocket_car"];
[storage setObject:@15 forKey:@"highest_unlocked_level"];
```

### Persist purchases using your own server

Send a copy of the receipt to your server, along with credentials or an identifier, so you can keep track of which receipts belong to a particular user. For example, let users identify themselves to your server with a user name and password. Don’t use the identifierForVendor property of UIDevice. Different devices have different values for this property, so you can’t use it to identify and restore purchases that the same user makes on a different device.

## See Also

### Content delivery

Unlocking purchased content

Deliver content to the customer after validating the purchase.

Finishing a transaction

Finish the transaction to complete the purchase process.

class SKDownload

Downloadable content associated with a product.

Deprecated

