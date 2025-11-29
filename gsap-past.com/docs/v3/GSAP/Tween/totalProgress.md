---
source_url: "https://gsap.com/docs/v3/GSAP/Tween/totalProgress()"
title: "totalProgress | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:10:53.666042Z"
selector: "article"
---

# totalProgress | GSAP | Docs & Learning

* [Tween](/docs/v3/GSAP/Tween)
* methods
* .totalProgress()

On this page

# totalProgress

### totalProgress( value:Number, suppressEvents:Boolean ) : [Number | self]

[override] Gets or sets the tween's totalProgress which is a value between 0 and 1 indicating the position of the virtual playhead (including repeats) where 0 is at the beginning, 0.5 is halfway complete, and 1 is complete.

#### Parameters

* #### **value**: Number

  (default = `NaN`) - Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.
* #### **suppressEvents**: Boolean

  (default = `false`) - If `true`, no events or callbacks will be triggered when the playhead moves to the new position.

### Returns : [Number | self][​](#returns--number--self "Direct link to Returns : [Number | self]")

Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Details[​](#details "Direct link to Details")

Gets or sets the tween's totalProgress which is a value between 0 and 1 indicating the position of the virtual playhead (**including repeats**) where 0 is at the beginning, 0.5 is halfway complete, and 1 is complete.

```
//gets current total progress  
var progress = myTween.totalProgress();  
  
//sets total progress to one quarter finished  
myTween.totalProgress(0.25);
```