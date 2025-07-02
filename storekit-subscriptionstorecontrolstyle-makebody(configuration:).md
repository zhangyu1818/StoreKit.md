

- StoreKit
- SubscriptionStoreControlStyle
-  makeBody(configuration:) 

Instance Method

# makeBody(configuration:)

Creates a view that represents the body of a subscription store control.

StoreKitSwiftUIiOS 17.0+iPadOS 17.0+macOS 14.0+tvOS 17.0+visionOS 1.0+watchOS 10.0+

``` source
@ViewBuilder @MainActor @preconcurrency
func makeBody(configuration: Self.Configuration) -> Self.Body
```

**Required**

## Parameters 

`configuration`  

The properties of a subscription store control that includes the list of auto-renewable subscriptions to merchandise.

## Return Value

A view which provides UI controls to subscribe to a subscription service.

## Discussion

Implement this method to define a custom subscription store control style which conforms to the SubscriptionStoreControlStyle. Use the `configuration` input — a value of SubscriptionStoreControlStyleConfiguration — to access the collection of subscription options to merchandise, and other properties of the controls. Return a view that provides controls for someone to choose an option from the configuration and subscribe. The following code example defines a style that adds price comparison captions to buttons:

```
struct PriceComparisonButtonsSubscriptionStoreControlStyle: SubscriptionStoreControlStyle {

    func makeBody(configuration: Configuration) -> some View {
        ForEach(configuration.options) { option in
            VStack {
                Button(localizedPrice(for: option), action: option.subscribe)
                if let priceComparison = priceComparison(for: option, allOptions: configuration.allOptions) {
                    Text(priceComparison)
                }
            }
        }
    }

    // Helper methods for localizing text

    private func localizedPrice(for option: Configuration.Option) -> LocalizedStringKey {
        // Use 'displayPrice' and 'subscriptionPeriod' on 'option' to localize the price.
        // For example: "$9.99/month"
    }

    private func priceComparison(for option: Configuration.Option, allOptions: [Product]) -> LocalizedStringKey? {
        guard let subscriptionPeriod = option.subscriptionPeriod, subscriptionPeriod != .monthly else {
            return nil
        }
        let monthlyOption = allOptions.first { otherOption in 
            otherOption.subscriptionPeriod == .monthly && otherOption.groupLevel == option.groupLevel
        }
        guard let monthlyOption else { 
            return nil
        }
        // Create a localized string to represent the savings of subscribing to 'option' compared to paying per
        // month with 'monthlyOption'. For example, "Save $20.00 per year compared to the monthly option".
    }
}
```

The `PriceComparisonButtonsSubscriptionStoreControlStyle` structure in the example code provides a button to subscribe to each option in the options property of the `configuration`, along with an optional informative caption for options with durations longer than one month. By calling the subscribe() method when a button is triggered, the subscription store view automatically manages a purchase task with the appropriate purchase options. The buttons automatically use the same button style as standard subscription store control styles, but you can customize this using buttonStyle(_:).

Since the control style creates a VStack for each option, the subscription store view automatically lays out the stacks appropriately. You could instead provide an explicit layout container around ForEach to customize the spacing and alignment of the buttons.

To handle cases where the monthly plans aren’t visible, the control style uses the allOptions property to compute price comparsions instead of options.

The control style reads properties of Product.SubscriptionInfo directly on the SubscriptionStoreControlStyleConfiguration.Option using dynamic member lookup, such as subscriptionPeriod.

Whenever any of the properties of `configuration` change, the system calls your makeBody(configuration:) method again to display an updated view.

The above example provides a button per plan, but not all control styles need to work this way. For example, you could combine multiple controls together with buttons, such as Picker or Toggle, and use state to implement more complicated interactions.

### Modifying subviews of standard control styles

The `PriceComparisonButtonsSubscriptionStoreControlStyle` in the example code above uses the Button type to add buttons, but you can also use the SubscriptionStoreButton view to modify the standard subscribe button. When within the scope of a type conforming to SubscriptionStoreControlStyle, you can simply spell this view as `SubscribeButton`.

