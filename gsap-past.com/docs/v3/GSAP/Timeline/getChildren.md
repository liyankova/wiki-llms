---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/getChildren()"
title: "getChildren | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:11:30.824968Z"
selector: "article"
---

# getChildren | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .getChildren()

On this page

# getChildren

### getChildren( nested:Boolean, tweens:Boolean, timelines:Boolean, ignoreBeforeTime:Number ) : Array

Returns an array containing all the tweens and/or timelines nested in this timeline.

#### Parameters

* #### **nested**: Boolean

  (default = `true`) - Determines whether or not tweens and/or timelines that are inside nested timelines should be returned. If you only want the "top level" tweens and timelines, set this to `false`.
* #### **tweens**: Boolean

  (default = `true`) - Determines whether or not tweens should be included in the results.
* #### **timelines**: Boolean

  (default = `true`) - Determines whether or not timelines should be included in the results.
* #### **ignoreBeforeTime**: Number

  `Number` (default = `-Infinity`) - All children with start times that are less than this value will be ignored.

### Returns : Array[​](#returns--array "Direct link to Returns : Array")

An Array of child tweens and timelines.

### Details[​](#details "Direct link to Details")

Returns an array containing all the tweens and/or timelines nested in this timeline that match the provided criteria. Callbacks (delayed calls) are considered zero-duration tweens.

```
//first, let's set up a master timeline and nested timeline:  
var master = gsap.timeline({ defaults: { duration: 1 } }),  
  nested = gsap.timeline();  
  
//drop 2 tweens into the nested timeline  
nested.to("#e1", { duration: 1, x: 100 }).to("#e2", { duration: 2, y: 200 });  
  
//drop 3 tweens into the master timeline  
master  
  .to("#e3", { top: 200 })  
  .to("#e4", { left: 100 })  
  .to("#e5", { backgroundColor: "red" });  
  
//nest the timeline:  
master.add(nested);  
  
//get only the direct children of the master timeline:  
var children = master.getChildren(false, true, true);  
  
console.log(children.length); //"3" (2 tweens and 1 timeline)  
  
//get all of the tweens/timelines (including nested ones) that occur AFTER 0.5 seconds  
children = master.getChildren(true, true, true, 0.5);  
  
console.log(children.length); //"5" (4 tweens and 1 timeline)  
  
//get only tweens (not timelines) of master (including nested tweens):  
children = master.getChildren(true, true, false);  
  
console.log(children.length); //"5" (5 tweens)
```