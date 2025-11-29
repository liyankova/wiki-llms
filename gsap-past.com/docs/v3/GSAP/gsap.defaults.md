---
source_url: "https://gsap.com/docs/v3/GSAP/gsap.defaults()"
title: "gsap.defaults() | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:54:57.320042Z"
selector: "article"
---

# gsap.defaults() | GSAP | Docs & Learning

* [GSAP](/docs/v3/GSAP/)
* methods
* gsap.defaults()

`gsap.defaults()` lets you set properties that should be inherited by **ALL** tweens (that don't have `inherit:false` set) unless overridden by that tween. General configuration settings that aren't Tween-specific (like `units`, `autoSleep`, and `force3D`) should be set using [`gsap.config()`](/docs/v3/GSAP/gsap.config()) instead.

For example, if you want to change the default `ease` and `duration` of all tweens you'd do:

```
gsap.defaults({  
  ease: "power2.in",  
  duration: 1,  
});
```