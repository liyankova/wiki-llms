---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollTrigger/isActive"
title: "isActive | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:12:40.749816Z"
selector: "article"
---

# isActive | GSAP | Docs & Learning

* [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/)
* properties
* .isActive

On this page

# .isActive

### .isActive : Boolean

[read-only] Only `true` if the scroll position is between the start and end positions of the ScrollTrigger instance.

### Details[​](#details "Direct link to Details")

[read-only] Only `true` if the scroll position is between the start and end positions of the ScrollTrigger instance.

## Example[​](#example "Direct link to Example")

```
ScrollTrigger.create({  
  trigger: ".trigger",  
  start: "top center",  
  end: "+=500",  
  onToggle: (self) => console.log("toggled. active?", self.isActive),  
});
```