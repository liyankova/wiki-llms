---
source_url: "https://gsap.com/docs/v3/GSAP/Tween/totalDuration()"
title: "totalDuration | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:10:51.833174Z"
selector: "article"
---

# totalDuration | GSAP | Docs & Learning

* [Tween](/docs/v3/GSAP/Tween)
* methods
* .totalDuration()

On this page

# totalDuration

### totalDuration( value:Number ) : [Number | self]

[override] Gets or sets the total duration of the tween in seconds including any repeats or repeatDelays.

#### Parameters

* #### **value**: Number

  (default = `NaN`) - Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Returns : [Number | self][​](#returns--number--self "Direct link to Returns : [Number | self]")

Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Details[​](#details "Direct link to Details")

Gets or sets the total duration of the tween in seconds including any repeats or repeatDelays. `duration`, by contrast, does **NOT** include repeats and repeatDelays. For example, if the tween has a `duration` of 10, a `repeat` of 1 and a `repeatDelay` of 2, the `totalDuration` would be 22.

This method serves as both a getter and setter. Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

```
//gets total duration  
var total = myTween.totalDuration();  
  
//sets the total duration  
myTween.totalDuration(10);
```