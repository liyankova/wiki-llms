---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/recent()"
title: "recent | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:11:51.640484Z"
selector: "article"
---

# recent | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .recent()

On this page

# recent

### recent( ) : [Tween | Timeline | Callback]

Returns the most recently added child tween/timeline/callback regardless of its position in the timeline.

### Details[​](#details "Direct link to Details")

Returns the most recently added child tween, timeline, or callback regardless of its position in the timeline.

```
var tl = gsap.timeline();  
  
//very long tween  
tl.to(e1, { duration: 999, x: 100, repeat: 5 });  
  
//insert this tween at 0.5 seconds (toward the beginning of the timeline)  
tl.to(e2, { duration: 1, y: 200 }, 0.5);  
  
//inserts the new tween 3 seconds after the e2 tween which was added most recently.  
tl.to(e3, { duration: 1, scaleX: 2 }, tl.recent().endTime() + 3);
```