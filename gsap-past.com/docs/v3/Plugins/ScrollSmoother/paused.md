---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollSmoother/paused()"
title: "paused | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:14:38.451559Z"
selector: "article"
---

# paused | GSAP | Docs & Learning

* [ScrollSmoother](/docs/v3/Plugins/ScrollSmoother/)
* methods
* .paused()

On this page

# .paused

### .paused( pause:Boolean ) : Boolean | self

Gets/Sets the paused state - if `true`, nothing will scroll (except via [scrollTop()](/docs/v3/Plugins/ScrollSmoother/scrollTop()) or [scrollTo()](/docs/v3/Plugins/ScrollSmoother/scrollTo()) on this instance).

#### Parameters

* #### **pause**: Boolean

  If `true`, it will immediately stop scrolling. If `false`, it will resume.

### Details[​](#details "Direct link to Details")

Gets/Sets the paused state - if `true`, nothing will scroll (except via [scrollTop()](/docs/v3/Plugins/ScrollSmoother/scrollTop()) or [scrollTo()](/docs/v3/Plugins/ScrollSmoother/scrollTo()) on this instance).

Pausing immediately stops movement and prevents the user from even moving the scrollbar.

```
// setter  
smoother.paused(true);  
  
// getter  
if (!smoother.paused()) {  
  // do stuff...  
}
```

You could toggle, for example, like this:

```
document.querySelector("#toggle").addEventListener("click", () => {  
  // toggle!  
  smoother.paused(!smoother.paused());  
});
```