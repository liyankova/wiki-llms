---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollTrigger/static.addEventListener()"
title: "static-addEventListener | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:13:20.733863Z"
selector: "article"
---

# static-addEventListener | GSAP | Docs & Learning

* [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/)
* methods
* ScrollTrigger.addEventListener()

On this page

# ScrollTrigger.addEventListener

### ScrollTrigger.addEventListener( type:String, callback:Function ) : null

Add a listener for any of the following events: "scrollStart", "scrollEnd", "refreshInit", "revert", "matchMedia", or"refresh" which get dispatched globally when **any** such ScrollTrigger-related event occurs (it is not tied to a particular instance).

#### Parameters

* #### **type**: String

  Event type which may be "scrollStart", "scrollEnd", "refreshInit", "revert", "matchMedia", or "refresh".
* #### **callback**: Function

  The function to call when the event occurs

### Details[​](#details "Direct link to Details")

Add a listener for any of the following events:

* **"matchMedia"** - when a ScrollTrigger.matchMedia() breakpoint is reached and finishes executing.
* **"refreshInit"** - typically just after a resize occurs and *BEFORE* ScrollTrigger does all of its recalculating of start/end values in the [new] document flow. This will also happen when you call [ScrollTrigger.refresh()](/docs/v3/Plugins/ScrollTrigger/static.refresh()) directly.
* **"refresh"** - immediately after ScrollTrigger finishes all of its recalculations of start/end values when a refresh occurs (typically after a resize event or when ScrollTrigger.refresh() is called directly).
* **"revert"** - when ScrollTrigger reverts the page to its original state, after it has removed all of its pinning spacers, etc. This typically happens between a "refreshInit" event and a "refresh" event.
* **"scrollStart"** - when any ScrollTrigger-related scroller begins scrolling
* **"scrollEnd"** - when any ScrollTrigger-related scroller stops scrolling (when roughly 200ms elapses since the last "scroll" event AND the user doesn't have a pointer/mouse pressed on the document/scrollbar)

These events get dispatched *globally* when **any** such ScrollTrigger-related event occurs (it is not tied to a particular instance).

## Example[​](#example "Direct link to Example")

```
ScrollTrigger.addEventListener("scrollEnd", () =>  
  console.log("scrolling ended!")  
);
```