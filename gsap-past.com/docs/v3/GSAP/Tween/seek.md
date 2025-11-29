---
source_url: "https://gsap.com/docs/v3/GSAP/Tween/seek()"
title: "seek | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:57:06.157525Z"
selector: "article"
---

# seek | GSAP | Docs & Learning

* [Tween](/docs/v3/GSAP/Tween)
* methods
* .seek()

On this page

# seek

### seek( time:\*, suppressEvents:Boolean ) : self

Jumps to a specific time without affecting whether or not the instance is paused or reversed.

#### Parameters

* #### **time**: \*

  The time (or label for Timeline instances) to go to.
* #### **suppressEvents**: Boolean

  (default = `true`) - If `true` (the default), no events or callbacks will be triggered when the playhead moves to the new position defined in the `time` parameter.

### Returns : self[​](#returns--self "Direct link to Returns : self")

self (makes chaining easier)

### Details[​](#details "Direct link to Details")

Jumps to a specific time without affecting whether or not the instance is paused or reversed.

If there are any events/callbacks inbetween where the playhead was and the new time, they will not be triggered because by default `suppressEvents` (the 2nd parameter) is `true`. Think of it like picking the needle up on a record player and moving it to a new position before placing it back on the record. If, however, you do not want the events/callbacks suppressed during that initial move, simply set the `suppressEvents` parameter to `false`.

```
//jumps to exactly 2 seconds  
myAnimation.seek(2);  
  
//jumps to exactly 2 seconds but doesn't suppress events during the initial move:  
myAnimation.seek(2, false);
```