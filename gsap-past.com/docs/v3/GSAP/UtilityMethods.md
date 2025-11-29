---
source_url: "https://gsap.com/docs/v3/GSAP/UtilityMethods"
title: "Utility Methods | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:40:10.532847Z"
selector: "article"
---

# Utility Methods | GSAP | Docs & Learning

* Utility Methods

On this page

---

GSAP's utility methods can be surprisingly helpful. Note that many of them can optionally return FUNCTIONS so that they can be plugged directly into tweens, leveraging GSAP's function-based capabilities. In that case, they'll get called once for each target rather than just using the same end value for them all.

## Video[​](#video "Direct link to Video")

combining utility methods

## Available Utils[​](#available-utils "Direct link to Available Utils")

|  |  |
| --- | --- |
| [checkPrefix](/docs/v3/GSAP/UtilityMethods/checkPrefix()) | Prefixes the proved CSS property if necessary |
| [clamp](/docs/v3/GSAP/UtilityMethods/clamp()) | Clamp a value to fit within a specific range `clamp(0, 100, -12)` -> 0 |
| [distribute](/docs/v3/GSAP/UtilityMethods/distribute()) | Distribute a value among an array of objects either linearly or according to their position in a grid, optionally with easing applied. |
| [getUnit](/docs/v3/GSAP/UtilityMethods/getUnit()) | Get the unit of a string `getUnit("30px")` --> "px". |
| [interpolate](/docs/v3/GSAP/UtilityMethods/interpolate()) | Interpolate between almost any two values (numbers, colors, strings, arrays, complex strings, or even objects with multiple properties) ex `interpolate("red", "blue", 0.5)` --> "rgba(128,0,128,1)"). |
| [mapRange](/docs/v3/GSAP/UtilityMethods/mapRange()) : Number | Map one range to another ex `mapRange(-10, 10, 0, 100, 5) --> 75)` |
| [normalize](/docs/v3/GSAP/UtilityMethods/normalize()) | Map a number within a range to a progress between 0 to 1 ex `normalize(100, 200, 150) --> 0.5)` |
| [pipe](/docs/v3/GSAP/UtilityMethods/pipe()) | Sequence a number of function calls, passing the result of each into the next ex `pipe(clamp(0, 100), snap(5))(8) --> 10` |
| [random](/docs/v3/GSAP/UtilityMethods/random()) | Generate a random number based on parameters ex `random(0, 100, 5) --> 65)` or randomly pick an element from in a supplied array ex. `random(["red", "green", "blue"]) --> "red"` |
| [selector](/docs/v3/GSAP/UtilityMethods/selector()) | Returns a **selector** function that is scoped to a particular Element (or React ref or Angular ElementRef). ex `selector(myElement)` |
| [shuffle](/docs/v3/GSAP/UtilityMethods/shuffle()) | Shuffles the contents of an array in-place. ex `shuffle([1, 2, 3, 4, 5]) --> [4, 2, 1, 5, 3])` |
| [snap](/docs/v3/GSAP/UtilityMethods/snap()) | Snap a value to either an increment ex `snap(5, 13)` --> `15` or to the closest value in an array ex `snap([0, 5, 10], 7)` --> `5`. |
| [splitColor](/docs/v3/GSAP/UtilityMethods/splitColor()) | Split any color into its red, green, blue (and optionally alpha) components. Or hue, saturation, and brightness. ex `splitColor("red")` --> `[255, 0, 0])` |
| [toArray](/docs/v3/GSAP/UtilityMethods/toArray()) | Convert almost any array-like object to an array, including selector text! ex - `toArray(".class")` --> `[element1, element2]`. |
| [unitize](/docs/v3/GSAP/UtilityMethods/unitize()) | Wraps around another utility function, allowing it to accept values with units like "20px" or "50%", stripping off the unit when feeding into the wrapped utility function, and then adding it back to the result ex. `var wrap = gsap.utils.unitize( gsap.utils.wrap(0, 100) ) wrap("150px");` --> `"50px"`. Or force a specific unit ex `unitize( gsap.utils.mapRange(-10, 10, 0, 100), "%")`; --> always returns with `"%"`. |
| [wrap](/docs/v3/GSAP/UtilityMethods/wrap()) | Returns the next item in an array or number in a range after the given index. Or returns a function that returns that object or value if no index is given. |
| [wrapYoyo](/docs/v3/GSAP/UtilityMethods/wrapYoyo()) | Returns the element in an Array associated with the provided index or a number in a provided range, going backwards once the last index is reached (yoyo-ing). Or if no value to wrap is provided, it returns a reusable function that will do the wrapping accordingly when it's fed a value. |