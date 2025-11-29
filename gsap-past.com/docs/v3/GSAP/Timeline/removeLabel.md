---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/removeLabel()"
title: "removeLabel | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:11:55.415502Z"
selector: "article"
---

# removeLabel | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .removeLabel()

On this page

# removeLabel

### removeLabel( label:String ) : self

Removes a label from the timeline and returns the time of that label.

#### Parameters

* #### **label**: String

  The name of the label to remove.

### Returns : self[​](#returns--self "Direct link to Returns : self")

self (makes chaining easier)

### Details[​](#details "Direct link to Details")

Removes a label from the timeline. You could also use the remove() method to accomplish the same task.

```
tl.removeLabel("myLabel"); // returns the label time like 1.0
```