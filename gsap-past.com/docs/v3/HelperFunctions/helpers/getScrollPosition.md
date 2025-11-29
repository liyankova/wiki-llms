---
source_url: "https://gsap.com/docs/v3/HelperFunctions/helpers/getScrollPosition"
title: "getScrollPosition | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:16:28.182459Z"
selector: "article"
---

# getScrollPosition | GSAP | Docs & Learning

* [Helper functions](/docs/v3/HelperFunctions/)
* getScrollPosition

Perhaps you want to scroll the page to the exact spot where a particular scroll-triggered animation starts (or ends or any progress value) - just feed this helper function your animation (it must have a ScrollTrigger of course) and optionally a progress value (0 is when the animation starts, 0.5 is halfway through, 1 is the end) and it'll return the scroll position which you could feed into a scrollTo tween, for example:

```
function getScrollPosition(animation, progress) {  
  let p = gsap.utils.clamp(0, 1, progress || 0),  
    st = animation.scrollTrigger,  
    containerAnimation = st.vars.containerAnimation;  
  if (containerAnimation) {  
    let time = st.start + (st.end - st.start) * p;  
    st = containerAnimation.scrollTrigger;  
    return (  
      st.start + (st.end - st.start) * (time / containerAnimation.duration())  
    );  
  }  
  return st.start + (st.end - st.start) * p;  
}
```

It even works with the "containerAnimation" feature:

#### loading...