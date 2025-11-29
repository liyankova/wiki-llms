---
source_url: "https://gsap.com/docs/v3/Plugins/Draggable/y"
title: "y | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:17:48.061746Z"
selector: "article"
---

# y | GSAP | Docs & Learning

* more plugins
* [Draggable](/docs/v3/Plugins/Draggable/)
* properties
* .y

On this page

# y

### y : Number

[read-only] The current y (vertical) position of the Draggable instance.

### Details[​](#details "Direct link to Details")

*Number* - The current y (vertical) position of the Draggable instance. For a Draggable of `type: "x,y"`, it would be the `y` transform translation, as in the CSS `transform: translateY(...)`. For `type: "top,left"`, the Draggable's `y` would refer to the CSS `top` value that's applied. This is not the global coordinate - it is the inline CSS-related value applied to the element.

This value is updated each time the Draggable is dragged interactively and during the momentum-based tween that Draggable applies when the user releases their mouse/touch, but if you manually change (or tween) the element's position you can force Draggable to look at the "real" value and record it to its own `y` property by calling the Draggable's `update()` method. Basically that re-synchronizes it. Again, this is not necessary unless other code (outside Draggable) alters the target element's position.