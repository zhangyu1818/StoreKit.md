

- StoreKit
- Product
- Product.SubscriptionPeriod
-  dateRange(referenceDate:) 

Instance Method

# dateRange(referenceDate:)

The calculated date range of a subscription period, starting at the reference date.

iOS 15.0+iPadOS 15.0+Mac Catalyst 15.0+macOS 12.0+tvOS 15.0+visionOS 1.0+watchOS 8.0+

``` source
@backDeployed(before: iOS 16.0, macOS 13.0, tvOS 16.0, watchOS 9.0, macCatalyst 16.0)
func dateRange(referenceDate: Date = .now) -> Range
```

## Parameters 

`referenceDate`  

A date you provide that indicates the lower bound of the returned date range. The default value is now.

## Return Value

The subscription period represented by two dates that are the lower bound and upper bound of the subscription period of the Product.SubscriptionPeriod instance.

## Discussion

The date range calculates a single subscription period starting from the date you provide in `referenceDate`.

For example, if the subscription period of the Product.SubscriptionPeriod instance is one month, and the `referenceDate` is February 1, the date range contains February 1 and March 1. If the `referenceDate` is Feb 15, the date range contains February 15 and March 15.

Use the dateRange(referenceDate:) with a Date.ComponentsFormatStyle to get a human-readable string representation of the subscription period.

Get the format style (Date.ComponentsFormatStyle) corresponding to product’s storefront using the subscriptionPeriodFormatStyle.

