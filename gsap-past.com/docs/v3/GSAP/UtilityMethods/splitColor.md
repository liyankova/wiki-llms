---
source_url: "https://gsap.com/docs/v3/GSAP/UtilityMethods/splitColor()/"
title: "splitColor | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:54:00.002114Z"
selector: "article"
---

# splitColor | GSAP | Docs & Learning

* [Utility Methods](/docs/v3/GSAP/UtilityMethods)
* splitColor

On this page

### Returns : Array[​](#returns--array "Direct link to Returns : Array")

Converts a string-based color value into an array consisting of [red, green, blue] (or if an alpha value is required, it'll be in the last spot of a 4-element array). For example, `[255, 0 128, 1]`. You can optionally request HSLA (hue, saturation, lightness, and alpha) values instead by using the 2nd parameter.

---

`splitColor()` will work with `"rgb()"`, `"rgba()"`, `"hsl()"`, `"hsla()"`, hexadecimal values, or any of the basic named colors like "red", "blue", etc.

An example of a returned value would be `[255, 128, 0]` or [`255, 102, 153, 0.5]`. Or if you prefer to get HSL-based values, just pass in `true` as the 2nd parameter.

```
gsap.utils.splitColor("red"); // [255, 0, 0]  
gsap.utils.splitColor("#6fb936"); // [111, 185, 54]  
gsap.utils.splitColor("rgba(204, 153, 51, 0.5)"); // [204, 153, 51, 0.5]  
  
// the 2nd parameter indicates we want an HSL value back instead of RGB:  
gsap.utils.splitColor("#6fb936", true); // [94, 55, 47]
```

## Parameters[​](#parameters "Direct link to Parameters")

1. **color** : String - The color that should be split.
2. **returnHSL** : Boolean - (optional) If `true`, the resulting Array will contain HSL/HSLA values instead of RGB/RGBA ones.