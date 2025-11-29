---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollSmoother/smooth()"
title: "smooth | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:14:45.207708Z"
selector: "article"
---

# smooth | GSAP | Docs & Learning

* [ScrollSmoother](/docs/v3/Plugins/ScrollSmoother/)
* methods
* .smooth()

On this page

# .smooth

### .smooth( duration:Number ) : Number | self

Gets/Sets the number of seconds it takes to catch up to the scroll position (smoothing).

#### Parameters

* #### **duration**: Number

  The number of seconds that it should take to "catch up" to the native scroll position.

### Returns : Number | self[​](#returns--number--self "Direct link to Returns : Number | self")

The number of seconds it takes to catch up to the scroll position (if getter) or the ScrollSmoother instance itself (if setter) for easier chaining

### Details[​](#details "Direct link to Details")

Gets/Sets the number of seconds it takes to catch up to the scroll position (smoothing).

```
// setter  
smoother.smooth(1.5);  
  
// getter  
let duration = smoother.smooth();
```