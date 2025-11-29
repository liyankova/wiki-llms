---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/clear()"
title: "clear | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:11:17.938427Z"
selector: "article"
---

# clear | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .clear()

On this page

# clear

### clear( labels:Boolean ) : self

Empties the timeline of all tweens, timelines, and callbacks (and optionally labels too).

#### Parameters

* #### **labels**: Boolean

  (default = `true`) - If `true` (the default), labels will be cleared too.

### Returns : self[​](#returns--self "Direct link to Returns : self")

self (makes chaining easier)

### Details[​](#details "Direct link to Details")

Empties the timeline of all tweens, timelines, and callbacks (and optionally labels too). Event callbacks (like onComplete, onUpdate, onStart, etc.) are not removed. If you need to remove event callbacks, use the `eventCallback()` method and set them to null like `myTimeline.eventCallback("onComplete", null);`