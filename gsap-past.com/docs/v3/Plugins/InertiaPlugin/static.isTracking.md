---
source_url: "https://gsap.com/docs/v3/Plugins/InertiaPlugin/static.isTracking()"
title: "static-isTracking | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:19:44.030107Z"
selector: "article"
---

# static-isTracking | GSAP | Docs & Learning

* more plugins
* [Inertia](/docs/v3/Plugins/InertiaPlugin/)
* methods
* InertiaPlugin.isTracking()

On this page

# InertiaPlugin.isTracking

### InertiaPlugin.isTracking( target:Element | String, property:String ) : Boolean

#### Parameters

* #### **target**: Element | String

  The Element whose property may be tracked. This can be selector text or an Element.
* #### **property**: String

  The name of the property, like `"x"` or `"y"`

### Returns : Boolean[​](#returns--boolean "Direct link to Returns : Boolean")

`true` if the target or property is being tracked, `false` if not.

### Details[​](#details "Direct link to Details")

Allows you to discern whether the velocity of a particular target or one of its properties is being tracked (typically initiated using the `track()` method).