---
source_url: "https://gsap.com/docs/v3/Plugins/Observer/static.getById()"
title: "static-getById | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:20:35.021432Z"
selector: "article"
---

# static-getById | GSAP | Docs & Learning

* more plugins
* [Observer](/docs/v3/Plugins/Observer/)
* methods
* Observer.getById()

On this page

# Observer.getById

### Observer.getById( id:String ) : Observer

The Observer instance with the matching `id` that was defined in the configuration `vars` object (or undefined if no matching ScrollTriggers are found)

#### Parameters

* #### **id**: String

  The identifier string that was used as the Observer's id in the configuration object, like Observer.create({ id: "my-id" });

### Returns : Observer[​](#returns--observer "Direct link to Returns : Observer")

The Observer associated with the `id` (or null if none is found)

### Details[​](#details "Direct link to Details")

The Observer instance with the matching `id` that was defined in the configuration `vars` object, like:

```
Observer.create({  
  id: "my-id",  
  ...  
});  
  
// then later...  
let observer = Observer.getById("my-id");
```