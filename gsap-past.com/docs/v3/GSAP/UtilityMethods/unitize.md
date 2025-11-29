---
source_url: "https://gsap.com/docs/v3/GSAP/UtilityMethods/unitize()/"
title: "unitize | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:54:09.629734Z"
selector: "article"
---

# unitize | GSAP | Docs & Learning

* [Utility Methods](/docs/v3/GSAP/UtilityMethods)
* unitize

On this page

### Returns : Function[​](#returns--function "Direct link to Returns : Function")

---

Think of `unitize()` like a wrapper around **another** function, ensuring that the result gets a unit applied, like `"px"` or `"%"`. For example, perhaps you have a function that only deals with raw numbers like [wrap()](/docs/v3/GSAP/UtilityMethods/wrap()), but you need the result to get a `"px"` added to the end. Or maybe the incoming values have units so you need those removed before being fed into your function ([wrap()](/docs/v3/GSAP/UtilityMethods/wrap()) in this example), and then that same unit put back onto the end of the result. No problem!

#### Example[​](#example "Direct link to Example")

```
// get a function that always applies "px" to the result (and strips off any units from the input)  
var clamp = gsap.utils.unitize(gsap.utils.clamp(0, 100), "px");  
  
// now the result always gets "px" added:  
clamp(132); // "100px"  
clamp("-20%"); // "0px" (notice the unit change)  
clamp(50); // "50px"  
  
// or use whatever unit is in the input:  
var wrap = gsap.utils.unitize(gsap.utils.wrap(0, 100)); // no specific unit is declared in unitize()  
wrap("150px"); // 50px  
wrap("130%"); // 30%  
  
// another example of forcing a unit like "%":  
var map = gsap.utils.unitize(gsap.utils.mapRange(-10, 10, 0, 100), "%");  
map(0); // 50%  
map("5px"); // 75%  
  
// useful in modifier functions:  
gsap.to(".class", {  
  x: 1000,  
  modifiers: {  
    //the value fed into this function will have unit - this strips it off to feed in a raw number to wrap() and then slaps "px" onto the result.  
    x: gsap.utils.unitize(gsap.utils.wrap(0, window.innerWidth), "px"),  
  },  
});
```

## Parameters[​](#parameters "Direct link to Parameters")

1. **function** : Function - The function whose result should get the unit applied.
2. **unit** : String\*(optional)\* - The unit that should always be added to the end of the result. If you omit this parameter, the original unit from the input is applied dynamically.

Note: `unitize()` strips off any units from the input (using `parseFloat()`) before passing it along to the `function`.