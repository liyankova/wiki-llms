---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/addLabel()"
title: "addLabel | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:11:12.222578Z"
selector: "article"
---

# addLabel | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* methods
* .addLabel()

On this page

# addLabel

### addLabel( label:String, position:[Number | String] ) : self

Adds a label to the timeline, making it easy to mark important positions/times.

#### Parameters

* #### **label**: String

  The name of the label
* #### **position**: [Number | String]

  (default = `"+=0"`) - controls the insertion point in the timeline (by default, it's the end of the timeline). See options below, or the [Position Parameter article](/resources/position-parameter) which has interactive timeline visualizations and a video. If you define a label that doesn't exist yet, it will **automatically be added to the end of the timeline**

### Returns : self[​](#returns--self "Direct link to Returns : self")

self (makes chaining easier)

### Details[​](#details "Direct link to Details")

Adds a label to the timeline, making it easy to mark important positions/times. You can then reference that label in other methods, like `seek("myLabel")` or `add(myTween, "myLabel")` or `reverse("myLabel")`. You could also use the [`timeline.add()`](/docs/v3/GSAP/Timeline/add()) method to insert a label.

0

1

2blueSpin

3

4

Play

## Positioning labels in a timeline[​](#positioning-labels-in-a-timeline "Direct link to Positioning labels in a timeline")

By default, labels are added to the **end** of the timeline but you can use the [position parameter](/resources/position-parameter) to control precisely where things are placed. It uses a flexible syntax with the following options:

* **Absolute time** (in seconds) measured from the start of the timeline, as a **number** like `3`

  ```
  // insert exactly 3 seconds from the start of the timeline  
  tl.addLabel("myLabel", 3);
  ```
* **Label**, like `"someLabel"`. *If the label doesn't exist, it'll be added to the end of the timeline.*

  ```
  // insert at the "someLabel" label  
  tl.addLabel("myLabel", "someLabel");
  ```
* `"<"` The **start** of previous animation\*\*. *Think of `<` as a pointer back to the start of the previous animation.*

  ```
  // insert at the START of the  previous animation  
  tl.addLabel("myLabel", "<");
  ```
* `">"` - The **end** of the previous animation\*\*. *Think of `>` as a pointer to the end of the previous animation.*

  ```
  // insert at the END of the previous animation  
  tl.addLabel("myLabel", ">");
  ```
* A complex string where `"+="` and `"-="` prefixes indicate **relative** values. *When a number follows `"<"` or `">"`, it is interpreted as relative so `"<2"` is the same as `"<+=2"`.* Examples:

  + `"+=1"` - 1 second past the end of the timeline (creates a gap)
  + `"-=1"` - 1 second before the end of the timeline (overlaps)
  + `"myLabel+=2"` - 2 seconds past the label `"myLabel"`
  + `"<+=3"` - 3 seconds past the start of the previous animation
  + `"<3"` - same as `"<+=3"` (see above) (`"+="` is implied when following `"<"` or `">"`)
  + `">-0.5"` - 0.5 seconds before the end of the previous animation. It's like saying *"the end of the previous animation plus -0.5"*
* A complex string based on a **percentage**. When immediately following a `"+="` or `"-="` prefix, the percentage is based on [total duration](/docs/v3/GSAP/Tween/totalDuration()) of the **animation being inserted**. When immediately following `"<"` or `">"`, it's based on the [total duration](/docs/v3/GSAP/Tween/totalDuration()) of the **previous animation**. *Note: total duration includes repeats/yoyos*. Examples:

  + `"-=25%"` - overlap with the end of the timeline by 25% of the inserting animation's total duration
  + `"+=50%"` - beyond the end of the timeline by 50% of the inserting animation's total duration, creating a gap
  + `"<25%"` - 25% into the previous animation (from its start). Same as `">-75%"` which is negative 75% from the **end** of the previous animation.
  + `"<+=25%"` - 25% of the inserting animation's total duration past the start of the previous animation. Different than `"<25%"` whose percentage is based on the **previous animation's** total duration whereas anything immediately following `"+="` or `"-="` is based on the **inserting animation's** total duration.
  + `"myLabel+=30%"` - 30% of the inserting animation's total duration past the label `"myLabel"`.

\*Percentage-based values were added in GSAP 3.7.0  
\*\*The "previous animation" refers to the most recently-inserted animation, not necessarily the animation that is closest to the end of the timeline.

### Position Parameter Interactive Demo[​](#position-parameter-interactive-demo "Direct link to Position Parameter Interactive Demo")

#### loading...

Be sure to read our tutorial [Understanding the Position Parameter](/resources/position-parameter) which includes interactive timeline visualizations and a video.