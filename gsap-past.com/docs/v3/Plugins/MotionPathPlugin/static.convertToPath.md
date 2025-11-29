---
source_url: "https://gsap.com/docs/v3/Plugins/MotionPathPlugin/static.convertToPath()"
title: "static-convertToPath | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:19:08.188169Z"
selector: "article"
---

# static-convertToPath | GSAP | Docs & Learning

* more plugins
* [MotionPath](/docs/v3/Plugins/MotionPathPlugin)
* methods
* MotionPathPlugin.convertToPath()

On this page

# MotionPathPlugin.convertToPath

### MotionPathPlugin.convertToPath( shape:String | Element, swap:Boolean ) : Array

Converts SVG shapes like `<circle>`, `<rect>`, `<ellipse>`, or `<line>` into `<path>`

#### Parameters

* #### **shape**: String | Element

  Selector text or Element reference that should be converted
* #### **swap**: Boolean

  By default, the resulting <path> will be swapped directly into the DOM in place of the provided shape element, but you can define `false` for `swap` to prevent that.

### Returns : Array[​](#returns--array "Direct link to Returns : Array")

An Array of the resulting `<path>` elements

### Details[​](#details "Direct link to Details")

Identical to the [`MorphSVGPlugin.convertToPath()`](/docs/v3/Plugins/MorphSVGPlugin/static.convertToPath) method. Please see the corresponding MorphSVG [documentation for that method](/docs/v3/Plugins/MorphSVGPlugin/static.convertToPath) (includes a video).