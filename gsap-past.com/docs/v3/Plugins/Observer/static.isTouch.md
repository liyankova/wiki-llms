---
source_url: "https://gsap.com/docs/v3/Plugins/Observer/static.isTouch"
title: "static-isTouch | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:20:11.269911Z"
selector: "article"
---

# static-isTouch | GSAP | Docs & Learning

* more plugins
* [Observer](/docs/v3/Plugins/Observer/)
* properties
* Observer.isTouch

On this page

# Observer.isTouch

### Observer.isTouch : Number

A way to discern the touch capabilities of the current device - `0` is mouse/pointer only (no touch), `1` is touch-only, `2` accommodates both.

### Details[​](#details "Direct link to Details")

A way to discern the touch capabilities of the device:

* `0` - **no touch** (pointer/mouse only)
* `1` - **touch-only** device (like a phone)
* `2` - device can accept **touch** input and **mouse/pointer** (like Windows tablets)

```
if (Observer.isTouch) {  
  // any touch-capable device...  
}  
  
// or get more specific:  
if (Observer.isTouch === 1) {  
  // touch-only device  
}
```