---
source_url: "https://gsap.com/docs/v3/Plugins/MotionPathPlugin/static.getGlobalMatrix()"
title: "static-getGlobalMatrix | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:19:12.728266Z"
selector: "article"
---

# static-getGlobalMatrix | GSAP | Docs & Learning

* more plugins
* [MotionPath](/docs/v3/Plugins/MotionPathPlugin)
* methods
* MotionPathPlugin.getGlobalMatrix()

On this page

# MotionPathPlugin.getGlobalMatrix

### MotionPathPlugin.getGlobalMatrix( element:Element, inverse:Boolean, adjustGOffset:Boolean ) : Matrix2D

Gets the Matrix2D that would be used to convert the element's local coordinate space into the global coordinate space. So, for example, if you take a point `{x:0, y:0}` and `apply()` the matrix to it, the resulting point would be the viewport coordinates of that element's top left corner.

#### Parameters

* #### **element**: Element

  The element whose global matrix should be returned. This should be an element reference (like myElem), not a selector string (like "#myElem").
* #### **inverse**: Boolean

  [optional] if `true`, the inverse of the matrix will be returned, meaning that it'll produce the exact opposite transformation (like calling inverse() on the matrix)
* #### **adjustGOffset**: Boolean

  [optional] if `true`, the x/y offsets of `<g>` elements will be ignored (they behave differently than most other elements).

### Returns : Matrix2D[​](#returns--matrix2d "Direct link to Returns : Matrix2D")

An object with a, b, c, d, e, and f properties just like an [SVGMatrix](https://developer.mozilla.org/en-US/docs/Web/API/SVGMatrix).

### Details[​](#details "Direct link to Details")

Gets the Matrix2D that would be used to convert the element's local coordinate space into the global coordinate space. So, for example, if you take a point `{x:0, y:0}` and apply the matrix to it, the resulting point would be the window/viewport coordinates of that element's top left corner.

## What's a Matrix2D?[​](#whats-a-matrix2d "Direct link to What's a Matrix2D?")

A Matrix2D is just an object with `a`, `b`, `c`, `d`, `e`, and `f` properties representing a 2D transformation matrix (very similar to an [SVGMatrix](https://developer.mozilla.org/en-US/docs/Web/API/SVGMatrix)). It contains all rotation, scale, skew, and x/y translation data and it's useful for converting between coordinate spaces. It has an `apply()` method that accepts a point (like `matrix.apply({x:0, y:100})`) and returns a new point with the matrix transforms applied.

## Sample code[​](#sample-code "Direct link to Sample code")

```
let matrix = MotionPathPlugin.getGlobalMatrix(element),  
  // 0,0 is the top left corner, but you can use any local coordinates.  
  localPoint = { x: 0, y: 0 },  
  // get a new point with the matrix transformations applied.  
  globalPoint = matrix.apply(localPoint);  
  
gsap.to("#dot", {  
  x: globalPoint.x,  
  y: globalPoint.y,  
  ease: "power1.inOut",  
});
```

## Demo[​](#demo "Direct link to Demo")

#### loading...