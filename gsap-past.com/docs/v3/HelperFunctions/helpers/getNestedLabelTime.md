---
source_url: "https://gsap.com/docs/v3/HelperFunctions/helpers/getNestedLabelTime"
title: "getNestedLabelTime | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:16:22.942227Z"
selector: "article"
---

# getNestedLabelTime | GSAP | Docs & Learning

* [Helper functions](/docs/v3/HelperFunctions/)
* getNestedLabelTime

Labels are timeline-specific, so you can't tell a timeline to move its playhead to a label that exists in a **nested** timeline. So here's a helper function that lets you find a nested label and calculate where that lines up on the [parent/ancestor] timeline:

```
function getNestedLabelTime(timeline, label) {  
  let children = timeline.getChildren(true, false, true),  
    i = children.length,  
    tl,  
    time;  
  while (i--) {  
    if (label in children[i].labels) {  
      tl = children[i];  
      time = tl.labels[label];  
      break;  
    }  
  }  
  if (tl) {  
    while (tl !== timeline) {  
      time = tl.startTime() + time / tl.timeScale();  
      tl = tl.parent;  
    }  
  }  
  return time;  
}
```

So here's an example usage: `tl.seek(getNestedLabelTime(tl, "someNestedLabel"))`