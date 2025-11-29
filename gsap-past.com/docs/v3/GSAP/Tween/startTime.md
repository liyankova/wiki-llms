---
source_url: "https://gsap.com/docs/v3/GSAP/Tween/startTime()"
title: "startTime | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:56:24.313400Z"
selector: "article"
---

# startTime | GSAP | Docs & Learning

* [Tween](/docs/v3/GSAP/Tween)
* methods
* .startTime()

On this page

# startTime

### startTime( value:Number ) : [Number | self]

Gets or sets the time at which the animation begins on its parent timeline (after any delay that was defined).

#### Parameters

* #### **value**: Number

  (default = `NaN`) - Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Returns : [Number | self][​](#returns--number--self "Direct link to Returns : [Number | self]")

Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Details[​](#details "Direct link to Details")

Gets or sets the time at which the animation begins on its parent timeline (after any `delay` that was defined). For example, if a tween starts at exactly 3 seconds into the timeline on which it is placed, the tween's `startTime` would be 3.

The `startTime` may be automatically adjusted to make the timing appear seamless if the parent timeline's `smoothChildTiming` property is `true` and a timing-dependent change is made on-the-fly, like `reverse()` is called or `timeScale()` is changed, etc. See the documentation for the `smoothChildTiming` property of timelines for more details.

This method serves as both a getter and setter. Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

```
//gets current start time  
var start = myAnimation.startTime();  
  
//sets the start time  
myAnimation.startTime(2);
```