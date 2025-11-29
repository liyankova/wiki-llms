---
source_url: "https://gsap.com/docs/v3/HelperFunctions/helpers/blendEases"
title: "blendEases | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:16:04.303058Z"
selector: "article"
---

# blendEases | GSAP | Docs & Learning

* [Helper functions](/docs/v3/HelperFunctions/)
* blendEases

If you need one ease at the start of your animation, and a different one at the end, you can use this function to blend them!

```
//just feed in the starting ease and the ending ease (and optionally an ease to do &#xFEFF;the blending), and it'll return a new Ease that's...blended!  
function blendEases(startEase, endEase, blender) {  
  var parse = function (ease) {  
      return typeof ease === "function" ? ease : gsap.parseEase("power4.inOut");  
    },  
    s = gsap.parseEase(startEase),  
    e = gsap.parseEase(endEase),  
    blender = parse(blender);  
  return function (v) {  
    var b = blender(v);  
    return s(v) * (1 - b) + e(v) * b;  
  };  
}  
//example usage:  
gsap.to("#target", {  
  duration: 2,  
  x: 100,  
  ease: blendEases("back.in(1.2)", "bounce"),  
});
```

**DEMO**

#### loading...

If you need to **invert** an ease instead, see [this demo](https://codepen.io/GreenSock/pen/rgROxY?editors=0010) for a different helper function.