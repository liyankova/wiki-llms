---
url: https://gsap.com/docs/v3/GSAP/UtilityMethods/checkPrefix()
title: checkPrefix | GSAP | Docs & Learning
source_domain: gsap.com
---

# checkPrefix | GSAP | Docs & Learning

### Returns : String[​](https://gsap.com/docs/v3/GSAP/UtilityMethods/checkPrefix()#returns--string "Direct link to Returns : String")

---

Give `checkPrefix()` any CSS property name and it will return the appropriate, browser-prefixed version (if necessary) of that property. If no prefix is needed, it will return the original property name. If the property does not exist, it will return `undefined`. For example:

```
//the following may return "filter", "WebkitFilter", or "MozFilter" depending on your browser  
var filterProperty = gsap.utils.checkPrefix("filter");
```

## Parameters[​](https://gsap.com/docs/v3/GSAP/UtilityMethods/checkPrefix()#parameters "Direct link to Parameters")

1. **property** : *String* - The name of the property to check, like "filter".