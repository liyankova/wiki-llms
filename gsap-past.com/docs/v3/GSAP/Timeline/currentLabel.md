---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/currentLabel()"
title: "currentLabel | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:11:19.758329Z"
selector: "article"
---

# currentLabel | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .currentLabel()

On this page

# currentLabel

### currentLabel( value:String ) : [String | self]

Gets the closest label that is at or before the current time, or jumps to a provided label (behavior depends on whether or not you pass a parameter to the method).

#### Parameters

* #### **value**: String

  (default = `null`) - Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Returns : [String | self][​](#returns--string--self "Direct link to Returns : [String | self]")

Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.

### Details[​](#details "Direct link to Details")

Gets the closest label that is at or before the current time, or jumps to a provided label (behavior depends on whether or not you pass a parameter to the method).

This method serves as both a getter and setter. Omitting the parameter returns the current value (getter), whereas defining the parameter sets the value (setter) and returns the instance itself for easier chaining.