---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/removePause()"
title: "removePause | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:11:57.368031Z"
selector: "article"
---

# removePause | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .removePause()

On this page

# removePause

### removePause( position:[Number | Label] ) : self

Removes pauses that were added to a timeline via its `.addPause()` method.

#### Parameters

* #### **position**: [Number | Label]

  The time (or label) where the pause should be removed from.

### Returns : self[​](#returns--self "Direct link to Returns : self")

self (makes chaining easier)

### Details[​](#details "Direct link to Details")

Removes the pause from a specific position which was added to the timeline via [`addPause()`](/docs/v3/GSAP/Timeline/addPause()).

```
var tl = gsap.timeline();  
tl.to(obj, { duration: 1, x: 100 });  
  
//added at time of 1  
tl.addPause();  
  
//another animation  
tl.to(obj, { duration: 1, opacity: 0 });  
  
//later on remove the pause  
tl.removePause(1);
```