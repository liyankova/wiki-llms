---
source_url: "https://gsap.com/docs/v3/Plugins/Draggable/startX"
title: "startX | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:17:35.842747Z"
selector: "article"
---

# startX | GSAP | Docs & Learning

* more plugins
* [Draggable](/docs/v3/Plugins/Draggable/)
* properties
* .startX

On this page

# startX

### startX : Number

[read-only] The starting `x` (horizontal) position of the Draggable instance when the most recent drag began.

### Details[​](#details "Direct link to Details")

[read-only] The starting `x` (horizontal) position of the Draggable instance when the most recent drag began. For a Draggable of `type: "x,y"`, it would be the `x` transform translation, as in the CSS `transform: translateX(...)`. For `type: "top,left"`, the Draggable's `x` would refer to the CSS `left` value that's applied. For `type: "rotation"` it's the rotation (in degrees). This is not the global coordinate - it is the inline CSS-related value applied to the element.