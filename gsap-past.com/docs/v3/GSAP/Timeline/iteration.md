---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/iteration()"
title: "iteration | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:11:40.564587Z"
selector: "article"
---

# iteration | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .iteration()

On this page

# iteration

### iteration( value:Number ) : [Number | self]

Gets or sets the iteration (the current repeat) of timelines.

#### Parameters

* #### **value**: Number

  The `repeat` to jump to.

### Returns : [Number | self][​](#returns--number--self "Direct link to Returns : [Number | self]")

Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Details[​](#details "Direct link to Details")

Gets or sets the iteration (on a repeated timeline). For example, iteration is `1` the very first time through, then on the first repeat, the iteration would be `2`, then `3`, etc.

Setting the iteration will cause the timeline to go to the iteration provided. For example, if the `repeat` is 4, and the playhead is currently on its third repeat, `.iteration(2)` will make the timeline jump back to the second iteration.

```
//gets current iteration  
var progress = tl.iteration();  
  
//sets iteration the second iteration  
tl.iteration(2);
```