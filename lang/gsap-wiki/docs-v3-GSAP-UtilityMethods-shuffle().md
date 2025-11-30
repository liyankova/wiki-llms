---
url: https://gsap.com/docs/v3/GSAP/UtilityMethods/shuffle()
title: shuffle | GSAP | Docs & Learning
source_domain: gsap.com
---

# shuffle | GSAP | Docs & Learning

### Returns : Array[​](https://gsap.com/docs/v3/GSAP/UtilityMethods/shuffle()#returns--array "Direct link to Returns : Array")

---

Takes an array and randomly shuffles it, returning the same (but shuffled) array. It does **not** create a new Array.

```
var array = [1, 2, 3, 4, 5];  
  
gsap.utils.shuffle(array); // returns the same array, but shuffled like [2, 5, 3, 1, 4]
```

## Parameters[​](https://gsap.com/docs/v3/GSAP/UtilityMethods/shuffle()#parameters "Direct link to Parameters")

1. **target** : Array - The array to shuffle (in place).