---
source_url: "https://gsap.com/docs/v3/Plugins/Observer/static.getAll()"
title: "static-getAll | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:20:32.967707Z"
selector: "article"
---

# static-getAll | GSAP | Docs & Learning

* more plugins
* [Observer](/docs/v3/Plugins/Observer/)
* methods
* Observer.getAll()

On this page

# Observer.getAll

### Observer.getAll( ) : Array

Gets an Array of all Observers that have been created (and not killed). This can be useful if, for example, your framework requires that you kill everything like on a routing change.

### Returns : Array[​](#returns--array "Direct link to Returns : Array")

An Array of Observer instances

### Details[​](#details "Direct link to Details")

Gets an Array of all Observers that have been created (and not killed). This can be useful if, for example, your framework requires that you kill everything like on a routing change. Like:

```
Observer.getAll((o) => o.kill());
```