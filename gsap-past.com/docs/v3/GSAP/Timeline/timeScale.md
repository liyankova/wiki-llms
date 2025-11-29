---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/timeScale()"
title: "timeScale | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:56:18.758120Z"
selector: "article"
---

# timeScale | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .timeScale()

On this page

# timeScale

### timeScale( value:Number ) : [Number | self]

Factor that's used to scale time in the animation where 1 = normal speed (the default), 0.5 = half speed, 2 = double speed, etc.

#### Parameters

* #### **value**: Number

  (default = `NaN`) - Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Returns : [Number | self][​](#returns--number--self "Direct link to Returns : [Number | self]")

Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Details[​](#details "Direct link to Details")

Factor that's used to scale time in the animation where 1 = normal speed (the default), 0.5 = half speed, 2 = double speed, -1 = go backwards at normal speed, etc. For example, if an animation's `duration` is 2 but its `timeScale` is 0.5, it will take 4 seconds to finish. If you nest that animation in a timeline whose `timeScale` is 0.5 as well, it would take 8 seconds to finish. You can even tween the `timeScale` to gradually slow it down or speed it up.

This method serves as both a getter and setter. Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining, like `myAnimation.timeScale(2).play(1);`

```
//gets current timeScale  
var currentTimeScale = tl.timeScale();  
  
//sets timeScale to half-speed  
tl.timeScale(0.5);
```