---
source_url: "https://gsap.com/docs/v3/GSAP/gsap.isTweening()"
title: "gsap.isTweening() | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:55:29.735298Z"
selector: "article"
---

# gsap.isTweening() | GSAP | Docs & Learning

* [GSAP](/docs/v3/GSAP/)
* methods
* gsap.isTweening()

On this page

### Returns : Boolean[​](#returns--boolean "Direct link to Returns : Boolean")

Reports whether or not a particular object is actively animating. If a tween is paused, completed, or hasn't started yet, it isn't considered active. For example:

```
if (!gsap.isTweening("#id")) {  
  // do stuff  
}
```

The `target` can be selector text or an object/element.