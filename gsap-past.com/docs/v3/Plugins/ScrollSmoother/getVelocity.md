---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollSmoother/getVelocity()"
title: "getVelocity | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:14:31.979444Z"
selector: "article"
---

# getVelocity | GSAP | Docs & Learning

* [ScrollSmoother](/docs/v3/Plugins/ScrollSmoother/)
* methods
* .getVelocity()

On this page

# .getVelocity

### .getVelocity( ) : Number

Returns the current velocity of the smoothed scroll in pixels-per-second

### Details[​](#details "Direct link to Details")

Returns the current velocity of the smoothed scroll in pixels-per-second. For example:

```
ScrollSmoother.create({  
  onUpdate: (self) => console.log("velocity:", self.getVelocity()),  
});
```

Another way to write it would be:

```
let smoother = ScrollSmoother.create({...});  
  
button.addEventListener("click", () => {  
  console.log("velocity:", smoother.getVelocity());  
});
```