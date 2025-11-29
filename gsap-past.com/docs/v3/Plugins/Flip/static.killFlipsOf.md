---
source_url: "https://gsap.com/docs/v3/Plugins/Flip/static.killFlipsOf()"
title: "static-killFlipsOf | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:15:36.018685Z"
selector: "article"
---

# static-killFlipsOf | GSAP | Docs & Learning

* [Flip](/docs/v3/Plugins/Flip/)
* methods
* Flip.killFlipsOf()

On this page

# Flip.killFlipsOf

### Flip.killFlipsOf( targets:String | Array | NodeList | Element, complete:boolean ) ;

Immediately kills the Flip animation associated with any of the targets provided.

#### Parameters

* #### **targets**: String | Array | NodeList | Element

  The targets whose Flip animations should be killed. It can be selector text, an Array, Element, or NodeList.
* #### **complete**: boolean

  If `false`, the flip animation(s) will be forced to completion rather than just stopped.

### Details[​](#details "Direct link to Details")

Immediately kills the Flip animation associated with any of the targets provided. It will also force them to completion unless the 2nd parameter is explicitly set to `false`.

```
Flip.killFlipsOf(".box, .container");
```