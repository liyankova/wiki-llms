---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollSmoother/static.get()"
title: "static-get | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:14:49.903701Z"
selector: "article"
---

# static-get | GSAP | Docs & Learning

* [ScrollSmoother](/docs/v3/Plugins/ScrollSmoother/)
* methods
* ScrollSmoother.get()

On this page

# ScrollSmoother.get

### ScrollSmoother.get( ) : ScrollSmoother

Returns the ScrollSmoother instance (if one has been created). There can only be one instance at any given time.

### Details[​](#details "Direct link to Details")

Returns the ScrollSmoother instance (if one has been created). There can only be one instance at any given time.

```
let smoother = ScrollSmoother.create({...});  
  
// then later, you can get that instance (perhaps in another file) like this:  
let previouslyCreatedSmoother = ScrollSmoother.get();
```