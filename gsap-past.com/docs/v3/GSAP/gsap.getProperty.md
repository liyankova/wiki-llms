---
source_url: "https://gsap.com/docs/v3/GSAP/gsap.getProperty()"
title: "gsap.getProperty() | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:55:22.413596Z"
selector: "article"
---

# gsap.getProperty() | GSAP | Docs & Learning

* [GSAP](/docs/v3/GSAP/)
* methods
* gsap.getProperty()

On this page

### Returns : \*[​](#returns-- "Direct link to Returns : *")

Returns the value of the property requested as a number (if possible) unless you specify a unit in which case it will be added to the number, making it a string. Returns `null` if it doesn't exist.

```
gsap.getProperty("#id", "x"); // 20  
gsap.getProperty("#id", "x", "px"); // "20px"  
gsap.getProperty("#id", "backgroundColor"); // "rgb(255, 128, 0)"
```

### Details[​](#details "Direct link to Details")

`getProperty()` provides an easy way to get the current value of any property and if it's a DOM element, you can even have it convert into a particular unit! For DOM elements, it will check the following properties in this order (and return it as soon as one is found): the element's inline CSS, the element's `.getComputedStyle()` CSS, a property on the element itself like (`element.property`), an attribute on the element (like `element.getAttribute(property)`). Returns `null` if it doesn't exist.

If you omit the unit parameter, it will return a **NUMBER** (at least for simple values where `parseFloat()` returns a number). For example, a "top" or "left" or "x" property that's technically "20px" would be returned as 20 (no unit suffix) because it's so common to need to deal with numbers in animation. In practical use, it would be annoying to get values like "20px" back from getProperty() and have to manually wrap it in `parseFloat()`. But again, if you want the unit included, just pass in that unit like `gsap.getProperty("#element", "x", "px")` and it will return a string accordingly.

### Examples:[​](#examples "Direct link to Examples:")

```
let w = gsap.getProperty("#id", "width"); //you can use selector text  
let bgColor = gsap.getProperty(element, "backgroundColor");  
  
// convert into a specific unit, like em  
let emWidth = gsap.getProperty(element, "width", "em");
```

## Reusable getter function[​](#reusable-getter-function "Direct link to Reusable getter function")

If you omit the `property` parameter, `gsap.getProperty()` will return a getter function that you can reuse to grab properties of that target object:

```
let getter = gsap.getProperty("#id");  
var x = getter("x"),  
  y = getter("y", "em"); //in em units
```