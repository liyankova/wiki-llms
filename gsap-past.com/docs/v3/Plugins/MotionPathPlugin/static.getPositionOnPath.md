---
source_url: "https://gsap.com/docs/v3/Plugins/MotionPathPlugin/static.getPositionOnPath()"
title: "static-getPositionOnPath | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:19:17.167615Z"
selector: "article"
---

# static-getPositionOnPath | GSAP | Docs & Learning

* more plugins
* [MotionPath](/docs/v3/Plugins/MotionPathPlugin)
* methods
* MotionPathPlugin.getPositionOnPath()

On this page

# MotionPathPlugin.getPositionOnPath

### MotionPathPlugin.getPositionOnPath( rawPath:Array, progress:Number, includeAngle:Boolean ) : Object

Calculates the x/y position (and optionally the angle) corresponding to a particular progress value along the RawPath

#### Parameters

* #### **rawPath**: Array

  The RawPath Array on which you'd like to plot a position
* #### **progress**: Number

  A number between 0 and 1 representing the progress along the path where 0.5 would be halfway into the path
* #### **includeAngle**: Boolean

  [optional] If `true`, the angle (in degrees) will also be calculated and attached to the return object as an "angle" property.

### Returns : Object[​](#returns--object "Direct link to Returns : Object")

An object containing `x` and `y` properties (coordinates) and if the `includeAngle` parameter was `true`, an `angle` property as well (in degrees)

### Details[​](#details "Direct link to Details")

Calculates the x/y position (and optionally the angle) corresponding to a particular progress value (0-1 where 0.5 is the middle) along the RawPath. Note that the RawPath must have had its measurements cached FIRST, using the cacheRawPathMeasurements() method.

## Sample code[​](#sample-code "Direct link to Sample code")

```
// Get the RawPath associated with the`<path>`with an ID of "path"  
let rawPath = MotionPathPlugin.getRawPath("#path"),  
    point;  
  
// cache the measurements first (only necessary once, unless the path data changes)  
MotionPathPlugin.cacheRawPathMeasurements(rawPath);  
  
// find the coordinates and angle of the middle of the path  
point = MotionPathPlugin.getPositionOnPath(rawPath, 0.5, true);  
  
// move a #dot element there...  
gsap.to("#dot", {  
	x: point.x,  
	y: point.y,  
	rotation: point.angle  
});  
```
```