---
source_url: "https://gsap.com/docs/v3/HelperFunctions/helpers/pluckRandomFrom"
title: "pluckRandomFrom | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:16:38.239555Z"
selector: "article"
---

# pluckRandomFrom | GSAP | Docs & Learning

* [Helper functions](/docs/v3/HelperFunctions/)
* pluckRandomFrom

Randomly pluck values from an array one-by-one until they've all been plucked (almost as if when you pluck one, it's no longer available to be plucked again until ALL of them have been uniquely plucked):

```
function pluckRandomFrom(array) {  
  return (  
    array.eligible && array.eligible.length  
      ? array.eligible  
      : (array.eligible = gsap.utils.shuffle(array.slice(0)))  
  ).pop();  
}
```

All you've gotta do is feed the array in each time and it keeps track of things for you!

Alternatively, if you just want to pull a random element from an array that's not the PREVIOUS one that was pulled (so not emptying the array, just pulling randomly while ensuring the same element isn't pulled twice in a row), you can use this:

```
function getRandomFrom(array) {  
  var selected = array.selected;  
  while (  
    selected === (array.selected = Math.floor(Math.random() * array.length))  
  ) {}  
  return array[array.selected];  
}
```