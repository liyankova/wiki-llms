---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollTrigger/progress"
title: "progress | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:12:47.404135Z"
selector: "article"
---

# progress | GSAP | Docs & Learning

* [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/)
* properties
* .progress

On this page

# progress

### progress : Number

[read-only] The overall progress of the ScrollTrigger instance where 0 is at the start, 0.5 is in the middle, and 1 is at the end.

### Details[​](#details "Direct link to Details")

[read-only] The overall progress of the ScrollTrigger instance where 0 is at the start, 0.5 is in the middle, and 1 is at the end.

## Example[​](#example "Direct link to Example")

```
ScrollTrigger.create({  
  trigger: ".trigger",  
  start: "top center",  
  end: "+=500",  
  onUpdate: (self) => console.log("progress:", self.progress),  
});
```