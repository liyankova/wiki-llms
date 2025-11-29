---
source_url: "https://gsap.com/docs/v3/Plugins/DrawSVGPlugin/static.getLength()"
title: "static-getLength | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:18:58.750567Z"
selector: "article"
---

# static-getLength | GSAP | Docs & Learning

* more plugins
* [DrawSVG](/docs/v3/Plugins/DrawSVGPlugin)
* methods
* DrawSVGPlugin.getLength()

On this page

# DrawSVGPlugin.getLength

### DrawSVGPlugin.getLength( element:[Element | Selector text] ) : Number

Provides an easy way to get the length of an SVG element's stroke including: `<path>`, `<rect>`, `<circle>`, `<ellipse>`, `<line>`, `<polyline>`, and `<polygon>`

#### Parameters

* #### **element**: [Element | Selector text]

  The element (or the selector text for the element) whose stroke length you'd like to determine.

### Returns : Number[​](#returns--number "Direct link to Returns : Number")

The length of an SVG element's stroke.

### Details[​](#details "Direct link to Details")

Provides an easy way to get the length of an SVG element's stroke including: `<path>`, `<rect>`, `<circle>`, `<ellipse>`, `<line>`, `<polyline>`, and `<polygon>`.

When combined with the position (obtained using `DrawSVGPlugin.getPosition`), you can calculate the total percentage at any given moment like so:

```
function getPercentage(element) {  
  return Math.floor(  
    DrawSVGPlugin.getPosition(element)[1] /  
      (DrawSVGPlugin.getLength(element) / 100)  
  );  
}
```