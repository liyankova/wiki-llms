---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/previousLabel()"
title: "previousLabel | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:11:49.784529Z"
selector: "article"
---

# previousLabel | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .previousLabel()

On this page

# previousLabel

### previousLabel( time:Number ) : String

Returns the previous label in the timeline from the provided `time`. If no `time` is provided, the timeline's current playhead time will be used.

#### Parameters

* #### **time**: Number

  The time to get the previous label from.

### Returns : String[​](#returns--string "Direct link to Returns : String")

Name of the label that is before the time passed to `previousLabel()`. If no `time` is provided, the timeline's current playhead time will be used.

### Details[​](#details "Direct link to Details")

Returns the previous label (if any) that occurs **before** the `time` parameter. If no `time` is provided, the timeline's current playhead time will be used. It makes no difference if the timeline is reversed ("before" means earlier in the timeline's local time zone).

A label that is positioned exactly at the same `time` as the time parameter will be ignored.

You could use `previousLabel()` in conjunction with `tweenTo()` to make the timeline tween back to the previous label like this:

```
tl.tweenTo(tl.previousLabel());
```