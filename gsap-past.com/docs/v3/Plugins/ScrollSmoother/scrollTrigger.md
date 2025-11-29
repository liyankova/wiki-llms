---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollSmoother/scrollTrigger"
title: "scrollTrigger | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:14:21.496352Z"
selector: "article"
---

# scrollTrigger | GSAP | Docs & Learning

* [ScrollSmoother](/docs/v3/Plugins/ScrollSmoother/)
* properties
* .scrollTrigger

On this page

# .scrollTrigger

### .scrollTrigger : ScrollTrigger

The ScrollTrigger instance that ScrollSmoother created internally to manage the smooth scrolling effect of the page.

### Details[​](#details "Direct link to Details")

The [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger) instance that ScrollSmoother created internally to manage the smooth scrolling effect of the page.

```
let smoother = ScrollSmoother.create({...});  
  
let nativeScrollVelocity = smoother.scrollTrigger.getVelocity();
```