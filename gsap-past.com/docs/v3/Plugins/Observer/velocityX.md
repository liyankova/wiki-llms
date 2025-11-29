---
source_url: "https://gsap.com/docs/v3/Plugins/Observer/velocityX"
title: "velocityX | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:20:17.605051Z"
selector: "article"
---

# velocityX | GSAP | Docs & Learning

* more plugins
* [Observer](/docs/v3/Plugins/Observer/)
* properties
* .velocityX

On this page

# velocityX

### velocityX : Number

The horizontal velocity (in pixels per second).

### Details[​](#details "Direct link to Details")

The horizontal velocity (in pixels per second).

This is only affected by the event types that the Observer is watching. So, for example, `type: "wheel,touch"` would track the velocity based on wheel and touch events (not pointer or scroll). By default, touch and pointer events are only tracked **while pressing/dragging** but if you define an `onMove` (which is mapped to "pointermove"/"mousemove" events), it'll be tracked during any movement while hovering over the target.