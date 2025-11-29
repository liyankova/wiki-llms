---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollTrigger/static.isInViewport()"
title: "static-isInViewport | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:13:40.239579Z"
selector: "article"
---

# static-isInViewport | GSAP | Docs & Learning

* [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/)
* methods
* ScrollTrigger.isInViewport()

On this page

# ScrollTrigger.isInViewport

### ScrollTrigger.isInViewport( Element:Element | String, proportion:Number, horizontal:Boolean ) : Boolean

Returns `true` if the element is in the viewport. You can optionally specify a minimum proportion, like `ScrollTrigger.isInViewport(element, 0.2)` would only return `true` if at least 20% of the element is in the viewport.

#### Parameters

* #### **Element**: Element | String

  The element or selector text
* #### **proportion**: Number

  The minimum proportion of the element that must be in the viewport to return `true`, so 0.2 would mean that at least 20% of the element must be in the viewport in order for the method to return `true`
* #### **horizontal**: Boolean

  By default, the vertical position is evaluated but to use the horizontal position instead, set the horizontal parameter to `true`

### Details[​](#details "Direct link to Details")

Returns `true` if the element is in the viewport.

```
// is any part of the element in the viewport?  
if (ScrollTrigger.isInViewport(element)) {  
  // you can use selector text  
  // do stuff  
}
```

You can optionally specify a minimum proportion, so 0.2 would only return `true` if at least 20% of the element is in the viewport:

```
// at least 20% of the element must be in the viewport for this to return true  
if (ScrollTrigger.isInViewport(element, 0.2)) {  
  // do stuff  
}
```

By default, it checks the **vertical** position but if you'd like to check the *horizontal* position instead, set the 3rd parameter to `true` like:

```
// check horizontal instead of vertical  
if (ScrollTrigger.isInViewport(element, 0.2, true)) {  
  // do stuff  
}
```

To find out the precise location of the element within the viewport, see the [ScrollTrigger.positionInViewport()](/docs/v3/Plugins/ScrollTrigger/static.positionInViewport()) method.

## Demo[​](#demo "Direct link to Demo")

#### loading...