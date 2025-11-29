---
source_url: "https://gsap.com/docs/v3/GSAP/UtilityMethods/shuffle()/"
title: "shuffle | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:53:54.826816Z"
selector: "article"
---

# shuffle | GSAP | Docs & Learning

* [Utility Methods](/docs/v3/GSAP/UtilityMethods)
* shuffle

On this page

### Returns : Array[​](#returns--array "Direct link to Returns : Array")

---

Takes an array and randomly shuffles it, returning the same (but shuffled) array. It does **not** create a new Array.

```
var array = [1, 2, 3, 4, 5];  
  
gsap.utils.shuffle(array); // returns the same array, but shuffled like [2, 5, 3, 1, 4]
```

## Parameters[​](#parameters "Direct link to Parameters")

1. **target** : Array - The array to shuffle (in place).