---
source_url: "https://gsap.com/docs/v3/Plugins/Draggable/static.get()"
title: "static-get | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:18:08.050637Z"
selector: "article"
---

# static-get | GSAP | Docs & Learning

* more plugins
* [Draggable](/docs/v3/Plugins/Draggable/)
* methods
* Draggable.get()

On this page

# Draggable.get

### Draggable.get( target:Object ) : Draggable

[static] Provides an easy way to get the Draggable instance that's associated with a particular DOM element.

#### Parameters

* #### **target**: Object

  The target DOM element whose Draggable instance you want to retrieve; this can be either the element itself, or a selector string like `"#myElement"`

### Returns : Draggable[​](#returns--draggable "Direct link to Returns : Draggable")

The Draggable instance that's associated with the target element (or `undefined` if none exists).

### Details[​](#details "Direct link to Details")

Provides an easy way to get the Draggable instance that's associated with a particular DOM element. For example, maybe you made all of the elements with the class "draggable" draggable by calling `Draggable.create(".draggable")` and then you want to find the individual Draggable instance that's associated with the element with an ID of "element1" that'd be as simple as:

```
var draggable = Draggable.get("#element1"); //or use the element itself instead of a selector string: var myElement =
```