---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/restart()"
title: "restart | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:12:03.095303Z"
selector: "article"
---

# restart | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .restart()

On this page

# restart

### restart( includeDelay:Boolean, suppressEvents:Boolean ) : self

Restarts and begins playing forward from the beginning.

#### Parameters

* #### **includeDelay**: Boolean

  (default = `false`) - Determines whether or not the delay (if any) is honored when restarting.
* #### **suppressEvents**: Boolean

  (default = `true`) - If `true` (the default), no events or callbacks will be triggered when the playhead moves to the new position defined in the `time` parameter.

### Returns : self[​](#returns--self "Direct link to Returns : self")

self (makes chaining easier)

### Details[​](#details "Direct link to Details")

Restarts and begins playing forward from the beginning.

```
//restarts, not including any delay that was defined  
tl.restart();  
  
//restarts, including any delay, and doesn't suppress events during the initial move back to time:0  
tl.restart(true, false);
```