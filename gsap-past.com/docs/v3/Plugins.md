---
source_url: "https://gsap.com/docs/v3/Plugins/"
title: "Plugins | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:44:20.767831Z"
selector: "article"
---

# Plugins | GSAP | Docs & Learning

* What's a plugin?

On this page

info

A plugin adds extra capabilities to GSAP's core. This allows the GSAP core to remain relatively small and lets you add features only when you need them.

## Plugin Overview[​](#plugin-overview "Direct link to Plugin Overview")

## Included in GSAP's Core

* [## GSAP](/docs/v3/GSAP)CDN

[Tween](/docs/v3/GSAP/Tween) and [Timeline](/docs/v3/GSAP/Timeline)

### Animate anything

* [CSS properties](/docs/v3/GSAP/CorePlugins/CSS)
* [Attributes](/docs/v3/GSAP/CorePlugins/Attributes)
* [Array Values](/docs/v3/GSAP/CorePlugins/EndArray)
* [and more...](/resources/get-started#any-numeric-value-color-or-complex-string-containing-numbers)

### [Eases](/docs/v3/Eases)

* ["none"](/docs/v3/Eases)
* ["power1"](/docs/v3/Eases)
* ["power2"](/docs/v3/Eases)
* ["power3"](/docs/v3/Eases)
* ["power4"](/docs/v3/Eases)
* ["back"](/docs/v3/Eases)
* ["bounce"](/docs/v3/Eases)
* ["circ"](/docs/v3/Eases)
* ["elastic"](/docs/v3/Eases)
* ["expo"](/docs/v3/Eases)
* ["sine"](/docs/v3/Eases)
* ["steps(n)"](/docs/v3/Eases/SteppedEase)

### Animate efficiently

* [Staggers](/resources/getting-started/Staggers)
* [Callbacks](/resources/getting-started/control#callbacks)
* [Snapping](/docs/v3/GSAP/CorePlugins/Snap)
* [Modifiers](/docs/v3/GSAP/CorePlugins/Modifiers)
* [Keyframes](/resources/keyframes)
* [Ticker with lag smoothing](/docs/v3/GSAP/gsap.ticker())
* [Cleanup - context() & revert()](/docs/v3/GSAP/gsap.context())
* [Responsivity & Accessibility - matchMedia()](/docs/v3/GSAP/gsap.matchMedia())

### [Utility Methods](/docs/v3/GSAP/UtilityMethods)

* [checkPrefix()](/docs/v3/GSAP/UtilityMethods/checkPrefix())
* [clamp()](/docs/v3/GSAP/UtilityMethods/clamp())
* [distribute()](/docs/v3/GSAP/UtilityMethods/distribute())
* [getUnit()](/docs/v3/GSAP/UtilityMethods/getUnit())
* [interpolate()](/docs/v3/GSAP/UtilityMethods/interpolate())
* [mapRange()](/docs/v3/GSAP/UtilityMethods/mapRange())
* [normalize()](/docs/v3/GSAP/UtilityMethods/normalize())
* [pipe()](/docs/v3/GSAP/UtilityMethods/pipe())
* [random()](/docs/v3/GSAP/UtilityMethods/random())
* [selector()](/docs/v3/GSAP/UtilityMethods/selector())
* [shuffle()](/docs/v3/GSAP/UtilityMethods/shuffle())
* [snap()](/docs/v3/GSAP/UtilityMethods/snap())
* [splitColor()](/docs/v3/GSAP/UtilityMethods/splitColor())
* [toArray()](/docs/v3/GSAP/UtilityMethods/toArray())
* [unitize()](/docs/v3/GSAP/UtilityMethods/unitize())
* [wrap()](/docs/v3/GSAP/UtilityMethods/wrap())
* [wrapYoyo()](/docs/v3/GSAP/UtilityMethods/wrapYoyo())

### Scroll Plugins

* [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger)

  CDN
* [ScrollTo](/docs/v3/Plugins/ScrollToPlugin)

  CDN
* [ScrollSmoother](/docs/v3/Plugins/ScrollSmoother)

  requires [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger)

  CDN

### Text Plugins

* [SplitText](/docs/v3/Plugins/SplitText)

  CDN
* [ScrambleText](/docs/v3/Plugins/ScrambleTextPlugin)

  CDN
* [Text Replacement](/docs/v3/Plugins/TextPlugin)

  CDN

### SVG Plugins

* [DrawSVG](/docs/v3/Plugins/DrawSVGPlugin)

  CDN
* [MorphSVG](/docs/v3/Plugins/MorphSVGPlugin)

  CDN
* [MotionPath](/docs/v3/Plugins/MotionPathPlugin)

  CDN
* [MotionPathHelper](/docs/v3/Plugins/MotionPathHelper)

  CDN

### UI Plugins

* [Flip](/docs/v3/Plugins/Flip)

  CDN
* [Draggable](/docs/v3/Plugins/Draggable)

  CDN
* [Inertia](/docs/v3/Plugins/InertiaPlugin)

  CDN
* [Observer](/docs/v3/Plugins/Observer)

  CDN

### Other Plugins

* [Physics2D](/docs/v3/Plugins/Physics2DPlugin)

  CDN
* [PhysicsProps](/docs/v3/Plugins/PhysicsPropsPlugin)

  CDN
* [GSDevTools](/docs/v3/Plugins/GSDevTools)

  CDN
* [Easel](/docs/v3/Plugins/EaselPlugin)

  CDN
* [Pixi](/docs/v3/Plugins/PixiPlugin)

  CDN

### Eases

* [CustomEase](/docs/v3/Eases/CustomEase)

  CDN
* [EasePack](/docs/v3/Eases/CustomWiggle)

  [rough](/docs/v3/Eases/RoughEase), [slow](/docs/v3/Eases/SlowMo), and [expoScale](/docs/v3/Eases/ExpoScaleEase)

  CDN
* [CustomWiggle](/docs/v3/Eases/CustomWiggle)

  requires [CustomEase](/docs/v3/Eases/CustomEase)

  CDN
* [CustomBounce](/docs/v3/Eases/CustomBounce)

  requires [CustomEase](/docs/v3/Eases/CustomEasee)

  CDN

### React

* [useGSAP()](https://gsap.com/resources/React)

  npm

## Installing/Loading a plugin[​](#installingloading-a-plugin "Direct link to Installing/Loading a plugin")

At the end of the day, all the plugins are just JS files - just like the core library. You can install them with script tags, via npm, with yarn, or even with a tgz file.

Head on over to our [install helper](/docs/v3/Installation) to choose your own adventure.

## Registering a plugin[​](#registering-a-plugin "Direct link to Registering a plugin")

Registering a plugin with the GSAP core ensures that the two work seamlessly together and also prevents tree shaking issues in build tools/bundlers. You only need to register a plugin once before using it, like:

```
//list as many as you'd like  
gsap.registerPlugin(MotionPathPlugin, ScrollTrigger, MorphSVGPlugin);
```

Obviously you need to load the plugin file first. There is no harm in registering the same plugin multiple times (but it doesn't help either).