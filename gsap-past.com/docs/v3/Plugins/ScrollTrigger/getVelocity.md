---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollTrigger/getVelocity()"
title: "getVelocity | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:13:04.531191Z"
selector: "article"
---

# getVelocity | GSAP | Docs & Learning

* [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/)
* methods
* .getVelocity()

On this page

# .getVelocity

### .getVelocity( ) : Number

Gets the scroll velocity in pixels-per-second

### Returns : Number[​](#returns--number "Direct link to Returns : Number")

Velocity in pixels-per-second

### Details[​](#details "Direct link to Details")

Gets the scroll velocity in pixels-per-second

## Example[​](#example "Direct link to Example")

```
ScrollTrigger.create({  
  trigger: ".trigger",  
  start: "top center",  
  end: "+=500",  
  onUpdate: (self) => console.log("velocity:", self.getVelocity()),  
});
```