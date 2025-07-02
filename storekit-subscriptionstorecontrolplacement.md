

- StoreKit
-  SubscriptionStoreControlPlacement 

Protocol

# SubscriptionStoreControlPlacement

A type that specifies the placement of a subscription control in a subscription store view.

StoreKitSwiftUIiOS 18.0+iPadOS 18.0+macOS 15.0+tvOS 18.0+visionOS 2.0+watchOS 11.0+

``` source
protocol SubscriptionStoreControlPlacement : RawRepresentable where Self.RawValue == SubscriptionStoreControlPlacementKey
```

## Overview

A placement indicates a position for placing a control in a view. Specifically, a subscription store control placement indicates a postion for placing a subscription control in a subscription store view. You typically don’t need to implement your own control placement; instead, use the conforming placement types. To see the available control placements for a type, such as a PagedPickerSubscriptionStoreControlStyle, check the `Placement` associated type on a control style.

Not all subscription store control styles support all placements. For example, the picker control styles don’t support the bottom bar placement because the height obscures the scroll view.

## Topics

### Getting a placement

static var automatic: Self

The default placement for a subscription store control.

**Required**

### Placement types

struct AutomaticSubscriptionStoreControlStyle

The default in-app subscription store control style that resolves its appearance based on the view’s context.

struct ButtonsSubscriptionStoreControlStyle

A subscription store control style that displays a subscribe button for each subscription plan.

struct PickerSubscriptionStoreControlStyle

A subscription store control style that displays subscription plans as a picker control, with a single button to subscribe.

struct CompactPickerSubscriptionStoreControlStyle

A subscription store control style that displays subscription plans as a compact picker control, with a single button to subscribe.

struct PagedPickerSubscriptionStoreControlStyle

A subscription store control style that displays subscription plans as a paged picker control, with a single button to subscribe.

## Relationships

### Inherits From

- RawRepresentable

### Conforming Types

- AutomaticSubscriptionStoreControlPlacement
- CompactPickerSubscriptionStoreControlStyle.Placement
- PagedPickerSubscriptionStoreControlStyle.Placement

## See Also

### Styling subscription store controls

nonisolated func subscriptionStoreControlStyle(_ style: some SubscriptionStoreControlStyle) -> some View 

Sets the control style for subscription store views within a view.

nonisolated func subscriptionStoreControlStyle&lt;S>(_ style: S, placement: S.Placement) -> some View where S : SubscriptionStoreControlStyle 

Sets the control style and control placement for subscription store views within a view.

protocol SubscriptionStoreControlStyle

A type that specifies the appearance and interaction of controls in the subscription store view instances within the view hierarchy.

struct SubscriptionStoreControlStyleConfiguration

The properties of a subscription store control that includes the list of auto-renewable subscriptions to merchandise.

