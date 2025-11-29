---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollTrigger/static.killAll()"
title: "static-killAll | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:13:45.326364Z"
selector: "article"
---

# static-killAll | GSAP | Docs & Learning

* [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/)
* methods
* ScrollTrigger.killAll()

On this page

# ScrollTrigger.killAll

### ScrollTrigger.killAll( ) ;

Immediately calls `kill()` on **all** ScrollTriggers (except the main ScrollSmoother one if it exists).

### Details[​](#details "Direct link to Details")

Immediately calls `kill()` on **all** ScrollTriggers (except the main ScrollSmoother one if it exists). This can be useful when routing in frameworks where you need to clear out the current page and then load a new one without refreshing the window.