---
source_url: "https://gsap.com/docs/v3/HelperFunctions/helpers/killChildTweensOf"
title: "killChildTweensOf | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:16:33.385252Z"
selector: "article"
---

# killChildTweensOf | GSAP | Docs & Learning

* [Helper functions](/docs/v3/HelperFunctions/)
* killChildTweensOf

On this page

You can kill all tweening elements that are children of a given target by using this function:

## Demo[​](#demo "Direct link to Demo")

```
function killChildTweensOf(ancestor) {  
  ancestor = gsap.utils.toArray(ancestor)[0];  
  gsap.globalTimeline  
    .getChildren(true, true, false)  
    .forEach((tween) =>  
      tween  
        .targets()  
        .forEach((e) => e.nodeType && ancestor.contains(e) && tween.kill(e))  
    );  
}
```

#### loading...