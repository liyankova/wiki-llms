---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/labels"
title: "labels | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:11:02.688058Z"
selector: "article"
---

# labels | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* properties
* .labels

On this page

# labels

### labels : Object

This stores any labels that have been added to the timeline.

### Details[​](#details "Direct link to Details")

This stores any labels that have been added to the timeline. You can get the full object with all labels by using `timeline.labels`. For example:

```
var tl = gsap.timeline();  
  
tl.addLabel("myLabel", 3);  
tl.addLabel("anotherLabel", 5);  
  
//now the label object has those labels and times, like:  
console.log(tl.labels.myLabel); // 3  
console.log(tl.labels.anotherLabel); // 5
```