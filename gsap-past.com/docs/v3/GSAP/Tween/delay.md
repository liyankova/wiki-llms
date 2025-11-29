---
source_url: "https://gsap.com/docs/v3/GSAP/Tween/delay()"
title: "delay | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:10:24.910141Z"
selector: "article"
---

# delay | GSAP | Docs & Learning

* [Tween](/docs/v3/GSAP/Tween)
* methods
* .delay()

On this page

# delay

### delay( value:Number ) : [Number | self]

Gets or sets the animation's initial delay which is the length of time in seconds before the animation should begin.

#### Parameters

* #### **value**: Number

  (default = `NaN`) - Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Returns : [Number | self][​](#returns--number--self "Direct link to Returns : [Number | self]")

Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Details[​](#details "Direct link to Details")

Gets or sets the animation's initial `delay` which is the length of time in seconds before the animation should begin. A tween's starting values are not recorded until after the `delay` has expired (except in `from()` tweens which render immediately by default unless `immediateRender: false` is set in the `vars` parameter). An animation's `delay` is unaffected by its `timeScale`, so if you were to change `timeScale` from `1` to `10`, for example, it wouldn't cause the delay to grow tenfold.

This method serves as both a getter and setter. Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining, like `myAnimation.delay(2).timeScale(0.5).restart(true);`

```
var currentDelay = myAnimation.delay(); //gets current delay  
myAnimation.delay(2); //sets delay
```