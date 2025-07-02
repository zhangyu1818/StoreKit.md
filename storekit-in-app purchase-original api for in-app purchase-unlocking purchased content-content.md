

- StoreKit
- In-App Purchase
- Original API for In-App Purchase
-  Unlocking purchased content 

Article

# Unlocking purchased content

Deliver content to the customer after validating the purchase.

## Overview

After a purchase is complete, it’s your responsibility to make sure that you programmatically make the content available to the customer.

### Identify the purchased content

For an in-app purchase product that enables app functionality, such as a premium subscription, set a Boolean value to enable the code path and update your user interface as needed. Consult your app’s persistent transaction record to determine the functionality to unlock. Your app needs to update this Boolean value whenever the user completes a purchase and at app launch. For information on making a persistent record, see Persisting a purchase.

For example, using the app receipt, your code might look like the following:

- Swift
- Objective-C

```
guard let receiptURL = Bundle.main.appStoreReceiptURL else { customError() }
do {
    let receiptData = try Data(contentsOf: receiptURL)
    // Custom method to work with receipts.
    let rocketCarEnabled = receipt(receiptData, includesProductID: "com.example.rocketCar")
    } catch {
        print(error)
    }
```

```
NSURL *receiptURL = [[NSBundle mainBundle] appStoreReceiptURL];
NSData *receiptData = [NSData dataWithContentsOfURL:receiptURL];

// Custom method to work with receipts.
BOOL rocketCarEnabled = [self receipt:receiptData
        includesProductID:@"com.example.rocketCar"];
```

Or, using the user defaults system.

- Swift
- Objective-C

```
let defaults = UserDefaults.standard
let rocketCarEnabled = defaults.bool(forKey: "enable_rocket_car")
```

```
NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
BOOL rocketCarEnabled = [defaults boolForKey:@"enable_rocket_car"];

```

After you define the Boolean variable that represents the in-app purchase content, use the purchase information to enable the appropriate code paths in your app.

```
if (rocketCarEnabled) {
    // Use the rocket car.
} else {
    // Use the regular car.
}
```

### Deliver associated content

Your app needs to deliver any content associated with the purchased product to the user. For example, purchasing instruments in a music app requires delivering the sound files needed to let the user play those instruments. You can embed that content in your app bundle or download it as necessary. Each approach has its advantages and disadvantages.

Embed smaller files (up to a few megabytes) in your app, especially if you expect most users to buy that product. You can make the content in your app bundle available immediately after the user purchases it. However, to add or update content in your app bundle, you need to submit an updated version of your app.

Download larger files only when needed. Separating content from your app bundle keeps your app’s initial download small. For example, a game can include the first level in its app bundle and let users download additional levels as they purchase them. Assuming your app fetches its list of product identifiers from your server and the information isn’t hard-coded in the app bundle, you don’t need to resubmit your app to add or update content that your app downloads.

Note

You can’t patch your app binary or download executable code. Your app needs to contain all executable code necessary to support all of its functionality when you submit it. If a new product requires code changes, submit an updated version of your app.

### Load local content

Load local content using the `NSBundle` class as you load other resources from your app bundle.

- Swift
- Objective-C

```
guard let url = Bundle.main.url(forResource: "rocketCar", withExtension: "plist") else { fatalError() }
loadVehicle(at: url)
```

```
NSURL *url = [[NSBundle mainBundle] URLForResource:@"rocketCar"
                                     withExtension:@"plist"];
[self loadVehicleAtURL:url];

```

### Download content from your own server

As with all interactions between your app and your server, the details and process of downloading content from your own server are your responsibility. The communication consists of, at a minimum, the following steps:

1.  Your app sends the receipt to your server and requests the content.

2.  Your server validates the receipt to establish that the user purchased the content, as described in Validating receipts with the App Store.

3.  Assuming the receipt is valid, your server responds to your app with the content.

Ensure that your app handles errors gracefully. For example, if the device runs out of disk space during a download, give the user the option to discard the partial download or to resume the download later when space becomes available.

