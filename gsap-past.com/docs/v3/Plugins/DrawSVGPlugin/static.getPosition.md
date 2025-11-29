---
source_url: "https://gsap.com/docs/v3/Plugins/DrawSVGPlugin/static.getPosition()"
title: "static-getPosition | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:19:01.039115Z"
selector: "article"
---

# static-getPosition | GSAP | Docs & Learning

* more plugins
* [DrawSVG](/docs/v3/Plugins/DrawSVGPlugin)
* methods
* DrawSVGPlugin.getPosition()

On this page

# DrawSVGPlugin.getPosition

### DrawSVGPlugin.getPosition( element:[Element | Selector text] ) : Number

Provides an easy way to get the current position of the DrawSVG.

#### Parameters

* #### **element**: [Element | Selector text]

  The element (or the selector text for the element) whose position you'd like to get.

### Returns : Number[​](#returns--number "Direct link to Returns : Number")

The position of an SVG element's stroke.

### Details[​](#details "Direct link to Details")

Provides an easy way to get the position of an SVG element's stroke including: `<path>`, `<rect>`, `<circle>`, `<ellipse>`, `<line>`, `<polyline>`, and `<polygon>`.

When combined with the length (obtained using `DrawSVGPlugin.getLength`), you can calculate the total percentage at any given moment like so:

```
function getPercentage(element) {  
  return Math.floor(  
    DrawSVGPlugin.getPosition(element)[1] /  
      (DrawSVGPlugin.getLength(element) / 100)  
  );  
}
```