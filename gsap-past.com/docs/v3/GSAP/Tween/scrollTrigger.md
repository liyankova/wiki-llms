---
source_url: "https://gsap.com/docs/v3/GSAP/Tween/scrollTrigger"
title: "scrollTrigger | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:10:21.160175Z"
selector: "article"
---

# scrollTrigger | GSAP | Docs & Learning

* [Tween](/docs/v3/GSAP/Tween)
* properties
* .scrollTrigger

On this page

# scrollTrigger

### scrollTrigger: [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/) | undefined

A handy way to access the ScrollTrigger associated with a tween. This is only accessible if the tween has a ScrollTrigger.

### Details[​](#details "Direct link to Details")

warning

A "scrollTrigger" property is **only** added to the Timeline or Tween **if** it has a ScrollTrigger.

See the [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/) docs for more details

```
// add a ScrollTrigger to a Timeline  
let tl = gsap.to("#id" {scrollTrigger: {start: "top center"...}});  
  
// access the ScrollTrigger to call various methods  
tl.scrollTrigger.refresh();  
// or  
tl.scrollTrigger.kill();
```