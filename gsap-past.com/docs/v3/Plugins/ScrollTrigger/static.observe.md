---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollTrigger/static.observe()"
title: "static-observe | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:13:54.644201Z"
selector: "article"
---

# static-observe | GSAP | Docs & Learning

* [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/)
* methods
* ScrollTrigger.observe()

On this page

# ScrollTrigger.observe

### ScrollTrigger.observe( config:Object ) : Observer

Super-flexible, unified way to sense meaningful events across all (touch/mouse/pointer) devices without wrestling with all the implementation details. Trigger simple callbacks like onUp, onDown, onLeft, onRight, onChange, onHover, onDrag, etc. Functionally identical to [Observer.create()](/docs/v3/Plugins/Observer/static.create())

#### Parameters

* #### **config**: Object

  A configuration object with properties like target, type, onUp, onDown, etc.

### Returns : Observer[​](#returns--observer "Direct link to Returns : Observer")

An Observer object that has properties like `deltaX`, `deltaY`, etc. See [Observer docs](/docs/v3/Plugins/Observer) for details.

### Details[​](#details "Direct link to Details")

Super-flexible, unified way to sense meaningful events across all (touch/mouse/pointer) devices without wrestling with all the implementation details. Perhaps you want to respond to "scroll-like" user behavior which could be a mouse wheel spin, finger swipe on a touch device, a scrollbar drag, or a pointer press & drag...and of course you need directional data and velocity. No problem!

`ScrollTrigger.observe()` is just a convenient way to access [Observer.create()](/docs/v3/Plugins/Observer/static.create()). Since [ScrollTrigger.normalizeScroll()](/docs/v3/Plugins/ScrollTrigger/static.normalizeScroll()) functionality leverages Observer under the hood (thus it's included inside ScrollTrigger anyway), it made sense to expose its functionality so that you can avoid loading Observer as a separate file if you're already using ScrollTrigger in your project. You're welcome. 🙂

Look how easy it is to trigger next()/previous() functions based on when the user swipes up/down or uses their mouse wheel:

```
ScrollTrigger.observe({  
  target: window, // can be any element (selector text is fine)  
  type: "wheel,touch", // comma-delimited list of what to listen for ("wheel,touch,scroll,pointer")  
  onUp: () => previous(),  
  onDown: () => next(),  
});
```

## Demo[​](#demo "Direct link to Demo")

Notice there's no actual scrolling in the demo below but you can use your mouse wheel (or swipe on touch devices) to initiate movement so it "feels" like a scroll:

#### loading...

## Configuration and Usage Details[​](#configuration-and-usage-details "Direct link to Configuration and Usage Details")

Please see the [Observer docs](/docs/v3/Plugins/Observer) for all the nitty-gritty details.