---
source_url: "https://gsap.com/docs/v3/GSAP/gsap.getById()"
title: "gsap.getById() | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:55:19.194766Z"
selector: "article"
---

# gsap.getById() | GSAP | Docs & Learning

* [GSAP](/docs/v3/GSAP/)
* methods
* gsap.getById()

On this page

### Returns : [Tween](/docs/v3/GSAP/Tween) or [Timeline](/docs/v3/GSAP/Timeline)[​](#returns--tween-or-timeline "Direct link to returns--tween-or-timeline")

The tween or timeline associated with the given ID. Returns `undefined` if no tween or timeline has that ID.

### Details[​](#details "Direct link to Details")

When creating a tween or timeline you can assign it an `id` so that you can reference it later. This is helpful when using frameworks and build tools like React where keeping track of variables can be difficult.

```
gsap.to(obj, { id: "myTween", duration: 1, x: 100 });  
  
//later  
let tween = gsap.getById("myTween"); //returns the tween  
tween.pause();
```

warning

GSAP automatically releases animations for garbage collection shortly after they complete, so `getById()` will only find animations that are active or haven't begun yet. Otherwise, if kept all animations around just in case you're gonna call `getById()` to find one, it could quickly clog up the system and lead to memory leaks. If you need to maintain a reference to an animation even after it completes, you should use a variable like this:

```
let myTween = gsap.to(obj, { duration: 1, x: 100 });  
  
// later  
myTween.pause();
```