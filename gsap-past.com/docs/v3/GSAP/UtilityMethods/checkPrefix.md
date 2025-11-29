---
source_url: "https://gsap.com/docs/v3/GSAP/UtilityMethods/checkPrefix()/"
title: "checkPrefix | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:53:04.955953Z"
selector: "article"
---

# checkPrefix | GSAP | Docs & Learning

* [Utility Methods](/docs/v3/GSAP/UtilityMethods)
* checkPrefix

On this page

### Returns : String[​](#returns--string "Direct link to Returns : String")

---

Give `checkPrefix()` any CSS property name and it will return the appropriate, browser-prefixed version (if necessary) of that property. If no prefix is needed, it will return the original property name. If the property does not exist, it will return `undefined`. For example:

```
//the following may return "filter", "WebkitFilter", or "MozFilter" depending on your browser  
var filterProperty = gsap.utils.checkPrefix("filter");
```

## Parameters[​](#parameters "Direct link to Parameters")

1. **property** : *String* - The name of the property to check, like "filter".