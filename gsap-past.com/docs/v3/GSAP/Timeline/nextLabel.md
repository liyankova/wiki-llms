---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/nextLabel()"
title: "nextLabel | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:11:46.092499Z"
selector: "article"
---

# nextLabel | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .nextLabel()

On this page

# nextLabel

### nextLabel( time:Number ) : String

Returns the next label in the timeline from the provided time. If no `time` is provided, the timeline's current playhead time will be used.

#### Parameters

* #### **time**: Number

  The time to get the next label from.

### Returns : String[​](#returns--string "Direct link to Returns : String")

Name of the label that is after the time passed to `nextLabel()`. If no `time` is provided, the timeline's current playhead time will be used.

### Details[​](#details "Direct link to Details")

Returns the next label (if any) that occurs **after** the `time` parameter. If no `time` is provided, the timeline's current playhead time will be used. It makes no difference if the timeline is reversed ("after" means later in the timeline's local time zone).

A label that is positioned exactly at the same `time` as the time parameter will be ignored.

You could use `nextLabel()` in conjunction with `tweenTo()` to make the timeline tween to the next label like this:

```
tl.tweenTo(tl.nextLabel());
```