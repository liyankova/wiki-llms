---
source_url: "https://gsap.com/docs/v3/GSAP/UtilityMethods/interpolate()/"
title: "interpolate | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:53:19.633524Z"
selector: "article"
---

# interpolate | GSAP | Docs & Learning

* [Utility Methods](/docs/v3/GSAP/UtilityMethods)
* interpolate

On this page

A super-flexible method that interpolates linearly between any two values of a similar type (numbers, colors, strings, arrays, complex strings with multiple sets of embedded numbers, objects with multiple properties...almost anything!). You provide a `progress` value between 0 and 1 where 0.5 is halfway between, and it will return the interpolated value accordingly.

---

Choose one of the following method signatures - either get an interpolated value immediately or omit the `progress` parameter to get a **reusable function** that interpolates according to any progress values you feed in later:

## 1) interpolate(startValue, endValue, progress)[​](#1-interpolatestartvalue-endvalue-progress "Direct link to 1) interpolate(startValue, endValue, progress)")

1. **startValue** : \* - The starting value. This can be almost any data type (Number, String, Array, complex String, color, Object)
2. **endValue** : \* - The ending value. This can be almost any data type, as long as it matches the `startValue`
3. **progress** : Number - A value between 0 and 1 where 0 is the start, 0.5 is halfway between, and 1 is the end.

**Returns**: the interpolated value. Colors are in rgba() format (or hsla() if that's detected in the end value)

#### Example[​](#example "Direct link to Example")

```
//interpolate halfway between 0 and 500 (number)  
gsap.utils.interpolate(0, 500, 0.5); // 250  
  
// strings  
gsap.utils.interpolate("20px", "40px", 0.5); // "30px"  
  
//colors  
gsap.utils.interpolate("red", "blue", 0.5); // "rgba(128,0,128,1)"  
  
//objects  
gsap.utils.interpolate(  
  { a: 0, b: 10, c: "red" },  
  { a: 100, b: 20, c: "blue" },  
  0.5  
); // {a: 50, b: 15, c: "rgba(128,0,128,1)"}
```

## 2) interpolate(array, progress)[​](#2-interpolatearray-progress "Direct link to 2) interpolate(array, progress)")

1. **array** : Array - An array of values to linearly interpolate between (numbers, colors, strings, whatever...they just need to be of a similar data type)
2. **progress** : Number - A value between 0 and 1 where 0 is the start, 0.5 is halfway between, and 1 is the end.

**Returns**: the interpolated value

#### Example[​](#example-1 "Direct link to Example")

```
// an array of numbers  
gsap.utils.interpolate([100, 50, 500], 0.5); // 50  
gsap.utils.interpolate([100, 50, 500], 0.75); // 275  
  
// colors  
gsap.utils.interpolate(["red", "green", "blue"], 0.5); // "green"  
gsap.utils.interpolate(["red", "green", "blue"], 0.25); // "rgba(128,64,0,1)"
```

## 3) interpolate(startValue, endValue)[​](#3-interpolatestartvalue-endvalue "Direct link to 3) interpolate(startValue, endValue)")

1. **startValue** : \* - The starting value. This can be almost any data type (Number, String, Array, complex String, color, Object)
2. **endValue** : \* - The ending value. This can be almost any data type, as long as it matches the `startValue`

**Returns**: a reusable function that accepts one parameter - a progress value (between 0 and 1)

If you omit the `progress` (3rd) parameter, the utility method will return a **reusable function** that's ready to interpolate based on any progress value you provide later. In other words, the returned function remembers the `startValue` and `endValue` so that it can very quickly and efficiently do the interpolating later.

#### Example[​](#example-2 "Direct link to Example")

```
// get a function that will always interpolate between 0 and 100  
var interp = gsap.utils.interpolate(0, 100); //notice we didn't provide a progress value  
  
// now we can reuse the function to interpolate any values:  
console.log(interp(0.5)); // 50  
console.log(interp(0.25)); // 25  
console.log(interp(1)); // 100  
  
// even works for an object with multiple properties!  
var interp = gsap.utils.interpolate(  
  { a: 0, b: 10, c: "red" },  
  { a: 100, b: 20, c: "blue" }  
);  
  
interp(0.5); // {a: 50, b: 15, c: "rgba(128,0,128,1)"}
```

When animating objects, if you want it to mutate the original startValue (instead of creating a separate object internally), you can pass in `true` as the 3rd parameter.

## 4) interpolate(array)[​](#4-interpolatearray "Direct link to 4) interpolate(array)")

1. **array** : Array - An array of values to linearly interpolate between (numbers, colors, strings, whatever...they just need to be of a similar data type)

**Returns**: a reusable function that accepts one parameter - a progress value (between 0 and 1)

If you omit the `progress` (2nd) parameter, the utility method will return a **reusable function** that's ready to interpolate the array based on any progress value you provide later. In other words, the returned function remembers the `array` so that it can very quickly and efficiently do the interpolating later.

#### Example[​](#example-3 "Direct link to Example")

```
// get a function that will interpolate the Array  
var interp = gsap.utils.interpolate([100, 50, 500]); //notice we didn't provide a progress value  
  
// now we can reuse the function to interpolate any values:  
console.log(interp(0.5)); // 50  
console.log(interp(0.75)); // 275  
  
// even works for colors!  
var interp = gsap.utils.interpolate(["red", "green", "blue"]);  
  
interp(0.25); // "rgba(128,64,0,1)"
```

## Tip: combine reusable functions for powerful data transformations![​](#tip-combine-reusable-functions-for-powerful-data-transformations "Direct link to Tip: combine reusable functions for powerful data transformations!")

You can [`pipe()`](/docs/v3/GSAP/UtilityMethods/pipe()) several reusable functions together to perform multiple tasks on an incoming value, like [clamping](/docs/v3/GSAP/UtilityMethods/clamp()), [mapping](/docs/v3/GSAP/UtilityMethods/mapRange()) to another range, [snapping](/docs/v3/GSAP/UtilityMethods/snap()), [interpolating](/docs/v3/GSAP/UtilityMethods/interpolate()), and [more](/docs/v3/GSAP/UtilityMethods). For example:

```
// get a clamping function that will always clamp to a range between 0 and 100  
var colorizer = gsap.utils.pipe(  
  // clamp between 0 and 100  
  gsap.utils.clamp(0, 100),  
  
  // normalize to a value between 0 and 1  
  gsap.utils.normalize(0, 100),  
  
  // then interpolate between red and blue  
  gsap.utils.interpolate("red", "blue")  
);  
  
// now we feed one value in and it gets run through ALL those transformations!:  
colorizer(25.874);
```

### Video demo: combining utility methods[​](#video-demo-combining-utility-methods "Direct link to Video demo: combining utility methods")

Combining utility Methods