---
source_url: "https://gsap.com/docs/v3/GSAP/Tween/vars"
title: "vars | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:10:23.034698Z"
selector: "article"
---

# vars | GSAP | Docs & Learning

* [Tween](/docs/v3/GSAP/Tween)
* properties
* .vars

On this page

# vars

### vars : Object

The configuration object passed into the constructor which contains all the properties/values you want to animate, along with any of the optional **special properties** like like `onComplete`, `onUpdate`, etc., like `gsap.to(".class",{onComplete: func});`

### Details[​](#details "Direct link to Details")

The `vars` object passed into the constructor which contains all the properties/values you want to animate, along with any of the optional **special properties** like like `onComplete`, `onUpdate`, etc. (listed below)

### Property

### Description

* #### callbackScope

  The scope to be used for all of the callbacks (onStart, onUpdate, onComplete, etc.).
* #### data

  Assign arbitrary data to this property (a string, a reference to an object, whatever) and it gets attached to the tween instance itself so that you can reference it later like `yourTween.data`.
* #### delay

  Amount of delay before the animation should begin (in seconds).
* #### duration

  The duration of the animation (in seconds). Default: `0.5`.
* #### ease

  Controls the rate of change during the animation, giving it a specific feel. For example, `"elastic"` or `"strong.inOut"`. See the [Ease Visualizer](/docs/v3/Eases) for a list of all of the options. `ease` can be a String (most common) or a function that accepts a progress value between 0 and 1 and returns a converted, similarly normalized value. Default: `"power1.out"`.
* #### id

  Allows you to (optionally) assign a unique identifier to your tween instance so that you can find it later with `gsap.getById()` and it will show up in [GSDevTools](/docs/v3/Plugins/GSDevTools/) with that id.
* #### immediateRender

  Normally a tween waits to render for the first time until the very next tick (update cycle) unless you specify a delay. Set `immediateRender: true` to force it to render immediately upon instantiation. Default: `false` for [to()](/docs/v3/GSAP/gsap.to()) tweens, `true` for [from()](/docs/v3/GSAP/gsap.from()) and [fromTo()](/docs/v3/GSAP/gsap.fromTo()) tweens or anything with a [scrollTrigger](/docs/v3/Plugins/ScrollTrigger) applied.
* #### inherit

  Normally tweens inherit from their parent timeline's `defaults` object (if one is defined), but you can disable this on a per-tween basis by setting `inherit: false`.
* #### lazy

  When a tween renders for the very first time and reads its starting values, GSAP will try to delay writing of values until the very end of the current "tick" which can improve performance because it avoids the read/write/read/write layout thrashing that browsers dislike. To disable lazy rendering for a particular tween, set `lazy: false`. In most cases, there's no need to set `lazy`. To learn more, watch [this video](https://www.youtube.com/watch?v=TMHJptqnDpU). Default: `true` (except for zero-duration tweens).
* #### onComplete

  A function to call when the animation has completed.
* #### onCompleteParams

  An Array of parameters to pass the onComplete function. For example, `gsap.to(".class", {x:100, onComplete:myFunction, onCompleteParams:["param1", "param2"]});`.
* #### onRepeat

  A function to call each time the animation enters a new iteration cycle (repeats). Obviously this only occurs if you set a non-zero `repeat`.
* #### onRepeatParams

  An Array of parameters to pass the onRepeat function.
* #### onReverseComplete

  A function to call when the animation has reached its beginning again from the reverse direction (excluding repeats).
* #### onReverseCompleteParams

  An Array of parameters to pass the onReverseComplete function.
* #### onStart

  A function to call when the animation begins (when its time changes from 0 to some other value which can happen more than once if the tween is restarted multiple times).
* #### onStartParams

  An Array of parameters to pass the onStart function.
* #### onUpdate

  A function to call every time the animation updates (on each "tick" that moves its playhead).
* #### onUpdateParams

  An Array of parameters to pass the onUpdate function.
* #### overwrite

  If `true`, all tweens of the same targets will be killed immediately regardless of what properties they affect. If `"auto"`, when the tween renders for the first time it hunt down any conflicts in active animations (animating the same properties of the same targets) and kill **only those parts** of the other tweens. Non-conflicting parts remain intact. If `false`, no overwriting strategies will be employed. Default: `false`.
* #### paused

  If `true`, the animation will pause itself immediately upon creation. Default: `false`.
* #### repeat

  How many times the animation should repeat. So `repeat: 1` would play a total of two iterations. Default: `0`.
  `repeat: -1` will repeat infinitely.
* #### repeatDelay

  Amount of time to wait between repeats (in seconds). Default: `0`.
* #### repeatRefresh

  Setting `repeatRefresh: true` causes a repeating tween to `invalidate()` and re-record its starting/ending values internally on each full iteration (not including yoyo's). This is useful when you use dynamic values (relative, random, or function-based). For example, `x: "random(-100, 100)"` would get a new random x value on each repeat. `duration`, `delay`, and `stagger` do **NOT** refresh.
* #### reversed

  If `true`, the animation will start out with its playhead reversed, meaning it will be oriented to move toward its start. Since the playhead begins at a time of 0 anyway, a reversed tween will *appear* paused initially because its playhead cannot move backward past the start.
* #### runBackwards

  If `true`, the animation will invert its starting and ending values (this is what a [from()](/docs/v3/GSAP/gsap.from()) tween does internally), though the ease doesn't get flipped. In other words, you can make a `to()` tween into a `from()` by setting `runBackwards: true`.
* #### stagger

  If multiple targets are defined, you can easily [stagger](https://codepen.io/GreenSock/pen/938f5cd34818443c43af9ba2692137a5) the start times for each by setting a value like `stagger: 0.1` (for 0.1 seconds between each start time). Or you can get much more advanced staggers by using a stagger object. For more information, see [the stagger documentation](/resources/getting-started/Staggers).
* #### startAt

  Defines starting values for any properties (even if they're not animating). For example, `startAt: {x: -100, opacity: 0}`
* #### yoyo

  If `true`, every other `repeat` iteration will run in the opposite direction so that the tween appears to go back and forth. This has no affect on the `reversed` property though. So if `repeat` is `2` and `yoyo` is `false`, it will look like: start - 1 - 2 - 3 - 1 - 2 - 3 - 1 - 2 - 3 - end. But if `yoyo` is `true`, it will look like: start - 1 - 2 - 3 - 3 - 2 - 1 - 1 - 2 - 3 - end. Default: `false`.
* #### yoyoEase

  Allows you to alter the ease in the tween's `yoyo` phase. Set it to a specific ease like `"power2.in"` or set it to `true` to simply invert the tween's normal `ease`. Note: GSAP is smart enough to automatically set `yoyo: true` if you define any `yoyoEase`, so there's less code for you to write. Default: `false`.
* #### keyframes

  To animate the targets to various states, use `keyframes` - an array of vars objects that serve as `to()` tweens. For example, `keyframes: [{x:100, duration:1}, {y:100, duration:0.5}]`. All keyframes will be perfectly sequenced back-to-back, but you can define a `delay` value to add spacing between each step (or a negative delay would create an overlap). Keyframes are only to be used in `to()` tweens.