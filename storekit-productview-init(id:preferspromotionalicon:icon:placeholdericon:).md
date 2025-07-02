

- StoreKit
- ProductView
-  init(id:prefersPromotionalIcon:icon:placeholderIcon:) 

Initializer

# init(id:prefersPromotionalIcon:icon:placeholderIcon:)

Creates a view to load an individual product from the App Store and merchandise it using an image and a custom placeholder icon.

StoreKitSwiftUIiOS 17.0+iPadOS 17.0+macOS 14.0+tvOS 17.0+visionOS 1.0+watchOS 10.0+

``` source
nonisolated
init(
    id productID: Product.ID,
    prefersPromotionalIcon: Bool = false,
    @ViewBuilder icon: () -> Icon,
    @ViewBuilder placeholderIcon: () -> PlaceholderIcon
)
```

## Parameters 

`productID`  

The product identifier to load from the App Store.

`prefersPromotionalIcon`  

A Boolean value that indicates whether to use the promotional image from the App Store, if it’s available. If this value is `true` and a promotional image for the product is available, the view displays it instead of the view you provide in the `icon` parameter.

`icon`  

A closure that returns the image the view displays when the system successfully finishes loading the product from the App Store.

`placeholderIcon`  

A closure that returns the image that the view uses while the system loads the product from the App Store.

## Discussion

The product view displays the custom `placeholderIcon` until the system finishes loading the product. After the product loads, the system uses the view you provide in the `icon` parameter by default. If `prefersPromotionalIcon` is `true` and the product has a promotional image, the view displays the promotional image as its image instead of the view that `icon` provides.

The following code example shows how to create a product view using the `icon` and a custom `placeholderIcon`:

```
ProductView(id: "com.example.product") {
    Image(systemName: "star.fill")
        .foregroundStyle(.yellow)
} placeholderIcon: {
    Image(systemName: "star.fill")
        .foregroundStyle(.gray)
}
```

Tip

To gain more control over the image that decorates this view, use the init(id:icon:placeholderIcon:) initializer. It receives a ProductIconPhase, which enables you to supply an image for each phase of the image-loading process.

## See Also

### Creating product views that load products

init(id: Product.ID, prefersPromotionalIcon: Bool)

Creates a view to load and merchandise an individual product from the App Store.

init(id: Product.ID, prefersPromotionalIcon: Bool, icon: () -> Icon)

Creates a view to load an individual product from the App Store and merchandise it using a custom icon.

init(id: Product.ID, icon: (ProductIconPhase) -> Icon, placeholderIcon: () -> PlaceholderIcon)

Creates a view to load an individual product from the App Store, and merchandise it using its promotional image and a custom placeholder icon.

