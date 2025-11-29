---
source_url: "https://gsap.com/docs/v3/GSAP/UtilityMethods/toArray()/"
title: "toArray | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:54:02.410458Z"
selector: "article"
---

# toArray | GSAP | Docs & Learning

* [Utility Methods](/docs/v3/GSAP/UtilityMethods)
* toArray

On this page

### Returns : Array[​](#returns--array "Direct link to Returns : Array")

---

Converts selector text, an Array of objects or selector text, a NodeList, an object, or almost any Array-like object into a flat `Array`. You can optionally define a scope (added in 3.7.0) for the selector text which limits results to descendants of that scope Element.

```
// these all return the corresponding elements wrapped in a flat Array:  
  
// selector text (returns the raw elements wrapped in an Array)  
let targets = gsap.utils.toArray(".class");  
  
// raw element/object  
let targets = gsap.utils.toArray(myElement);  
  
// Array of selector text (same result as ".class1, .class2")  
let targets = gsap.utils.toArray([".class1", ".class2"]);  
  
// Only descendant elements of myElement  
let targets = gsap.utils.toArray(".class", myElement);
```

## Parameters[​](#parameters "Direct link to Parameters")

1. **targets** : [Object | String | NodeList | Array] - The target(s) that you want wrapped in a flattened Array (it can be selector text, objects, NodeList, etc.)
2. **scope** : [Element | Ref] (optional) - The Element (or React ref) to which the selector text scope should be limited, like calling `.querySelectorAll([selector-text])` on this Element rather than the document. In other words, it will only return **descendant** Elements of the scope Element. This is only helpful when `targets` is selector text.