---
source_url: "https://gsap.com/docs/v3/GSAP/UtilityMethods/distribute()/"
title: "distribute | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:53:11.899032Z"
selector: "article"
---

# distribute | GSAP | Docs & Learning

* [Utility Methods](/docs/v3/GSAP/UtilityMethods)
* distribute

On this page

### Returns : Function[​](#returns--function "Direct link to Returns : Function")

Returns a function to distribute an array of values based on the inputs that you give it.

---

Distributes an amount across the elements in an array according to various configuration options. Internally, it's what [advanced staggers](/resources/getting-started/Staggers) use, but you can apply it for any value. It essentially assigns values based on the element's position in the array (or in a grid):

```
// get a function that, when fed an index value, will return a value according to the configuration options  
let distributor = gsap.utils.distribute({  
  // the base value to start from (default:0)  
  base: 50,  
  
  // total amount to distribute across the targets (this amount gets added to the "base" when returned)  
  amount: 100,  
  
  // position in the targets array to begin from (can be an index number, a keyword like "start", "center",  
  // "edges", "random", or "end", or an array of ratios along the x-axis and y-axis like [0.25, 0.75]) (default: 0)  
  from: "center",  
  
  // bases distribution on the element's position in a grid [rows, columns] instead of a flat array.  
  // You can also define the rows and columns in array format like [5, 10]  
  grid: "auto",  
  
  // for grid-based distributing, you can limit measurements to one axis ("x" or "y")  
  axis: "y",  
  
  // distributes based on an ease curve!  
  ease: "power1.inOut",  
});  
  
// get an array of all the elements with the class ".box" applied  
let targets = gsap.utils.toArray(".box");  
  
// Now for any target element, we can just feed in its index from the targets array (along with the target  
// and array) and it'll do all the calculations and return the appropriate amount:  
let distributedValue = distributor(2, targets[2], targets);
```

This can be used directly in a tween:

```
// animate the scale of all ".class" elements so that the ones in the middle are 0.5 and the ones on  
// the outer edges are 3  
gsap.to(".class", {  
  scale: gsap.utils.distribute({  
    base: 0.5,  
    amount: 2.5,  
    from: "center",  
  }),  
});
```

## Parameters[​](#parameters "Direct link to Parameters")

1. **config** : *Object* - The config object to declare how you want inputs to be distributed. All properties inside of this object are optional. These properties can be used:
   * **base** : *Number* - The base value to start from. The default is 0.
   * **amount** : *Number* - The total amount to distribute across the targets (this amount gets added to the "base" when returned). So if `amount` is `1` and there 100 targets, there would be a 0.01 difference between every return value. If you prefer to specify a certain amount between each target, use the `each` property *instead*.
   * **each** : Number - The amount to add between each target (this amount gets added to the "base" when returned). So if `each` is `1` and the there are 4 targets, it would return 0, 1, 2, and 3. If you prefer to specify a **total** amount to split up among the targets, use the `amount` property *instead*.
   * **from** : [*Number* | *String* | *Array*] - The position in the targets array to begin from (can be an index number, a keyword like `"start"`, `"center"`, `"edges"`, `"random"`, or `"end"`, or an array of ratios along the x-axis and y-axis like `[0.25, 0.75]`). The default is `0`.
   * **grid** : [*String* | *Array*] - Bases distribution on the element's position in a grid [rows, columns], like `[5, 10]`, instead of a flat array. You can use `"auto"` to have GSAP try to automatically detect the column and row count for DOM elements.
   * **axis** : *String* - For grid-based distributing, you can limit measurements to one axis (`"x"` or `"y"`).
   * **ease** : *Ease* - Distributes based on an ease curve! The default is `"none"`.

This video on distribute that's part of SnorklTV's [GSAP 3: Beyond the Basics course](https://www.creativecodingclub.com/courses/gsap3-beyond-the-basics?ref=44f484) may help your understand.

And the companion pen used in the video.

#### loading...