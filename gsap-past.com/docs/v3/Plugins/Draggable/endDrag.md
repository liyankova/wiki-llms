---
source_url: "https://gsap.com/docs/v3/Plugins/Draggable/endDrag()"
title: "endDrag | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:18:05.970164Z"
selector: "article"
---

# endDrag | GSAP | Docs & Learning

* more plugins
* [Draggable](/docs/v3/Plugins/Draggable/)
* methods
* .endDrag()

On this page

# endDrag

### endDrag( event:Object ) : void

You may force the Draggable to immediately stop interactively dragging by calling `endDrag()` and passing it the original mouse or touch event that initiated the stop - this is necessary because Draggable must inspect that event for various information like `pageX`, `pageY`, `target`, etc.

#### Parameters

* #### **event**: Object

  A mouse or touch event.

### Details[​](#details "Direct link to Details")

You may force the Draggable to immediately stop interactively dragging by calling `endDrag()` and passing it the original mouse or touch event that initiated the stop - this is necessary because Draggable must inspect that event for various information like `pageX`, `pageY`, `target`, etc. You cannot call `endDrag()` without passing that original event.

`endDrag()` is different than `disable()` in that `disable()` completely shuts down the Draggable instance so that the user cannot initiate dragging anymore whereas `endDrag()` simply stops a drag-in-progress, acting like the user released their mouse/touch.