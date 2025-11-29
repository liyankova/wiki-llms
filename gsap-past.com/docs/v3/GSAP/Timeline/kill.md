---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/kill()"
title: "kill | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:11:42.437896Z"
selector: "article"
---

# kill | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .kill()

On this page

# kill

### kill( ) : Timeline

Immediately kills the timeline and removes it from its parent timeline, stopping its animation.

### Returns : Timeline[​](#returns--timeline "Direct link to Returns : Timeline")

Self (for chaining)

### Details[​](#details "Direct link to Details")

Immediately stops the animation, removing it from its parent timeline, and releasing it for garbage collection. **Note**: don't kill() an animation if you want to use it again later - you could pause() it instead if you want to reuse it.

```
// kill the timeline  
tl.kill();  
  
// set to null so the reference is removed  
tl = null;
```