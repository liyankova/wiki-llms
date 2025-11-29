---
source_url: "https://gsap.com/docs/v3/Plugins/Draggable/lockAxis"
title: "lockAxis | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:17:09.335477Z"
selector: "article"
---

# lockAxis | GSAP | Docs & Learning

* more plugins
* [Draggable](/docs/v3/Plugins/Draggable/)
* properties
* .lockAxis

On this page

# lockAxis

### lockAxis : Boolean

Locks movement to one axis based on the how it is moved initially.

### Details[​](#details "Direct link to Details")

*Boolean* - If `true`, dragging more than 2 pixels in either direction (horizontally or vertically) will lock movement into that axis so that the element can only be dragged that direction (horizontally or vertically, whichever had the most initial movement). No diagonal movement will be allowed. Obviously this is only applicable for `type: "x,y"` and `type: "top,left"` and `type: "scroll"` Draggables. If you only want to allow vertical movement, you should set the `type` to `"y"`, `"top"`, or `"scrollTop"`. If you only want to allow horizontal movement, you should set the `type` to `"x"`, `"left"`, or `"scrollLeft"`.