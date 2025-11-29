---
source_url: "https://gsap.com/docs/v3/Plugins/MotionPathPlugin/static.getAlignMatrix()"
title: "static-getAlignMatrix | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:19:10.338260Z"
selector: "article"
---

# static-getAlignMatrix | GSAP | Docs & Learning

* more plugins
* [MotionPath](/docs/v3/Plugins/MotionPathPlugin)
* methods
* MotionPathPlugin.getAlignMatrix()

On this page

# MotionPathPlugin.getAlignMatrix

### MotionPathPlugin.getAlignMatrix( fromElement:Element | window, toElement:Element | window, fromOrigin:Array, toOrigin:Array | String ) : Matrix2D

Gets a Matrix2D for translating between coordinate spaces, typically so that you can move the `fromElement` to align it with the `toElement` while factoring in all transforms (even nested ones). The matrix allows you to convert any point/coordinate using its apply() method.

#### Parameters

* #### **fromElement**: Element | window

  The element that serves as the basis for the alignment matrix. Typically this is the element that will be moved to the `toElement` using the resulting matrix.
* #### **toElement**: Element | window

  The element that the `fromElement` should be aligned with
* #### **fromOrigin**: Array

  [optional] Determines the point on the `fromElement` that gets aligned. It can be either an Array with progress values along the x and y axis like `[0.5, 0.5]` (center), `[1, 0]` (top right corner), etc. OR a point Object with pixel-based local coordinates like `{x: 100, y: 0}`
* #### **toOrigin**: Array | String

  [optional] Determines the point on the `toElement` that gets aligned. It can be either an Array with progress values along the x and y axis like `[0.5, 0.5]` (center), `[1, 0]` (top right corner), etc. OR a point Object with pixel-based local coordinates like `{x: 100, y: 0}` OR for If the toElement is a <path> you can use `"auto"` to align with the beginning of the path itself rather than using the bounding box.

### Returns : Matrix2D[​](#returns--matrix2d "Direct link to Returns : Matrix2D")

An object with a, b, c, d, e, and f properties just like an [SVGMatrix](https://developer.mozilla.org/en-US/docs/Web/API/SVGMatrix).

### Details[​](#details "Direct link to Details")

Gets a Matrix2D for translating between coordinate spaces, typically so that you can move the `fromElement` to align it with the `toElement` while factoring in all transforms (even nested ones). The matrix allows you to convert any point/coordinate using its `apply()` method. For example, you can get a matrix that aligns the top left corner of #div1 with the top left corner of #div2 (regardless of nested transforms) and then to plot where 200px over and 100px down (in #div2's coordinate space) corresponds to #div1's coordinates, you could `matrix.apply({x:200, y:100})`.

## What's a Matrix2D?[​](#whats-a-matrix2d "Direct link to What's a Matrix2D?")

A Matrix2D is just an object with `a`, `b`, `c`, `d`, `e`, and `f` properties representing a 2D transformation matrix (very similar to an [SVGMatrix](https://developer.mozilla.org/en-US/docs/Web/API/SVGMatrix)). It contains all rotation, scale, skew, and x/y translation data and it's useful for converting between coordinate spaces. It has an `apply()` method that accepts a point (like `matrix.apply({x:0, y:100})`) and returns a new point with the matrix transforms applied.

## Sample code[​](#sample-code "Direct link to Sample code")

```
// get a matrix for aligning the center of the dot element with the top left corner of the dragme element (which will be treated as 0,0)  
let matrix = MotionPathPlugin.getAlignMatrix(dot, dragme, [0.5, 0.5], [0, 0]),  
  // 0,0 is the origin of the alignment (the top left corner in this case), but try any local coordinates.  
  dragmePoint = { x: 0, y: 0 },  
  // convert into the dot's coordinate space (technically its parentNode's)  
  dotPoint = matrix.apply(dragmePoint);  
  
gsap.to(dot, {  
  // if there were already transforms applied, those would affect the matrix, so we should treat them as relative.  
  x: "+=" + dotPoint.x,  
  y: "+=" + dotPoint.y,  
  ease: "power1.inOut",  
});
```

## Demo[​](#demo "Direct link to Demo")

#### loading...

`getAlignMatrix()` was added in GSAP 3.2.0