---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/play()"
title: "play | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:56:08.606052Z"
selector: "article"
---

# play | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .play()

On this page

# play

### play( from:\*, suppressEvents:Boolean ) : self

Begins playing forward, optionally from a specific time (by default playback begins from wherever the playhead currently is).

#### Parameters

* #### **from**: \*

  (default = `null`) - The time (or label for Time instances) from which the animation should begin playing (if none is defined, it will begin playing from wherever the playhead currently is).
* #### **suppressEvents**: Boolean

  (default = `true`) - If `true` (the default), no events or callbacks will be triggered when the playhead moves to the new position defined in the `from` parameter.

### Returns : self[​](#returns--self "Direct link to Returns : self")

self (makes chaining easier)

### Details[​](#details "Direct link to Details")

Begins playing forward, optionally from a specific time (by default playback begins from wherever the playhead currently is). This also ensures that the instance is neither paused nor reversed.

If you define a "from" time (the first parameter, which could also be a label for Timeline instances), the playhead moves there immediately and if there are any events/callbacks inbetween where the playhead was and the new time, they will not be triggered because by default `suppressEvents` (the 2nd parameter) is `true`. Think of it like picking the needle up on a record player and moving it to a new position before placing it back on the record. If, however, you do not want the events/callbacks suppressed during that initial move, simply set the `suppressEvents` parameter to `false`.

```
//begins playing from wherever the playhead currently is:  
tl.play();  
  
//begins playing from exactly 2-seconds into the animation:  
tl.play(2);  
  
//begins playing from exactly 2-seconds into the animation but doesn't suppress events during the initial move:  
tl.play(2, false);>
```

**Note:** if the Timeline's timeScale is exactly 0 when play() is called, it will be changed to 1 (otherwise it wouldn't play). If you're going to tween it up from 0 you can set it to a very small number before calling play() like `tl.timeScale(tl.timeScale() || 0.001).play()` so that it doesn't jump to 1.