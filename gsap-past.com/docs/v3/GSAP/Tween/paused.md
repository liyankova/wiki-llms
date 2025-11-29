---
source_url: "https://gsap.com/docs/v3/GSAP/Tween/paused()"
title: "paused | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:10:38.819606Z"
selector: "article"
---

# paused | GSAP | Docs & Learning

* [Tween](/docs/v3/GSAP/Tween)
* methods
* .paused()

On this page

# paused

### paused( value:Boolean ) : [Boolean | self]

Gets or sets the animation's paused state which indicates whether or not the animation is currently paused.

#### Parameters

* #### **value**: Boolean

  (default = `false`) - Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Returns : [Boolean | self][​](#returns--boolean--self "Direct link to Returns : [Boolean | self]")

Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Details[​](#details "Direct link to Details")

Gets or sets the animation's paused state which indicates whether or not the animation is currently paused. This does not take into account anscestor timelines. So for example, a tween that is not paused might appear paused if its parent timeline (or any ancenstor timeline) is paused. Pausing an animation doesn't remove it from its parent timeline, but it does cause it not to be factored into the parent timeline's `duration`/`totalDuration`. When an animation completes, it does NOT alter its paused state.

In most cases, it is easiest to use the `pause()` method to pause the animation, and `resume()` to resume it. But to check the current state, you must use the `paused()` method. It can also be useful for toggling like `myAnimation.paused( !myAnimation.paused() );`

You can set the `paused` state initially by passing `paused: true` in the `vars` parameter.

This method serves as both a getter and setter. Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining, like `myAnimation.paused(true).delay(2).timeScale(0.5);`

```
//gets current paused state  
var paused = myAnimation.paused();  
  
//sets paused state to true (just like pause())  
myAnimation.paused(true);  
  
//toggles the paused state  
myAnimation.paused(!myAnimation.paused());
```