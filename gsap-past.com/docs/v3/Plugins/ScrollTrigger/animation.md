---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollTrigger/animation"
title: "animation | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:12:34.208581Z"
selector: "article"
---

# animation | GSAP | Docs & Learning

* [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/)
* properties
* .animation

On this page

# .animation

### .animation : Tween | Timeline | undefined

[read-only] The [Tween](/docs/v3/GSAP/Tween) or [Timeline](/docs/v3/GSAP/Timeline) associated with the ScrollTrigger instance (if any).

### Returns : Tween | Timeline | undefined[​](#returns--tween--timeline--undefined "Direct link to Returns : Tween | Timeline | undefined")

The Tween or Timeline associated with the ScrollTrigger (if any)

### Details[​](#details "Direct link to Details")

[read-only] The [Tween](/docs/v3/GSAP/Tween) or [Timeline](/docs/v3/GSAP/Timeline) associated with the ScrollTrigger instance (if any). ScrollTriggers don't have to have any animation associated with them, of course, in which case `animation` will be undefined.

## Embedded example[​](#embedded-example "Direct link to Embedded example")

```
let tween = gsap.to(".class", {  
  x: 100,  
  id: "example",  
  scrollTrigger: ".trigger",  
});  
  
console.log(ScrollTrigger.getById("example").animation); // tween
```

## Standalone example[​](#standalone-example "Direct link to Standalone example")

```
let tween = gsap.to(".class", { x: 100 }),  
  st = ScrollTrigger.create({  
    trigger: ".trigger",  
    start: "top center",  
    end: "+=500",  
    animation: tween,  
  });  
  
console.log(st.animation); // tween
```