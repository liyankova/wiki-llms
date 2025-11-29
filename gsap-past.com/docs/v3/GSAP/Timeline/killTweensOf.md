---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/killTweensOf()"
title: "killTweensOf | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:11:44.243575Z"
selector: "article"
---

# killTweensOf | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .killTweensOf()

On this page

# killTweensOf

### killTweensOf( targets:Selector text | Array | Object, props:String, onlyActive:Boolean ) : Timeline

Kills all of the tweens inside this timeline that affect the provided `targets`. You can optionally specify specific properties that you want killed.

#### Parameters

* #### **targets**: Selector text | Array | Object

  The target object(s) whose tweens should be killed.
* #### **props**: String

  A comma-delimited list of property names to kill (optional). If null, all properties will be killed.
* #### **onlyActive**: Boolean

  If `true`, only active (in-progress) tweens will be affected.

### Returns : Timeline[​](#returns--timeline "Direct link to Returns : Timeline")

self (for easy chaining)

### Details[​](#details "Direct link to Details")

Kills all of the tweens inside this timeline that affect the provided `targets`. You can optionally specify specific properties that you want killed. For example:

```
// kills all the tweens of elements with the class of "box"  
tl.killTweensOf(".box");  
  
// kills only animations of "x" and "y" properties of elements with the class of "box"  
tl.killTweensOf(".box", "x,y");
```