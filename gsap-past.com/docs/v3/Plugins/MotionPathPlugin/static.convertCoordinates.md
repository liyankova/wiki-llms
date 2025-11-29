---
source_url: "https://gsap.com/docs/v3/Plugins/MotionPathPlugin/static.convertCoordinates()"
title: "static-convertCoordinates | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:19:05.873306Z"
selector: "article"
---

# static-convertCoordinates | GSAP | Docs & Learning

* more plugins
* [MotionPath](/docs/v3/Plugins/MotionPathPlugin)
* methods
* MotionPathPlugin.convertCoordinates()

On this page

# MotionPathPlugin.convertCoordinates

### MotionPathPlugin.convertCoordinates( fromElement:Element | window, toElement:Element | window, point:Object ) : Object (point or Matrix2D)

Converts a point from one element's local coordinates into where that point lines up in a different element's local coordinate system regardless of how many nested transforms are affecting the elements!

#### Parameters

* #### **fromElement**: Element | window

  The element whose local coordinates serve as the **input**. The `point` (3rd parameter) is defined according to this element's local coordinates.
* #### **toElement**: Element | window

  The element whose local coordinates serve as the **output**. In other words, the `point` will be converted into this element's local coordinate system. This should be an element reference (like myElem), not a selector string
* #### **point**: Object

  [optional] An object with x and y properties like `{x:100, y:200}` that define the local coordinates in the `fromElement` that should be converted into the `toElement`'s local coordinates.

### Returns : Object (point or Matrix2D)[​](#returns--object-point-or-matrix2d "Direct link to Returns : Object (point or Matrix2D)")

If a `point` parameter is provided, it will be converted and a new point is returned like `{x: 100, y: 200}` representing the converted coordinates in the `toElement`. If no `point` is provided, a **Matrix2D** object is returned so that you can use it to quickly convert ANY coordinates using its `apply()` method.

### Details[​](#details "Direct link to Details")

Converts a point from one element's local coordinates into where that point lines up in a different element's local coordinate system regardless of how many nested transforms are affecting the elements! For example, if an element is rotated and scaled inside a transformed container and the user clicks on it, you could convert the event's pageX and pageY coordinates into where that is in that nested element's coordinate system.

## Sample code[​](#sample-code "Direct link to Sample code")

```
let fromElement = document.querySelector("#from"),  
  toElement = document.querySelector("#to"),  
  point = { x: 100, y: 0 },  
  convertedPoint = MotionPathPlugin.convertCoordinates(  
    fromElement,  
    toElement,  
    point  
  );  
  
// or if you want to convert multiple points, don't pass one to the function and it'll return a Matrix2D  
let matrix = MotionPathPlugin.convertCoordinates(fromElement, toElement), // no point parameter!  
  p1 = matrix.apply({ x: 100, y: 0 }),  
  p2 = matrix.apply({ x: 0, y: 200 }),  
  p3 = matrix.apply({ x: 50, y: 50 });
```

## Video[​](#video "Direct link to Video")

## Demo[​](#demo "Direct link to Demo")

#### loading...