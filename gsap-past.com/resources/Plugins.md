---
source_url: "https://gsap.com/resources/Plugins/"
title: "Plugins | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:46:07.371356Z"
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

[Tween](/resources/Plugins/GSAP/Tween) and [Timeline](/resources/Plugins/GSAP/Timeline)

### Animate anything

* [CSS properties](/resources/Plugins/GSAP/CorePlugins/CSS)
* [Attributes](/resources/Plugins/GSAP/CorePlugins/Attributes)
* [Array Values](/resources/Plugins/GSAP/CorePlugins/EndArray)
* [and more...](/resources/get-started#any-numeric-value-color-or-complex-string-containing-numbers)

### [Eases](/resources/Plugins/Eases)

* ["none"](/resources/Plugins/Eases)
* ["power1"](/resources/Plugins/Eases)
* ["power2"](/resources/Plugins/Eases)
* ["power3"](/resources/Plugins/Eases)
* ["power4"](/resources/Plugins/Eases)
* ["back"](/resources/Plugins/Eases)
* ["bounce"](/resources/Plugins/Eases)
* ["circ"](/resources/Plugins/Eases)
* ["elastic"](/resources/Plugins/Eases)
* ["expo"](/resources/Plugins/Eases)
* ["sine"](/resources/Plugins/Eases)
* ["steps(n)"](/resources/Plugins/Eases/SteppedEase)

### Animate efficiently

* [Staggers](/resources/getting-started/Staggers)
* [Callbacks](/resources/getting-started/control#callbacks)
* [Snapping](/resources/Plugins/GSAP/CorePlugins/Snap)
* [Modifiers](/resources/Plugins/GSAP/CorePlugins/Modifiers)
* [Keyframes](/resources/keyframes)
* [Ticker with lag smoothing](/resources/Plugins/GSAP/gsap.ticker())
* [Cleanup - context() & revert()](/resources/Plugins/GSAP/gsap.context())
* [Responsivity & Accessibility - matchMedia()](/resources/Plugins/GSAP/gsap.matchMedia())

### [Utility Methods](/resources/Plugins/GSAP/UtilityMethods)

* [checkPrefix()](/resources/Plugins/GSAP/UtilityMethods/checkPrefix())
* [clamp()](/resources/Plugins/GSAP/UtilityMethods/clamp())
* [distribute()](/resources/Plugins/GSAP/UtilityMethods/distribute())
* [getUnit()](/resources/Plugins/GSAP/UtilityMethods/getUnit())
* [interpolate()](/resources/Plugins/GSAP/UtilityMethods/interpolate())
* [mapRange()](/resources/Plugins/GSAP/UtilityMethods/mapRange())
* [normalize()](/resources/Plugins/GSAP/UtilityMethods/normalize())
* [pipe()](/resources/Plugins/GSAP/UtilityMethods/pipe())
* [random()](/resources/Plugins/GSAP/UtilityMethods/random())
* [selector()](/resources/Plugins/GSAP/UtilityMethods/selector())
* [shuffle()](/resources/Plugins/GSAP/UtilityMethods/shuffle())
* [snap()](/resources/Plugins/GSAP/UtilityMethods/snap())
* [splitColor()](/resources/Plugins/GSAP/UtilityMethods/splitColor())
* [toArray()](/resources/Plugins/GSAP/UtilityMethods/toArray())
* [unitize()](/resources/Plugins/GSAP/UtilityMethods/unitize())
* [wrap()](/resources/Plugins/GSAP/UtilityMethods/wrap())
* [wrapYoyo()](/resources/Plugins/GSAP/UtilityMethods/wrapYoyo())

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