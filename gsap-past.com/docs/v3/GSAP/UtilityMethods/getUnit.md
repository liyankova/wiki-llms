---
source_url: "https://gsap.com/docs/v3/GSAP/UtilityMethods/getUnit()/"
title: "getUnit | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:53:14.750507Z"
selector: "article"
---

# getUnit | GSAP | Docs & Learning

* [Utility Methods](/docs/v3/GSAP/UtilityMethods)
* getUnit

On this page

### Returns : String[​](#returns--string "Direct link to Returns : String")

Returns unit of a given string where the number comes first, then the unit.

---

Isolates the unit inside a string where the number is first, then the unit.

```
// returns the unit of a CSS valuegsap.utils.getUnit("50%"); // "%"gsap.utils.getUnit("100vw"); // "vw"
```

## Parameters[​](#parameters "Direct link to Parameters")

1. **value** : *String* - The value that you want the unit of.