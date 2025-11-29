---
source_url: "https://gsap.com/docs/v3/Plugins/Flip/static.isFlipping()"
title: "static-isFlipping | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:15:33.544203Z"
selector: "article"
---

# static-isFlipping | GSAP | Docs & Learning

* [Flip](/docs/v3/Plugins/Flip/)
* methods
* Flip.isFlipping()

On this page

# Flip.isFlipping

### Flip.isFlipping( target:String | Element ) : Boolean

Returns `true` if the given target is currently being Flipped. Otherwise returns `false`.

#### Parameters

* #### **target**: String | Element

  The target element to check. Can be selector text or an Element

### Returns : Boolean[​](#returns--boolean "Direct link to Returns : Boolean")

Whether or not the given target is currently being Flipped.

### Details[​](#details "Direct link to Details")

Returns `true` if the given target is currently being Flipped. Otherwise returns `false`.

```
if (Flip.isFlipping(".box-1")) {  
  // do stuff  
}
```