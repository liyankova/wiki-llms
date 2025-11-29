---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/scrollTrigger"
title: "scrollTrigger | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:11:06.366259Z"
selector: "article"
---

# scrollTrigger | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* properties
* .scrollTrigger

On this page

# scrollTrigger

### scrollTrigger: [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/) | undefined

A handy way to access the ScrollTrigger associated with a timeline. This is only accessible if the timeline has a ScrollTrigger.

### Details[​](#details "Direct link to Details")

warning

A `scrollTrigger`property is only added to the Timeline or Tween *if* it has a ScrollTrigger.

See the [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/) docs for more details

```
// add a ScrollTrigger to a Timeline  
let tl = gsap.timeline({scrollTrigger: {start: "top center"...}});  
  
// access the ScrollTrigger to call various methods  
tl.scrollTrigger.refresh();  
// or  
tl.scrollTrigger.kill();
```