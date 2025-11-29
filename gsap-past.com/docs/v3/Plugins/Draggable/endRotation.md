---
source_url: "https://gsap.com/docs/v3/Plugins/Draggable/endRotation"
title: "endRotation | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:16:58.784213Z"
selector: "article"
---

# endRotation | GSAP | Docs & Learning

* more plugins
* [Draggable](/docs/v3/Plugins/Draggable/)
* properties
* .endRotation

On this page

# endRotation

### endRotation : Number

[read-only] [only applies to type:"rotation"] The ending rotation of the Draggable instance which is calculated as soon as the mouse/touch is released after a drag, meaning you can use it to predict precisely where it'll land after a `inertia` flick.

### Details[​](#details "Direct link to Details")

*Number* - [only applies to `type: "rotation"` Draggable objects] The ending rotation of the Draggable instance. `endRotation` gets populated immediately when the mouse (or touch) is released after dragging, even before tweening has completed. This makes it easy to predict exactly what angle the element will land at (useful for `inertia: true` Draggables where momentum gets applied and you want to predict where it'll land).