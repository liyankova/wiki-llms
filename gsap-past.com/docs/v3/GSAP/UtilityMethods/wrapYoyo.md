---
source_url: "https://gsap.com/docs/v3/GSAP/UtilityMethods/wrapYoyo()/"
title: "wrapYoyo | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:54:14.074513Z"
selector: "article"
---

# wrapYoyo | GSAP | Docs & Learning

* [Utility Methods](/docs/v3/GSAP/UtilityMethods)
* wrapYoyo

On this page

### Returns : \*[​](#returns-- "Direct link to Returns : *")

Returns the element in an Array associated with the provided index or a number in a provided range, going backwards once the last index is reached (yoyo-ing). Or if no value to wrap is provided, it returns a reusable **function** that will do the wrapping accordingly when it's fed a value.

---

Places a number into a specified range such that when it exceeds the maximum, it yoyos back toward the start and if it is less than the minimum, it yoyo's forward to the end. In the context of tweening this has the effect of cycling back and forth through the values.

For example, if you have 10 elements with the `"box"` class applied, and you've got a `["red", "green", "yellow"]` array of colors that you'd like to have those elements animate to so that the first box animates to `"red"`, then next to `"green"`, then next to `"yellow"` and then go backwards so that the 4th would go to `"green"`, 5th to `"red"`, then forwards again to `"green"`, etc., `wrapYoyo()` is perfect for that. If we don't provide an `index` value, we'll get a `function` instead that's ready to do the wrap yoyo-ing accordingly.

```
//returns the corresponding value in the array (wrapping back to the beginning when necessary)  
let color = gsap.utils.wrapYoyo(["red", "green", "yellow"], 5); // "red" (index 5 maps to index 0 in a 3-element Array)  
  
//or use a range  
let num = gsap.utils.wrapYoyo(5, 10, 12); // 8 (12 is two past the max of 10, thus the yoyo would go backward to 8)  
  
//if we don't provide an index, we get a function that's ready to do wrapping accordingly  
let wrap = gsap.utils.wrapYoyo(["red", "green", "yellow"]);  
  
//now we just feed an index number into the function we got back from the line above and we'll get the corresponding value from the wrapped Array  
let color = wrap(5) // "green"
```

#### loading...

## Parameters[​](#parameters "Direct link to Parameters")

1. **value 1** : [*Array* | *Number*] - The Array of values **or** the *minimum* number of a range. If an Array is provided, the index becomes the second parameter.
2. **value 2** : *Number* - The *maximum* number of the range **or** if an Array is provided as the first argument, this parameter should be the index to wrap.
3. **index** : *Number* - (optional) the number to wrap into the *range* provided.