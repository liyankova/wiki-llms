---
source_url: "https://gsap.com/docs/v3/Plugins/Draggable/applyBounds()"
title: "applyBounds | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:17:54.260839Z"
selector: "article"
---

# applyBounds | GSAP | Docs & Learning

* more plugins
* [Draggable](/docs/v3/Plugins/Draggable/)
* methods
* .applyBounds()

On this page

# applyBounds

### applyBounds( bounds:Element | String | Object ) ;

Applies new bounds to the Draggable.

#### Parameters

* #### **bounds**: Element | String | Object

  The bounds to restrict the Draggable to. It could be an element reference, selector text, or an object with the values {top: 100, left: 0, width: 1000, height: 800} or {minX: 10, maxX: 300, minY: 50, maxY: 500} or {minRotation: 0, maxRotation: 270}.

### Details[​](#details "Direct link to Details")

Applies new bounds to the Draggable.

The bounds could be another another DOM element (like a container) using an element reference (like document.getElementById("container")) or selector text (like `"#container"`), rectangle coordinates (like `{top: 100, left: 0, width: 1000, height: 800}` which is based on the parent's coordinate system where top and left would be from the upper left corner of the parent), or specific maximum and minimum values like `{minX: 10, maxX: 300, minY: 50, maxY: 500}` or `{minRotation: 0, maxRotation: 270}`.