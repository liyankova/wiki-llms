---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollTrigger/static.removeEventListener()"
title: "static-removeEventListener | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:14:01.182638Z"
selector: "article"
---

# static-removeEventListener | GSAP | Docs & Learning

* [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/)
* methods
* ScrollTrigger.removeEventListener()

On this page

# ScrollTrigger.removeEventListener

### ScrollTrigger.removeEventListener( type:String, callback:Function ) : null

Removes an event listener

#### Parameters

* #### **type**: String

  The type of listener which can be "scrollStart", "scrollEnd", "refreshInit", or "refresh".
* #### **callback**: Function

  The callback that should be removed as a listener

### Details[​](#details "Direct link to Details")

Removes a listener that had previously been added for any of the following events:

* **"scrollStart"** - when any ScrollTrigger-related scroller begins scrolling
* **"scrollEnd"** - when any ScrollTrigger-related scroller stops scrolling (when roughly 200ms elapses since the last "scroll" event AND the user doesn't have a pointer/mouse pressed on the document/scrollbar)
* **"refreshInit"** - typically just after a resize occurs and *BEFORE* ScrollTrigger does all of its recalculating of start/end values in the [new] document flow. This will also happen when you call [ScrollTrigger.refresh()](/docs/v3/Plugins/ScrollTrigger/static.refresh()) directly.
* **"refresh"** - immediately after ScrollTrigger finishes all of its recalculations of start/end values when a refresh occurs (typically after a resize event or when ScrollTrigger.refresh() is called directly).

## Example[​](#example "Direct link to Example")

```
ScrollTrigger.removeEventListener("scrollEnd", yourFunction);
```