---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/then()"
title: "then | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:12:16.283973Z"
selector: "article"
---

# then | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .then()

On this page

# then

### then( callback:Function ) : Promise

Returns a promise so that you can uses promises to track when a tween or timeline is complete.

#### Parameters

* #### **callback**: Function

  The function that you want to handle the Timeline's promise that is generated.

### Returns : Promise[​](#returns--promise "Direct link to Returns : Promise")

Returns a promise so that you can uses promises to track when a tween or timeline is complete.

### Details[​](#details "Direct link to Details")

Some people prefer to use a [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) instead of an `onComplete` callback - that's exactly what `then()` is for. It returns a `Promise` that will get resolved when the animation completes.

```
gsap.timeline().to(".class", {duration: 1, x: 100}).then(yourFunction).then(...);
```