---
source_url: "https://gsap.com/docs/v3/GSAP/Tween/totalTime()"
title: "totalTime | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:10:55.530553Z"
selector: "article"
---

# totalTime | GSAP | Docs & Learning

* [Tween](/docs/v3/GSAP/Tween)
* methods
* .totalTime()

On this page

# totalTime

### totalTime( time:Number, suppressEvents:Boolean ) : [Number | self]

Gets or sets the position of the playhead according to the totalDuration which includes any repeats and repeatDelays.

#### Parameters

* #### **time**: Number

  (default = `NaN`) - Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining. Negative values will be interpreted from the **END** of the animation.
* #### **suppressEvents**: Boolean

  (default = `false`) - If `true`, no events or callbacks will be triggered when the playhead moves to the new position defined in the `time` parameter.

### Returns : [Number | self][​](#returns--number--self "Direct link to Returns : [Number | self]")

Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Details[​](#details "Direct link to Details")

Gets or sets the position of the playhead according to the `totalDuration` which **includes any repeats and repeatDelays**. For example, if a tween has a `duration` of 2 and a `repeat` of 3, `totalTime` will go from 0 to 8 during the course of the tween (plays once then repeats 3 times, making 4 total cycles) whereas `time` will go from 0 to 2 a total of 4 times. If you added a `repeatDelay` of 1, that would make the `totalTime` go from 0 to 11 over the course of the tween.

This method serves as both a getter and setter. Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

`totalTime` will never exceed the `totalDuration`, nor will it be less than 0 (values will be clipped appropriately). Negative values will be interpreted from the **END** of the animation. For example, -2 would be 2 seconds before the end. If the animation's `totalDuration` is 6 and you do `myAnimation.totalTime(-2)`, it will jump to a `totalTime` of 4.

```
//gets total time  
var totalTime = myAnimation.totalTime();  
  
//sets total time, jumping to new value just like seek().  
myAnimation.totalTime(2);
```