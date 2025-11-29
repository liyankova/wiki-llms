---
source_url: "https://gsap.com/docs/v3/GSAP/gsap.globalTimeline()"
title: "gsap.globalTimeline() | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:56:21.542739Z"
selector: "article"
---

# gsap.globalTimeline() | GSAP | Docs & Learning

* [GSAP](/docs/v3/GSAP/)
* properties
* gsap.globalTimeline()

On this page

### Type : [Timeline](/docs/v3/GSAP/Timeline)[​](#type--timeline "Direct link to type--timeline")

`gsap.globalTimeline` is the root Timeline instance that drives everything in GSAP, making it a powerful way to affect all animations at once. Keep in mind, however, that [gsap.delayedCalls()](/docs/v3/GSAP/gsap.delayedCall()) are also technically tweens, so if you [pause()](/docs/v3/GSAP/Timeline/pause()) or [timeScale()](/docs/v3/GSAP/Timeline/timeScale()) the globalTimeline, it will affect delayedCalls() too. If you want to omit those, check out [gsap.exportRoot()](/docs/v3/GSAP/gsap.exportRoot()).

## Useful Methods[​](#useful-methods "Direct link to Useful Methods")

* `gsap.globalTimeline`[`.pause()`](/docs/v3/GSAP/Timeline/pause()) - Pauses the global timeline which affects **ALL** animations. Returns itself.
* `gsap.globalTimeline`[`.play()`](/docs/v3/GSAP/Timeline/play()) - Resumes the global timeline which affects **ALL** animations. Returns itself.
* `gsap.globalTimeline`[`.paused()`](/docs/v3/GSAP/Timeline/paused()) - Returns `true` if the global timeline is paused. Returns `false` if the global timeline is playing.
* `gsap.globalTimeline`[`.timeScale()`](/docs/v3/GSAP/Timeline/timeScale()) - Gets or sets the global time scale which is a multiplier that affects **ALL** animations. This doesn't actually set the `timeScale()` of each individual tween/timeline, but rather it affects the rate at which the root timeline plays (that timeline contains all other animations). This is a great way to globally speed up or slow down all animations at once. For example:

```
gsap.globalTimeline.timeScale(0.5); //plays at half-speed  
gsap.globalTimeline.timeScale(2); //plays twice the normal speed  
var currentTimeScale = gsap.globalTimeline.timeScale(); //returns the current global timeScale
```

## Notes[​](#notes "Direct link to Notes")

* Keep in mind that since the global timeline is used to run all other tweens and timelines, `gsap.globalTimeline.isActive()` will always return `true` regardless of whether or not there are any tweens or timelines currently active.