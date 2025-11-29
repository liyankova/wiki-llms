---
source_url: "https://gsap.com/docs/v3/Plugins/Draggable/startY"
title: "startY | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:17:37.821828Z"
selector: "article"
---

# startY | GSAP | Docs & Learning

* more plugins
* [Draggable](/docs/v3/Plugins/Draggable/)
* properties
* .startY

On this page

# startY

### startY : Number

[read-only] The starting `y` (vertical) position of the Draggable instance when the most recent drag began.

### Details[​](#details "Direct link to Details")

[read-only] The starting `y` (vertical) position of the Draggable instance when the most recent drag began. For a Draggable of `type: "x,y"`, it would be the `y` transform translation, as in the CSS `transform: translateY(...)`. For `type: "top,left"`, the Draggable's `y` would refer to the CSS `top` value that's applied. This is not the global coordinate - it is the inline CSS-related value applied to the element.