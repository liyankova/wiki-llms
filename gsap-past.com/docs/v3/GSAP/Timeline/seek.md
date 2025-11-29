---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/seek()"
title: "seek | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:12:08.703821Z"
selector: "article"
---

# seek | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .seek()

On this page

# seek

### seek( position:\*, suppressEvents:Boolean ) : self

[override] Jumps to a specific time (or label) without affecting whether or not the instance is paused or reversed.

#### Parameters

* #### **position**: \*

  The position to go to, described in any of the following ways: a numeric value indicates an absolute position, like 3 would be exactly 3 seconds from the beginning of the timeline. A string value can be either a label (i.e. "myLabel") or a relative value using the "+=" or "-=" prefixes like "-=2" (2 seconds before the end of the timeline) or a combination like "myLabel+=2" to indicate 2 seconds after "myLabel" See the [Position Parameter article](/resources/position-parameter) which has interactive timeline visualizations and a video.
* #### **suppressEvents**: Boolean

  (default = `true`) - If `true` (the default), no events or callbacks will be triggered when the playhead moves to the new position defined in the `time`parameter.

### Returns : self[​](#returns--self "Direct link to Returns : self")

self (makes chaining easier)

### Details[​](#details "Direct link to Details")

Jumps to a specific time (or label) without affecting whether or not the instance is paused or reversed.

If there are any events/callbacks inbetween where the playhead was and the new time, they will not be triggered because by default `suppressEvents` (the 2nd parameter) is `true`. Think of it like picking the needle up on a record player and moving it to a new position before placing it back on the record. If, however, you do not want the events/callbacks suppressed during that initial move, simply set the `suppressEvents` parameter to `false`.

```
//jumps to exactly 2 seconds  
tl.seek(2);  
  
//jumps to exactly 2 seconds but doesn't suppress events during the initial move:  
tl.seek(2, false);  
  
//jumps to the "myLabel" label  
tl.seek("myLabel");
```