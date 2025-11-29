---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollTrigger/static.create()"
title: "static-create | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:13:31.828950Z"
selector: "article"
---

# static-create | GSAP | Docs & Learning

* [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/)
* methods
* ScrollTrigger.create()

On this page

# ScrollTrigger.create

### ScrollTrigger.create( vars:Object ) : ScrollTrigger

Creates a standalone ScrollTrigger instance

#### Parameters

* #### **vars**: Object

  An object containing all of the configuration details for the ScrollTrigger

### Returns : ScrollTrigger[​](#returns--scrolltrigger "Direct link to Returns : ScrollTrigger")

The new ScrollTrigger instance

### Details[​](#details "Direct link to Details")

Creates a new standalone ScrollTrigger instance. You don't need to put ScrollTriggers directly into animations (though that's probably the most common use case). With a standalone ScrollTrigger, you can tap into the rich callback system to do almost anything.

## Example[​](#example "Direct link to Example")

```
ScrollTrigger.create({  
  trigger: "#id",  
  start: "top top",  
  endTrigger: "#otherID",  
  end: "bottom 50%+=100px",  
  onToggle: (self) => console.log("toggled, isActive:", self.isActive),  
  onUpdate: (self) => {  
    console.log(  
      "progress:",  
      self.progress.toFixed(3),  
      "direction:",  
      self.direction,  
      "velocity",  
      self.getVelocity()  
    );  
  },  
});
```

Detailed Walkthrough

## Configuration[​](#configuration "Direct link to Configuration")

[see the main ScrollTrigger page.](/docs/v3/Plugins/ScrollTrigger/#config-object)