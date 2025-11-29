---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollTrigger/previous()"
title: "previous | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:13:13.368276Z"
selector: "article"
---

# previous | GSAP | Docs & Learning

* [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/)
* methods
* .previous()

On this page

# .previous

### .previous( ) : ScrollTrigger instance

Returns the previous ScrollTrigger in the refresh order.

### Returns : ScrollTrigger instance[​](#returns--scrolltrigger-instance "Direct link to Returns : ScrollTrigger instance")

The previous ScrollTrigger in the refresh order

### Details[​](#details "Direct link to Details")

Returns the previous ScrollTrigger in the refresh order. This can be useful in advanced scenarios where you want to base one ScrollTrigger's start/end value on the previous one's:

```
ScrollTrigger.create({  
  start: self => self.previous().end, // start at the end of the previous ScrollTrigger  
  ...  
});
```