---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/yoyo()"
title: "yoyo | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:12:30.216048Z"
selector: "article"
---

# yoyo | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .yoyo()

On this page

# yoyo

### yoyo( value:Boolean ) : [Boolean | self]

Gets or sets the timeline's yoyo state, where true causes the timeline to go back and forth, alternating backward and forward on each repeat.

#### Parameters

* #### **value**: Boolean

  (default = `false`) - Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Returns : [Boolean | self][​](#returns--boolean--self "Direct link to Returns : [Boolean | self]")

Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Details[​](#details "Direct link to Details")

Gets or sets the timeline's `yoyo` state, where `true` causes the timeline to go back and forth, alternating backward and forward on each repeat. `yoyo` works in conjunction with `repeat`, where `repeat` controls how many times the timeline repeats, and `yoyo` controls whether or not each repeat alternates direction. So in order to make a timeline `yoyo`, you must set its `repeat` to a non-zero value.

Yoyo-ing, has no affect on the timeline's `reversed` property. For example, if `repeat` is 2 and `yoyo` is `false`, it will look like: start - 1 - 2 - 3 - 1 - 2 - 3 - 1 - 2 - 3 - end. But if `yoyo` is `true`, it will look like: start - 1 - 2 - 3 - 3 - 2 - 1 - 1 - 2 - 3 - end.

You can set the `yoyo` property initially by passing `yoyo: true` in the `vars` parameter, like: `gsap.timeline({repeat: 1, yoyo: true});`

This method serves as both a getter and setter. Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining, like `myTimeline.yoyo(true).repeat(3).timeScale(2).play(0.5);`

```
//gets current yoyo state  
var yoyo = tl.yoyo();  
  
//sets yoyo to true  
tl.yoyo(true);
```