---
source_url: "https://gsap.com/docs/v3/Plugins/Observer/deltaX"
title: "deltaX | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:19:54.560800Z"
selector: "article"
---

# deltaX | GSAP | Docs & Learning

* more plugins
* [Observer](/docs/v3/Plugins/Observer/)
* properties
* .deltaX

On this page

# deltaX

### deltaX : Number

The amount of change (in pixels) horizontally since the last time a callback was fired on that axis. For example, `onChangeX` or `onRight`

### Details[​](#details "Direct link to Details")

The amount of change (in pixels) horizontally since the last time a callback was fired on that axis. For example, `onChangeX` or `onRight`

This is only affected by the event types that the Observer is watching. So, for example, `type: "wheel,touch"` would track the delta based on wheel and touch events (not pointer or scroll). By default, touch and pointer events are only tracked **while pressing/dragging** but if you define an `onMove` (which is mapped to "pointermove"/"mousemove" events), it'll be tracked during any movement while hovering over the target.