---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/endTime()"
title: "endTime | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:11:25.298665Z"
selector: "article"
---

# endTime | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .endTime()

On this page

# endTime

### endTime( includeRepeats:Boolean ) : [Number | self]

Returns the time at which the animation will finish according to the parent timeline's local time.

#### Parameters

* #### **includeRepeats**: Boolean

  (default = `true`) - by default, repeats are included when calculating the end time but you can pass `false` to prevent that.

### Returns : [Number | self][​](#returns--number--self "Direct link to Returns : [Number | self]")

The end time of the timeline according to its parent timeline.

### Details[​](#details "Direct link to Details")

Returns the time at which the animation will finish according to the parent timeline's local time. This does factor in the `timeScale`. For example:

```
var tl = gsap.timeline();  
  
//create a 1-second tween  
var tween = gsap.to(e, { duration: 1, x: 100 });  
  
//insert the tween at 0.5 seconds into the timeline  
tl.add(tween, 0.5);  
  
console.log(tween.endTime()); //1.5  
  
//double the speed of the tween, thus it'll finish in half the normal time  
tween.timeScale(2);  
  
console.log(tween.endTime()); //1
```