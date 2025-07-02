

- StoreKit
-  StoreButtonKind 

Structure

# StoreButtonKind

A button to display in a store view or subscription store view.

StoreKitSwiftUIiOS 17.0+iPadOS 17.0+macOS 14.0+tvOS 17.0+visionOS 1.0+watchOS 10.0+

``` source
struct StoreButtonKind
```

## Overview

Use the storeButton(_:for:) modifier on a view to set the visibility of the buttons.

## Topics

### Getting button types for store views

static var cancellation: StoreButtonKind

A type of button that people use to dismiss the current store presentation.

static var restorePurchases: StoreButtonKind

A type of button that people use to restore purchases.

### Getting additional button types for subscription store views

static var signIn: StoreButtonKind

A type of button that people use to sign in.

static var redeemCode: StoreButtonKind

A type of button that people use to redeem an offer code.

static var policies: StoreButtonKind

A type of button that people use to display store policies.

## See Also

### Configuring accessory buttons

nonisolated func storeButton(_ visibility: Visibility, for buttonKinds: StoreButtonKind...) -> some View 

Specifies the visibility of auxiliary buttons that store view and subscription store view instances may use.

nonisolated func subscriptionStoreSignInAction(_ action: (() -> ())?) -> some View 

Adds an action to perform when a person uses the sign-in button on a subscription store view within a view.

