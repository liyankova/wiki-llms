---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollTrigger/static.getById()"
title: "static-getById | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:13:38.063406Z"
selector: "article"
---

# static-getById | GSAP | Docs & Learning

* [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/)
* methods
* ScrollTrigger.getById()

On this page

# ScrollTrigger.getById

### ScrollTrigger.getById( id:String ) : ScrollTrigger

Returns the ScrollTrigger that was assigned the corresponding `id`

#### Parameters

* #### **id**: String

  The identifier string that was used as the ScrollTrigger's `id`

### Returns : ScrollTrigger[​](#returns--scrolltrigger "Direct link to Returns : ScrollTrigger")

The ScrollTrigger instance with the matching `id` (or undefined if no matching ScrollTriggers are found)

### Details[​](#details "Direct link to Details")

Returns the ScrollTrigger that was assigned the corresponding `id`. For example:

```
ScrollTrigger.create({  
  id: "myID",  
  ...  
});  
  
// then later...  
let trigger = ScrollTrigger.getById("myID");
```