For example, the following update to the `PriceComparisonButtonsSubscriptionStoreControlStyle` example code uses `SubscribeButton` instead of Button:

```
struct PriceComparisonButtonsSubscriptionStoreControlStyle: SubscriptionStoreControlStyle {

    func makeBody(configuration: Configuration) -> some View {
        ForEach(configuration.options) { option in
            VStack {
                SubscribeButton(option)
                if let priceComparison = priceComparison(for: option, allOptions: configuration.allOptions) {
                    Text(priceComparison)
                }
            }
            .subscriptionStoreButtonLabel(.price)
        }
    }

    // Helper method for localizing text     
    private func priceComparison(for option: Configuration.Option, allOptions: [Product]) -> LocalizedStringKey? {
        // Create a localized string to represent the savings of subscribing to 'option' compared to paying per
        // month with 'monthlyOption'. For example, "Save $20.00 per year compared to the monthly option".
    }
}
```

The updated custom style no longer needs to implement a custom `localizedPrice(for:)` method, instead the `SubscribeButton` automatically creates the localized label. The custom style uses the `subscriptionStoreButtonLabel(_:)` view modifier to only show the price in the button’s label.

You can also create custom control styles which modify the standard subscription picker control by using the SubscriptionStorePicker type. When within the scope of a type conforming to SubscriptionStoreControlStyle, you can simply spell this view as `SubscriptionPicker`. For example, you can create a style to modify the standard subscription picker to use a custom label for the picker options:

```
struct SimpleCustomPickerOptionLabelSubscriptionStoreControlStyle: SubscriptionStoreControlStyle {

    func makeBody(configuration: Configuration) -> some View {
        SubscriptionPicker(configuration) { option in 
            HStack {
                VStack {
                    Text(option.displayName)
                    if option.activeOffer != nil {
                        Label("Special Offer", systemImage: "star")
                            .symbolVariant(.fill)
                            .foregroundStyle(.tint)
                            .font(.caption)
                            .padding(4)
                            .background(.secondary, .rect(cornerRadius: 4)
                    }
                }
                Spacer()
                Image(systemName: "checkmark")
                    .foregroundStyle(.tint)
                    .opacity(option.isSelected ? 1.0 : 0.0)
            }
        } confirmation: { option in 
            SubscribeButton(option)
        }
    }
}
```

The `SimpleCustomPickerOptionLabelSubscriptionStoreControlStyle` in the example code provides a picker control to select a plan from the `configuration` by providing the `configuration` value to the `SubscriptionPicker` view.

The first closure provided to the subscription picker receives a SubscriptionStoreControlStyleConfiguration.PickerOption value, and returns a view to use as the label for each picker option. The subscription picker calls this closure once for each option in the configuration’s options property. The style uses the displayName property of Product via dynamic member lookup to indicate which plan the picker option corresponds to. If the subscription store is configured to merchandise an offer, the custom style shows a label by checking `offer` . The style uses the isSelected property to adjust the visibility of a checkmark indicating the selected plan. The isSelected property is available instead of subscribe() when declaring subscription picker option labels.

The second closure provided to the subscription picker receives a SubscriptionStoreControlStyleConfiguration.Option value, providing a control to confirm the currently selected plan. The custom style only provides custom picker option, and uses the standard subscribe button for the confirmation content. The standard subscribe button displays the price of the selected option.

You can also access the standard subscription picker option label by using SubscriptionStorePickerOption.

## See Also

### Creating custom subscription store control styles

typealias Configuration

The properties of a subscription store control that includes the list of auto-renewable subscriptions to merchandise.

typealias SubscribeButton

A button for subscribing to an in-app subscription.

typealias SubscriptionPicker

A composite control for selecting a subscription option and confirming the subscription.

typealias SubscriptionPickerOption

A subscription option within a subscription picker control.

struct SubscriptionStoreControlPlacementKey

A placement for a subscription store control in a store view.

associatedtype Placement : SubscriptionStoreControlPlacement = AutomaticSubscriptionStoreControlPlacement

The placement of subscription controls in a subscription store.

**Required**

associatedtype Body : View

A view that represents the body of a subscription store control.

**Required**

