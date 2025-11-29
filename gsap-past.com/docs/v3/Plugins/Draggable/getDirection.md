---
source_url: "https://gsap.com/docs/v3/Plugins/Draggable/getDirection()"
title: "getDirection | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:18:10.255985Z"
selector: "article"
---

# getDirection | GSAP | Docs & Learning

* more plugins
* [Draggable](/docs/v3/Plugins/Draggable/)
* methods
* .getDirection()

On this page

# getDirection

### getDirection( from:String | Element ) : String

Returns the `direction` (`"right"` | `"left"` | `"up"` | `"down"` | `"left-up"` | `"left-down"` | `"right-up"` | `"right-down"`) as measured from either where the drag started (the default) or the moment-by-moment velocity, or its proximity to another element that you define.

#### Parameters

* #### **from**: String | Element

  Any of the the following can be used:

### Returns : String[​](#returns--string "Direct link to Returns : String")

The direction of the Draggable instance.

### Details[​](#details "Direct link to Details")

Sometimes it's useful to know which direction an element is dragged (`"left"` | `"right"` | `"up"` | `"down"` | `"left-up"` | `"left-down"` | `"right-up"` | `"right-down"`), or maybe you'd like to know which direction it is compared to another element. That's precisely what `getDirection()` is for. You can pass any of the following as the parameter to control its behavior:

* `"start"` (the default) - Measures from wherever the drag began.
* `"velocity"` (**requires**[InertiaPlugin](/docs/v3/Plugins/InertiaPlugin/)!) - Measures the moment-by-moment direction of the drag. For example, maybe the user dragged really far to the right, but then they start dragging to the left for a brief moment - it's still to the right of the starting position, but it's current velocity is moving to the left. That's what `velocity` measures.
* `[element]` - If you pass an element, it'll return the direction from that element's center to the Draggable's center.

#### loading...