---
source_url: "https://gsap.com/docs/v3/GSAP/Tween/reversed()"
title: "reversed | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:10:44.368020Z"
selector: "article"
---

# reversed | GSAP | Docs & Learning

* [Tween](/docs/v3/GSAP/Tween)
* methods
* .reversed()

On this page

# reversed

### reversed( value:Boolean ) : [Boolean | self]

Gets or sets the animation's reversed state which indicates whether or not the animation should be played backwards.

#### Parameters

* #### **value**: Boolean

  (default = `false`) - Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Returns : [Boolean | self][​](#returns--boolean--self "Direct link to Returns : [Boolean | self]")

Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Details[​](#details "Direct link to Details")

Gets or sets the animation's reversed state which indicates whether or not the animation should be played backwards. This value is not affected by `yoyo` repeats and it does not take into account the reversed state of ancestor timelines. So for example, a tween that is not reversed might appear reversed if its parent timeline (or any ancestor timeline) is reversed.

This method serves as both a getter and setter. Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

```
//gets current orientation  
var rev = myAnimation.reversed();  
  
//sets the orientation to reversed  
myAnimation.reversed(true);  
  
//toggles the orientation  
myAnimation.reversed(!myAnimation.reversed());
```