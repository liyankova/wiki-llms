---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/getTweensOf()"
title: "getTweensOf | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:11:32.885071Z"
selector: "article"
---

# getTweensOf | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .getTweensOf()

On this page

# getTweensOf

### getTweensOf( target:[Object | Selector text | Array], nested:Boolean ) : Array

Returns the tweens of a particular object that are inside this timeline.

#### Parameters

* #### **target**: [Object | Selector text | Array]

  The target object of the tweens.
* #### **nested**: Boolean

  (default = `true`) - Determines whether or not tweens that are inside nested timelines should be returned. If you only want the "top level" tweens and timelines, set this to `false`.

### Returns : Array[​](#returns--array "Direct link to Returns : Array")

An Array of Tween instances.

### Details[​](#details "Direct link to Details")

Returns the tweens of a particular target that are inside this timeline. You may pass in multiple targets in an array or selector text.

```
// Get all tweens of the timeline with the target of ".myClass"  
tl.getTweensOf(".myClass");  
  
// Get all tweens of the timeline with the target of myElem, including nested timelines  
tl.getTweensOf(myElem, true);
```