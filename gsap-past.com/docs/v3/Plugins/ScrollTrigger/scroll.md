---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollTrigger/scroll()"
title: "scroll | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:13:18.645071Z"
selector: "article"
---

# scroll | GSAP | Docs & Learning

* [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/)
* methods
* .scroll()

On this page

# .scroll

### .scroll( position:Number ) : Number | null

Gets/Sets the scroll position of the associated scroller (numeric).

#### Parameters

* #### **position**: Number

  The scroll position (in pixels). Or omit this to make the method act as a getter (it'll return the current scroll position).

### Returns : Number | null[​](#returns--number--null "Direct link to Returns : Number | null")

If a parameter is provided, it'll act as a setter and return undefined. If no parameter is provided, it'll act as a getter and return the numeric scroll position on the appropriate axis (vertical by default)

### Details[​](#details "Direct link to Details")

Gets/Sets the scroll position of the associated scroller (numeric). Remember that a ScrollTrigger is EITHER linked to **vertical** OR **horizontal** scrolling, so scroll() only affects that direction.

## Example[​](#example "Direct link to Example")

```
let st = ScrollTrigger.create({  
  trigger: ".class",  
  scroller: ".container", // if no scroller is defined, the viewport (window) is used.  
  start: "top center",  
  end: "+=500",  
});  
  
// get  
let position = st.scroll();  
  
// set  
st.scroll(100);
```