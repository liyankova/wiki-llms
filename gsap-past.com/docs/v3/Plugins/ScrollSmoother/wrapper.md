---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollSmoother/wrapper()"
title: "wrapper | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:14:52.221119Z"
selector: "article"
---

# wrapper | GSAP | Docs & Learning

* [ScrollSmoother](/docs/v3/Plugins/ScrollSmoother/)
* methods
* .wrapper()

On this page

# .wrapper

### .wrapper( element:String | Element ) : Element | self

Gets/Sets the wrapper element.

#### Parameters

* #### **element**: String | Element

  The element that should be used as the wrapper. You can use selector text like `"#wrapper"` or an element reference.

### Returns : Element | self[​](#returns--element--self "Direct link to Returns : Element | self")

The wrapper Element (or the ScrollSmoother instance if used as a setter)

### Details[​](#details "Direct link to Details")

Gets/Sets the wrapper element.

### Getter[​](#getter "Direct link to Getter")

```
let wrapper = smoother.wrapper();
```

### Setter[​](#setter "Direct link to Setter")

```
// set the wrapper to the element with #wrapper id  
smoother.wrapper("#wrapper");
```