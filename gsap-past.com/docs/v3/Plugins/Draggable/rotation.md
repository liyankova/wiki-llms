---
source_url: "https://gsap.com/docs/v3/Plugins/Draggable/rotation"
title: "rotation | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:17:33.821387Z"
selector: "article"
---

# rotation | GSAP | Docs & Learning

* more plugins
* [Draggable](/docs/v3/Plugins/Draggable/)
* properties
* .rotation

On this page

# rotation

### rotation : Number

[read-only] [only applies to `type: "rotation"`] The current rotation (in degrees) of the Draggable instance.

### Details[​](#details "Direct link to Details")

*Number* - [only applies to `type: "rotation"`] The current rotation (in degrees) of the Draggable instance. This is the rotation transform, as in the CSS `transform: rotate(...deg)`. This value is updated each time the Draggable is dragged interactively and during the momentum-based tween that Draggable applies when the user releases their mouse/touch, but if you manually change (or tween) the element's rotation you can force Draggable to look at the "real" value and record it to its own `x` property by calling the Draggable's `update()` method. Basically that re-synchronizes it. Again, this is not necessary unless other code (outside Draggable) alters the target element's position.