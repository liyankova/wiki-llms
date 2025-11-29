---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/getById()"
title: "getById | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:11:28.970957Z"
selector: "article"
---

# getById | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .getById()

On this page

# getById

### getById( id:String ) : Animation

#### Parameters

* #### **id**: String

  The `id` of the animation which is typically set in the vars object of the Tween/Timeline upon creation

### Returns : Animation[​](#returns--animation "Direct link to Returns : Animation")

The Tween or Timeline associated with the provided ID.

### Details[​](#details "Direct link to Details")

Searches the timeline and returns the first descendant with a matching ID. When creating a tween or timeline, you can assign it an `id` so that later you can find it using that `id`. This is particularly helpful when using frameworks and build tools like React where keeping track of variables can be difficult.

```
var tl = gsap.timeline();  
  
//give the animation a "myTween" id upon creation  
tl.to(obj, { id: "myTween", duration: 1, x: 100 });  
  
//later we can get it like this  
var myTween = tl.getById("myTween");
```