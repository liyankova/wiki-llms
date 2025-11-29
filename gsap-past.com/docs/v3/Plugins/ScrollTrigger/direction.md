---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollTrigger/direction"
title: "direction | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:12:36.408608Z"
selector: "article"
---

# direction | GSAP | Docs & Learning

* [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/)
* properties
* .direction

On this page

# .direction

### .direction : Number

[read-only] Reflects the moment-by-moment direction of scrolling where `1` is forward and `-1` is backward.

### Details[​](#details "Direct link to Details")

[read-only] Reflects the moment-by-moment direction of scrolling where `1` is forward and `-1` is backward.

## Example[​](#example "Direct link to Example")

```
ScrollTrigger.create({  
  trigger: ".trigger",  
  start: "top center",  
  end: "+=500",  
  onUpdate: (self) => console.log("direction:", self.direction),  
});
```