---
source_url: "https://gsap.com/docs/v3/GSAP/Tween/repeatDelay()"
title: "repeatDelay | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:10:42.503097Z"
selector: "article"
---

# repeatDelay | GSAP | Docs & Learning

* [Tween](/docs/v3/GSAP/Tween)
* methods
* .repeatDelay()

On this page

# repeatDelay

### repeatDelay( value:Number ) : [Number | self]

Gets or sets the amount of time in seconds between repeats.

#### Parameters

* #### **value**: Number

  (default = `NaN`) - Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Returns : [Number | self][​](#returns--number--self "Direct link to Returns : [Number | self]")

Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Details[​](#details "Direct link to Details")

Gets or sets the amount of time in seconds between repeats. For example, if `repeat` is 2 and `repeatDelay` is 1, the tween will play initially, then wait for 1 second before it repeats, then play again, then wait 1 second again before doing its final repeat. You can set the initial `repeatDelay` value via the `vars` parameter, like: `gsap.to(obj, {duration: 1, x: 100, repeat: 2, repeatDelay: 1});`

This method serves as both a getter and setter. Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining, like `myTween.repeat(2).yoyo(true).repeatDelay(0.5).play();`

```
//gets current repeatDelay value  
var repeatDelay = myTween.repeatDelay();  
  
//sets repeatDelay to 2  
myTween.repeatDelay(2);
```