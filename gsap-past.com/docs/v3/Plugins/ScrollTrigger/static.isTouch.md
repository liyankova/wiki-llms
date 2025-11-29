---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollTrigger/static.isTouch"
title: "static-isTouch | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:12:42.861196Z"
selector: "article"
---

# static-isTouch | GSAP | Docs & Learning

* [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/)
* properties
* ScrollTrigger.isTouch

On this page

# ScrollTrigger.isTouch

### ScrollTrigger.isTouch : Number

A way to discern the touch capabilities of the current device - `0` is mouse/pointer only (no touch), `1` is touch-only, `2` accommodates both.

### Details[​](#details "Direct link to Details")

A way to discern the touch capabilities of the device:

* `0` - **no touch** (pointer/mouse only)
* `1` - **touch-only** device (like a phone)
* `2` - device can accept **touch** input and **mouse/pointer** (like Windows tablets)

```
if (ScrollTrigger.isTouch) {  
  // any touch-capable device...  
}  
  
// or get more specific:  
if (ScrollTrigger.isTouch === 1) {  
  // touch-only device  
}
```