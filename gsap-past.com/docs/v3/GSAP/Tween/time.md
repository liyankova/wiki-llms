---
source_url: "https://gsap.com/docs/v3/GSAP/Tween/time()"
title: "time | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:57:09.860105Z"
selector: "article"
---

# time | GSAP | Docs & Learning

* [Tween](/docs/v3/GSAP/Tween)
* methods
* .time()

On this page

# time

### time( value:Number, suppressEvents:Boolean ) : [Number | self]

[override] Gets or sets the local position of the playhead (essentially the current time), not including any repeats or repeatDelays.

#### Parameters

* #### **value**: Number

  (default = `NaN`) - Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining. Negative values will be interpreted from the **END** of the animation.
* #### **suppressEvents**: Boolean

  (default = `false`) - If `true`, no events or callbacks will be triggered when the playhead moves to the new position defined in the `value` parameter.

### Returns : [Number | self][​](#returns--number--self "Direct link to Returns : [Number | self]")

Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Details[​](#details "Direct link to Details")

Gets or sets the local position of the playhead (essentially the current time), **not** including any repeats or repeatDelays. If the tween has a non-zero `repeat`, its `time` goes back to zero upon repeating even though the `totalTime` continues forward linearly (or if `yoyo` is `true`, the `time` alternates between moving forward and backward). `time` never exceeds the duration whereas the `totalTime` reflects the overall time including any repeats and repeatDelays.

For example, if a tween has a `duration` of 2 and a repeat of 3, `totalTime` will go from 0 to 8 during the course of the tween (plays once then repeats 3 times, making 4 total cycles) whereas `time` would go from 0 to 2 a total of 4 times.

This method serves as both a getter and setter. Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

```
//gets current time  
var currentTime = myTween.time();  
  
//sets time, jumping to new value just like seek()  
myTween.time(2);
```