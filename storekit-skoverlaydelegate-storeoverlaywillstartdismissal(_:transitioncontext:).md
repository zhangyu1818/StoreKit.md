

- StoreKit
- SKOverlayDelegate
-  storeOverlayWillStartDismissal(\_:transitionContext:) 

Instance Method

# storeOverlayWillStartDismissal(\_:transitionContext:)

Indicates that the platform dismisses an overlay.

iOS 14.0+iPadOS 14.0+Mac Catalyst 14.0+visionOS 1.0+

``` source
optional func storeOverlayWillStartDismissal(
    _ overlay: SKOverlay,
    transitionContext: SKOverlay.TransitionContext
)
```

## Parameters 

`overlay`  

An overlay object that’s about to disappear.

`transitionContext`  

The context you can use to animate changes to UI components when the overlay disappears.

## Discussion

Use the `transitionContext` parameter to animate updates to the UI on the main thread. For example, make a UIImageView appear by animating the change of its opacity to 100%`,` as shown in the following code:

```
func storeOverlayWillStartDismissal(_ overlay: SKOverlay, transitionContext: SKOverlay.TransitionContext) {
    transitionContext.addAnimation { [self] in
        self.imageView.layer.opacity = 1
    }
}
```

## See Also

### Responding to the Overlay’s Appearance and Disappearance

func storeOverlayWillStartPresentation(SKOverlay, transitionContext: SKOverlay.TransitionContext)

Indicates that the platform presents an overlay.

func storeOverlayDidFinishPresentation(SKOverlay, transitionContext: SKOverlay.TransitionContext)

Indicates that the platform finished presenting an overlay.

func storeOverlayDidFinishDismissal(SKOverlay, transitionContext: SKOverlay.TransitionContext)

Indicates that platform finished dismissing an overlay.

class TransitionContext

A context object you can use to animate UI changes while the platform presents or dismisses an overlay.

