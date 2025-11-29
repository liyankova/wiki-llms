---
source_url: "https://gsap.com/docs/v3/Plugins/Draggable/enabled()"
title: "enabled | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:18:03.880003Z"
selector: "article"
---

# enabled | GSAP | Docs & Learning

* more plugins
* [Draggable](/docs/v3/Plugins/Draggable/)
* methods
* .enabled()

On this page

# enabled

### enabled( value:Boolean ) : Boolean

Gets or sets the enabled state.

#### Parameters

* #### **value**: Boolean

  Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Returns : Boolean[​](#returns--boolean "Direct link to Returns : Boolean")

Returns `true` if the Draggable instance is able to be dragged (`false` if not).

### Details[​](#details "Direct link to Details")

Gets or sets the enabled state. Omitting the `value` parameter returns the current enabled value (getter), whereas defining the parameter sets the enabled value (setter). When a Draggable instance is enabled it responds to mouse events, fires callbacks and can be dragged.