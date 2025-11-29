---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollSmoother/content()"
title: "content | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:14:25.871141Z"
selector: "article"
---

# content | GSAP | Docs & Learning

* [ScrollSmoother](/docs/v3/Plugins/ScrollSmoother/)
* methods
* .content()

On this page

# .content

### .content( element:String | Element ) : Element | self

Gets/Sets the content element.

#### Parameters

* #### **element**: String | Element

  The element that should be used as the content. You can use selector text like `"#content"` or an element reference.

### Returns : Element | self[​](#returns--element--self "Direct link to Returns : Element | self")

The content Element (or the ScrollSmoother instance if used as a setter)

### Details[​](#details "Direct link to Details")

Gets/Sets the content element.

### Getter[​](#getter "Direct link to Getter")

```
let content = smoother.content();
```

### Setter[​](#setter "Direct link to Setter")

```
// set the content to the element with #content id  
smoother.content("#content");
```