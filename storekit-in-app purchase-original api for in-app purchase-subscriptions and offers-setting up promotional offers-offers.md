

- StoreKit
- In-App Purchase
- Original API for In-App Purchase
- Subscriptions and offers
-  Setting up promotional offers 

Article

# Setting up promotional offers

Generate a key and configure offers for auto-renewable subscriptions in App Store Connect.

## Overview

You can offer a discounted or free period of service for auto-renewable subscription products on macOS, iOS, and tvOS using promotional offers. Limited-time, discounted promotional offers can be effective in winning back lapsed subscribers or retaining current subscribers.

Before you can provide promotional offers in your app, you must first generate a subscription key and set up the offers in your App Store Connect account.

Note

If your goal is to attract new users, use introductory offers and promote the in-app purchase on the App Store. Redeeming an introductory offer doesn’t affect a user’s eligibility for a promotional offer. For more information, see Implementing introductory offers in your app.

### Generate a Private Key

You generate a private key in App Store Connect that you use on your server to sign promotional offers. This key allows Apple to authenticate and validate subscription requests.

Keys don’t expire, and you can use them with any apps in your account. To get started, generate a subscriptions access key in App Store Connect.

#### Download and Store the Private Key

Once you’ve generated your subscription key, you’re given the opportunity to download the private half of the key. You can only download this key one time.

The keys are provided in base64-encoded PEM format. Apple doesn’t keep a copy of the private key.

Important

Store your private subscription key in a safe place. You should never share your keys, store keys in a code repository, or include keys in apps or client-side code.

If the key becomes lost or compromised, revoke it immediately and update your promotional offers. See Revoke a subscription key for more information.

### Configure Promotional Offers

You configure promotional offers in App Store Connect, providing details such as a reference name, payment mode, duration, and price. To configure your offer, see Set up promotional offers for auto-renewable subscriptions. You can have up to 10 promotional offers active at any given time per subscription.

For business guidance on using promotional offers, see Auto-renewable Subscriptions > Providing Subscription Offers.

## See Also

### Promotional offers

Implementing promotional offers in your app

Offer discounted pricing for auto-renewable subscription products to eligible subscribers.

Generating a signature for promotional offers

Create a signature to validate a promotional offer using your private key.

Generating a Promotional Offer Signature on the Server

Generate a signature using your private key and lightweight cryptography libraries.

class SKPaymentDiscount

The signed discount to apply to a payment.

Deprecated

