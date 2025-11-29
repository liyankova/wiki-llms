---
source_url: "https://gsap.com/docs/v3/HelperFunctions/helpers/tickGSAPWhileHidden"
title: "tickGSAPWhileHidden | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:16:45.108544Z"
selector: "article"
---

# tickGSAPWhileHidden | GSAP | Docs & Learning

* [Helper functions](/docs/v3/HelperFunctions/)
* tickGSAPWhileHidden

Most browsers pause requestAnimationFrame() calls while a browser tab is hidden in order to reduce CPU/battery drain, but if you'd like GSAP to continue to update (at a reduced rate, typically about 2fps due to browsers throttling setInterval()/setTimeout()), you can use this function:

```
function tickGSAPWhileHidden(value) {  
  if (value === false) {  
    document.removeEventListener("visibilitychange", tickGSAPWhileHidden.fn);  
    return clearInterval(tickGSAPWhileHidden.id);  
  }  
  const onChange = () => {  
    clearInterval(tickGSAPWhileHidden.id);  
    if (document.hidden) {  
      gsap.ticker.lagSmoothing(0); // keep the time moving forward (don't adjust for lag)  
      tickGSAPWhileHidden.id = setInterval(gsap.ticker.tick, 500);  
    } else {  
      gsap.ticker.lagSmoothing(500, 33); // restore lag smoothing  
    }  
  };  
  document.addEventListener("visibilitychange", onChange);  
  tickGSAPWhileHidden.fn = onChange;  
  onChange(); // in case the document is currently hidden.  
}  
  
tickGSAPWhileHidden(true);
```