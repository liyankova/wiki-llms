---
source_url: "https://gsap.com/docs/v3/HelperFunctions/helpers/smoothOriginChange"
title: "smoothOriginChange | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:16:42.920427Z"
selector: "article"
---

# smoothOriginChange | GSAP | Docs & Learning

* [Helper functions](/docs/v3/HelperFunctions/)
* smoothOriginChange

If you want to change `transformOrigin` dynamically without a jump, you'd need to compensate its translation (x/y). Here's a function I whipped together for that purpose:

```
function smoothOriginChange(targets, transformOrigin) {  
  gsap.utils.toArray(targets).forEach(function (target) {  
    var before = target.getBoundingClientRect();  
    gsap.set(target, { transformOrigin: transformOrigin });  
    var after = target.getBoundingClientRect();  
    gsap.set(target, {  
      x: "+=" + (before.left - after.left),  
      y: "+=" + (before.top - after.top),  
    });  
  });  
}
```

**DEMO**

#### loading...