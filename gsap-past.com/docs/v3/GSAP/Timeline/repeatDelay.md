---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/repeatDelay()"
title: "repeatDelay | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:12:01.156473Z"
selector: "article"
---

# repeatDelay | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .repeatDelay()

On this page

# repeatDelay

### repeatDelay( value:Number ) : [Number | self]

Gets or sets the amount of time in seconds between repeats.

#### Parameters

* #### **value**: Number

  (default = `0`) - Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Returns : [Number | self][​](#returns--number--self "Direct link to Returns : [Number | self]")

Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Details[​](#details "Direct link to Details")

Gets or sets the number of times that the timeline should repeat after its first iteration.

For example, if `repeat` is 2 and `repeatDelay` is 1, the timeline will play initially, then wait for 1 second before it repeats, then play again, then wait 1 second again before doing its final repeat. You can set the initial `repeatDelay` value via the `vars` parameter, like:

```
var tl = gsap.timeline({ repeat: 2, repeatDelay: 1 });
```

This method serves as both a getter and setter. Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining, like `myTimeline.repeat(2).yoyo(true).play();`

```
//gets current repeat value  
var repeat = tl.repeatDelay();  
  
//sets repeat to 2  
tl.repeatDelay(2);
```