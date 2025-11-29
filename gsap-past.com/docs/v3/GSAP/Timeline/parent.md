---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/parent"
title: "parent | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:11:04.496429Z"
selector: "article"
---

# parent | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
* properties
* .parent

On this page

# parent

### parent : Timeline

The parent [Timeline](/docs/v3/GSAP/Timeline) to which the animation is attached. Anything that's not in a Timeline that you create is placed on the [gsap.globalTimeline](/docs/v3/GSAP/gsap.globalTimeline) by default.

### Details[​](#details "Direct link to Details")

The parent [Timeline](/docs/v3/GSAP/Timeline) to which the Timeline is attached. Anything that's not inside a Timeline that you create is placed on the [gsap.globalTimeline](/docs/v3/GSAP/gsap.globalTimeline()) by default.

Each animation ([Tweens](/docs/v3/GSAP/Tween) and [Timelines](/docs/v3/GSAP/Timeline)) can only exist in one parent. Think of it like a DOM element that can't have multiple parents. If you [add()](/docs/v3/GSAP/Timeline/add()) an animation to a different Timeline, its `parent` will change to that Timeline.

## How do timelines work?[​](#how-do-timelines-work "Direct link to How do timelines work?")

See the [Timeline docs for details](/docs/v3/GSAP/Timeline#mechanics). It's very helpful to understand how the mechanics work conceptually.