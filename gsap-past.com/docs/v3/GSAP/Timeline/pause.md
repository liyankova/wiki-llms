---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/pause()"
title: "pause | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:56:04.055557Z"
selector: "article"
---

# pause | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .pause()

On this page

# pause

### pause( atTime:\*, suppressEvents:Boolean ) : self

Pauses the instance, optionally jumping to a specific time.

#### Parameters

* #### **atTime**: \*

  (default = `null`) - The time (or label for Timeline instances) that the instance should jump to before pausing (if none is defined, it will pause wherever the playhead is currently located).
* #### **suppressEvents**: Boolean

  default = `true`) - If `true` (the default), no events or callbacks will be triggered when the playhead moves to the new position defined in the `atTime` parameter.

### Returns : self[​](#returns--self "Direct link to Returns : self")

self (makes chaining easier)

### Details[​](#details "Direct link to Details")

Pauses the animation, optionally jumping to a specific time first.

If you define a time to jump to (the first parameter, which could also be a label for Timeline instances), the playhead moves there immediately and skips any events/callbacks inbetween where the playhead was and the new time (unless `suppressEvents` parameter is `false`). Think of it like picking the needle up on a record player and moving it to a new position before placing it back on the record. If you do want the events/callbacks to be triggered during that initial move, simply set the `suppressEvents` parameter to `false`.

```
//pauses wherever the playhead currently is:  
tl.pause();  
  
//jumps to exactly 2-seconds into the animation and then pauses:  
tl.pause(2);  
  
//jumps to exactly 2-seconds into the animation and pauses but doesn't suppress events during the initial move:  
tl.pause(2, false);
```

Note that when an animation (tween or timeline) is nested within a timeline, the parent timeline's playhead will continue to run even if the child animation is paused ([demo](https://codepen.io/GreenSock/pen/BaKogyg?editors=1000)). In most cases you want to pause the parent timeline instead.