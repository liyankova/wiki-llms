---
source_url: "https://gsap.com/docs/v3/GSAP/Tween/duration()"
title: "duration | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:57:12.539302Z"
selector: "article"
---

# duration | GSAP | Docs & Learning

* [Tween](/docs/v3/GSAP/Tween)
* methods
* .duration()

On this page

# duration

### duration( value:Number ) : [Number | self]

Gets or sets the animation's duration, not including any repeats or repeatDelays.

#### Parameters

* #### **value**: Number

  (default = `NaN`) - Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Returns : [Number | self][​](#returns--number--self "Direct link to Returns : [Number | self]")

Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Details[​](#details "Direct link to Details")

Gets or sets the animation's `duration`, not including any `repeat`s or `repeatDelay`s. For example, if a tween has a `duration` of 2 and a `repeat` of 3, its `totalDuration` would be 8 (one standard play plus 3 repeats equals 4 total cycles).

This method serves as both a getter and setter. Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining, like `myAnimation.duration(2).delay(0.5).play(1);`

```
var currentDuration = myAnimation.duration(); //gets current durationmyAnimation.duration(2); //sets duration
```