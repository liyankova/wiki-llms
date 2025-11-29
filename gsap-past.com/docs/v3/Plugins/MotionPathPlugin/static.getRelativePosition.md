---
source_url: "https://gsap.com/docs/v3/Plugins/MotionPathPlugin/static.getRelativePosition()"
title: "static-getRelativePosition | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:19:22.254129Z"
selector: "article"
---

# static-getRelativePosition | GSAP | Docs & Learning

* more plugins
* [MotionPath](/docs/v3/Plugins/MotionPathPlugin)
* methods
* MotionPathPlugin.getRelativePosition()

On this page

# MotionPathPlugin.getRelativePosition

### MotionPathPlugin.getRelativePosition( fromElement:Element | window, toElement:Element | window, fromOrigin:Array | Object, toOrigin:Array | Object | String ) : Object

Gets the x and y distances between two elements regardless of nested transforms! feed two elements to this method and it'll return the gap between them as a point {x, y} according to the coordinate system of the fromElement's parent.

#### Parameters

* #### **fromElement**: Element | window

  The element from which the distance is measured (typically this is the element that will be moved to the `toElement`)
* #### **toElement**: Element | window

  The destination element. This should be an element reference (like myElem), not a selector string (like "#myElem").
* #### **fromOrigin**: Array | Object

  [optional] Determines the point on the `fromElement` that serves as the origin of the measurements. It can be either an Array with progress values along the x and y axis like `[0.5, 0.5]` (center), `[1, 0]` (top right corner), etc. OR a point Object with pixel-based local coordinates like `{x: 100, y: 0}`
* #### **toOrigin**: Array | Object | String

  [optional] Determines the point on the `toElement` to which to measure. It can be either an Array with progress values along the x and y axis like `[0.5, 0.5]` (center), `[1, 0]` (top right corner), etc. OR a point Object with pixel-based local coordinates like `{x: 100, y: 0}` OR for If the toElement is a <path> you can use `"auto"` to align with the beginning of the path itself rather than using the bounding box.

### Returns : Object[​](#returns--object "Direct link to Returns : Object")

An object with "x" and "y" properties describing the distance along each axis

### Details[​](#details "Direct link to Details")

Gets the x and y distances between two elements regardless of nested transforms! feed two elements to this method and it'll return the gap between them as a point `{x, y}` according to the coordinate system of the fromElement's parent. By default, it will align their top left corners (bounding box), but you can define a different origin for each, like `[0.5,&#xA0;0.5]` would be the center, `[1,&#xA0;1]` would be the bottom right, etc.

## Sample code[​](#sample-code "Direct link to Sample code")

```
let inner = document.querySelector("#inner"),  
  dot = document.querySelector("#dot"),  
  delta = MotionPathPlugin.getRelativePosition(  
    dot,  
    inner,  
    [0.5, 0.5],  
    [0.5, 0.5]  
  );  
gsap.to(dot, {  
  x: "+=" + delta.x,  
  y: "+=" + delta.y,  
  duration: 2,  
  ease: "power2.inOut",  
});
```

## Video[​](#video "Direct link to Video")

## Demo 1[​](#demo-1 "Direct link to Demo 1")

#### loading...

## Demo 2[​](#demo-2 "Direct link to Demo 2")

You can also localize the pointer coordinates, like in the below demo (click anywhere)

#### loading...

getRelativePosition()` was added in GSAP 3.2.0