---
source_url: "https://gsap.com/docs/v3/Plugins/Flip/static.getState()"
title: "static-getState | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:15:31.215125Z"
selector: "article"
---

# static-getState | GSAP | Docs & Learning

* [Flip](/docs/v3/Plugins/Flip/)
* methods
* Flip.getState()

On this page

# Flip.getState

### Flip.getState( targets:String | Element | Array, vars:Object ) : Object

Captures information about the current state of the `targets` so that they can be Flipped later. By default, this information includes the dimensions, rotation, skew, opacity, and the position of the targets in the viewport. Other properties can be captured by configuring the `vars` parameter.

#### Parameters

* #### **targets**: String | Element | Array

  The targets that you want to Flip. This can be selector text like `".my-class"` or an Element or an Array of Elements or an Array of selector text.
* #### **vars**: Object

  (optional) A configuration object that contain properties like `props`, `simple`, `kill`, or `batch`.

### Returns : Object[​](#returns--object "Direct link to Returns : Object")

The saved state object that can be passed into a [Flip.from()](/docs/v3/Plugins/Flip/static.from()), [Flip.to()](/docs/v3/Plugins/Flip/static.to()), [Flip.fit()](/docs/v3/Plugins/Flip/static.fit()), etc.

### Details[​](#details "Direct link to Details")

Captures information about the current state of the targets so that they can be Flipped later. By default, this information includes the dimensions, rotation, skew, opacity, and the position of the targets in the viewport. If there are any in-progress flip animations that affect any of the targets, they will be forced to completion so that the final inline styles are recorded properly. But other than completing any in-progress flip animations, `getState()` doesn't alter anything; it's purely for reading/saving state-related information.

```
// capture state  
const state = Flip.getState(".details, .full-screen");  
  
// now alter the state by toggling a class:  
detailsElement.classList.toggle("active");  
  
// now do a "Flip" animation from the previous state to the new one:  
Flip.from(state, {  
  duration: 1,  
  ease: "power1.inOut",  
  absolute: true,  
});
```

## Configuration[​](#configuration "Direct link to Configuration")

The `Flip.getState()` vars object (2nd parameter) can contain any of the following optional properties:

| Property | Description |
| --- | --- |
| batch | String - if you'd like this state to get merged into a specific [batch](/docs/v3/Plugins/Flip/static.batch()) so that its `batch.state` acts as a central object with ALL the state data with that id, use the batch's id like `batch: "id"`. where the "id" is the arbitrary string you assigned to that batch. Then, you can get the merged state object like `Flip.batch("id").state`. To clear the data out of that object so that it's empty and starts fresh again, you can `Flip.batch("id").clear(true)`. Note that whenever `batch.getState()` or `batch.run()` is called on that particular batch instance (with the matching id), it will automatically clear its `batch.state` object first. Batching is an advanced feature that typically isn't required. *(added in 3.9.0)* |
| kill | Boolean - by default, any in-progress flip animations of any of the `targets` will be forced to completion and killed so that the final state is correctly recorded and the inline styles don't contaminate the new state (which is typically set immediately after a `getState()` call). The only exception is when the `getState()` is called from *within* a [batch()](/docs/v3/Plugins/Flip/static.batch()), in which case the killing happens after all the actions finish their `getState()`). You can override this behavior by setting `kill: false` so that you can then manually [killFlipsOf()](/docs/v3/Plugins/Flip/static.killFlipsOf()) right before you set your new state. It's quite uncommon that you'd need to do this - normally Flip's defaults are ideal. *(added in 3.9.0)* |
| props | String - a comma-delimited list of *camelCased* CSS properties that should be recorded beyond the standard positioning/size ones. For example, `"backgroundColor,color"`. The following information is **always** recorded: transforms (like x, y, scaleX, scaleY, rotation, skewX), width, height, and opacity. |
| simple | Boolean - if `true`, Flip will skip the extra calculations that would be necessary to accommodate rotation/scale/skew in determining positions. It's like telling Flip *"I promise that there aren't any rotated/scaled/skewed containers for the Flipping elements"* which makes things **faster**. In most cases, the performance difference isn't noticeable, but if you're flipping a lot of elements it can help keep things snappy. |

### Example[​](#example "Direct link to Example")

```
// capture state  
const state = Flip.getState(".details, .full-screen", {  
  props: "backgroundColor,color",  
  simple: true,  
});
```