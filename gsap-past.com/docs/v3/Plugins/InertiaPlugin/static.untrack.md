---
source_url: "https://gsap.com/docs/v3/Plugins/InertiaPlugin/static.untrack()"
title: "static-untrack | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:19:48.532305Z"
selector: "article"
---

# static-untrack | GSAP | Docs & Learning

* more plugins
* [Inertia](/docs/v3/Plugins/InertiaPlugin/)
* methods
* InertiaPlugin.untrack()

On this page

# InertiaPlugin.untrack

### InertiaPlugin.untrack( target:Element | String | Array, props:String ) ;

#### Parameters

* #### **target**: Element | String | Array

  The Element(s) whose properties should not be tracked anymore. This can be an Element, selector text, or an Array fo Elements.
* #### **props**: String

  A comma-delimited list of property names that should be untracked, like `"x"` or `"x,y,rotation"`

### Details[​](#details "Direct link to Details")

Stops tracking the `velocity` of certain properties (or all properties of an object), like ones initiated with the `track()` method.

```
//starts tracking "x" and "y":  
InertiaPlugin.track(obj, "x,y");  
  
//stops tracking only the "x" property:  
InertiaPlugin.untrack(obj, "x");  
  
//stops tracking "x" and "y":  
InertiaPlugin.untrack(obj, "x,y");  
  
//stops tracking all properties of obj:  
InertiaPlugin.untrack(obj);
```