Consider the security implications of how you host your content and how your app communicates with your server. For more information, see Security Overview.

### Download content using on-demand resources

You can use On-Demand Resources (ODR) for flexibility in downloading data in your app. ODR is an Apple-hosted service you use to store in-app purchase data that your app downloads after you verify the user’s purchase using the app receipt. ODR doesn’t require a call to restore transactions and authenticate the user to download content hosted on Apple’s server.

### Download hosted content from Apple’s server

Important

SKDownload and its related functionality are deprecated. The following information is for apps that already host content on Apple’s servers and use SKDownload.

Apps can use Apple-hosted content for downloaded files. You create an Apple-hosted content bundle using the In-App Purchase Content target in Xcode and submit it to App Store Connect. Apple’s servers store your app’s content using the same infrastructure that supports other large-scale operations, such as the App Store. Apple-hosted content automatically downloads in the background even if your app isn’t running.

If you need to support older versions of iOS or share your server infrastructure across multiple platforms, you may choose to host your own content using your own server infrastructure.

When the user purchases a product that has associated Apple-hosted content, the transaction that passes to your transaction queue observer also includes an instance of SKDownload that lets you download the associated content.

To download the content, add the download objects from the transaction’s downloads property to the transaction queue by calling the start(_:) method of SKPaymentQueue. If the value of the `downloads` property is `nil`, there’s no Apple-hosted content for that transaction. Unlike downloading apps, downloading content doesn’t automatically require a Wi-Fi connection for content larger than a certain size. Avoid using cellular networks to download large files without an explicit action from the user.

Implement the paymentQueue(_:updatedDownloads:) method on the transaction queue observer to respond to changes in a download’s state, such as by updating progress in your UI. If a download fails, use the information in its error property to present the error to the user.

Ensure that your app handles errors gracefully. For example, if the device runs out of disk space during a download, give the user the option to discard the partial download or to resume the download later when space becomes available.

While the content is downloading, update your user interface using the values of the progress and timeRemaining properties. You can use the pause(_:), resume(_:), and cancel(_:) methods of `SKPaymentQueue` from your UI to let the user control in-progress downloads. Use the downloadState property to determine whether the download completes. Don’t use the progress or timeRemaining property of the download object to check its status; these properties are for updating your UI.

Note

Download all Apple-hosted content before finishing the transaction. After a transaction is complete, its download objects become unusable.

In iOS, your app can manage the downloaded files. The StoreKit framework saves these files for you in the `Caches` directory with the backup flag unset. After the download completes, your app is responsible for moving these files to the appropriate location. For content that can be deleted if the device runs out of disk space (and downloaded again later by your app), keep the files in the `Caches` directory. Otherwise, move the files to the `Documents` folder and set the flag to exclude them from user backups.

- Swift
- Objective-C

```
// This is the URL for downloaded content.
guard var url = download.contentURL else { fatalError() }

var resourceValues = URLResourceValues()
resourceValues.isExcludedFromBackup = true

do {
    try url.setResourceValues(resourceValues)
} catch {
    print(error)
}
```

```
NSError *error;
BOOL success = [URL setResourceValue:[NSNumber numberWithBool:YES]
                              forKey:NSURLIsExcludedFromBackupKey
                               error:&error];
if (!success) { /* Handle error... */ }
```

In macOS, the system manages the downloaded files; your app can’t move or delete them directly. To locate the content after downloading it, use the contentURL property of the download object. To locate the file on subsequent launches, use the contentURL(forProductID:) class method of `SKDownload`. To delete a file, use the deleteContent(forProductID:) class method. For information about reading the app receipt, see Validating receipts with the App Store.

## See Also

### Content delivery

Persisting a purchase

Keep a persistent record of a purchase to continue making the product available as needed.

Finishing a transaction

Finish the transaction to complete the purchase process.

class SKDownload

Downloadable content associated with a product.

Deprecated

