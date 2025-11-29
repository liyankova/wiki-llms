---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/remove()"
title: "remove | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:11:53.555936Z"
selector: "article"
---

# remove | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .remove()

On this page

# remove

### remove( value:[Tween | Timeline | Callback | Label] ) : self

Removes a tween, timeline, callback, or label (or array of them) from the timeline.

#### Parameters

* #### **value**: [Tween | Timeline | Callback | Label]

  The tween, timeline, callback, or label that should be removed from the timeline (or an array of them)

### Returns : self[​](#returns--self "Direct link to Returns : self")

self (makes chaining easier)

### Details[​](#details "Direct link to Details")

Removes a tween, timeline, callback, or label (or array of them) from the timeline.

```
tl.remove(myTween);  
tl.remove([myTween, mySubTimeline, "myLabel"]);
```