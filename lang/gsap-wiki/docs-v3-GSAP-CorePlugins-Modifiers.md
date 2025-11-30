---
url: https://gsap.com/docs/v3/GSAP/CorePlugins/Modifiers
title: Modifiers | GSAP | Docs & Learning
source_domain: gsap.com
---

# Modifiers | GSAP | Docs & Learning

What are internal plugins?

ModifiersPlugin is an internal plugin, It is **automatically included in GSAP's core** and **doesn't have to be loaded using gsap.registerPlugin()**.

You can think of internal plugins as just a part of GSAP.

### Description[​](https://gsap.com/docs/v3/GSAP/CorePlugins/Modifiers#description "Direct link to Description")

You can define a "modifier" function for almost any property. This modifier intercepts the value that GSAP would normally apply on each update ("tick"), feeds it to your function as the first parameter and lets you run custom logic, returning a new value that GSAP should then apply. This is perfect for tasks like snapping, clamping, wrapping, or other dynamic effects.

### value, target[​](https://gsap.com/docs/v3/GSAP/CorePlugins/Modifiers#value-target "Direct link to value, target")

The modifier functions are passed two parameters:

1. `value` (*number* | *string*) - The about-to-be-applied value from the regular tween. This is often a number, but could be a string based on whatever the property requires. For example if you're animating the `x` property, it would be a number, but if you're animating the `left` property it could be something like `"212px"`, or for the `boxShadow` property it could be `"10px 5px 10px rgb(255,0,0)"`.
2. target (*object*) - The target itself.

For example, change the `x` of one object based on the `y` of another object or change `rotation` based on the `direction` it is moving. Below are some examples that will help you get familiarized with the syntax.

### Snap rotation[​](https://gsap.com/docs/v3/GSAP/CorePlugins/Modifiers#snap-rotation "Direct link to Snap rotation")

The tween below animates 360 degrees but the modifier function forces the value to jump to the closest 45-degree increment. Take note how the modifier function gets passed the value of the property that is being modified, in this case a `rotation` number.

#### loading...

If snapping is all that you're wanting to do, we recommend using the [SnapPlugin](https://gsap.com/docs/v3/GSAP/CorePlugins/Snap) that is built into GSAP's core.

### Clamp with Modulus[​](https://gsap.com/docs/v3/GSAP/CorePlugins/Modifiers#clamp-with-modulus "Direct link to Clamp with Modulus")

The tween below animates `x` to 500 but the modifier function forces the value to wrap so that it's always between 0 and 100.

#### loading...

Here's the same sort of technique but using GSAP's [wrap utility function](https://gsap.com/docs/v3/GSAP/UtilityMethods/wrap()):

#### loading...

### Carousel Wrap[​](https://gsap.com/docs/v3/GSAP/CorePlugins/Modifiers#carousel-wrap "Direct link to Carousel Wrap")

Have you ever built a carousel and wrestled with making it loop seamlessly? Perhaps you duplicated each asset or wrote some code that moved each item back to the beginning when it reached the end. With ModifiersPlugin you can get a seamless repeating carousel with a single `.to()` with a `stagger`! The example below tweens each box to a relative `x` position of `"+=500"`. Click the "show overflow" button to see each box get reset to `x: 0` when it goes beyond 500.

#### loading...

### Advanced demos[​](https://gsap.com/docs/v3/GSAP/CorePlugins/Modifiers#advanced-demos "Direct link to Advanced demos")

We've only scratched the surface of what ModifiersPlugin can do. Our moderator [Blake Bowen](https://gsap.com/community/profile/21420-osublake/) has been putting this plugin to the test and has an [impressive collection of demos](https://codepen.io/collection/AWxOyk/) that will surely inspire you.

### Caveats:[​](https://gsap.com/docs/v3/GSAP/CorePlugins/Modifiers#caveats "Direct link to Caveats:")

* To modify CSS transform's `scale`, use `scaleX` and `scaleY` (since it's a shortcut for those). And use `rotation`, not `rotationZ`.
* RoundPropsPlugin and SnapPlugin tap into the same mechanism internally as ModifiersPlugin (to maximize efficiency, minimize memory, and keep kb down). Think of a `roundProps` tween as just a shortcut that creates a modifier that applies `Math.round()`, thus you cannot do *both*`roundProps` and a modifier on the same property. It's easy to get that functionality, though, by just doing `Math.round()` inside the modifier function.

## FAQs[​](https://gsap.com/docs/v3/GSAP/CorePlugins/Modifiers#faqs "Direct link to FAQs")

#### How do I include this plugin in my project?

Simply load GSAP's core - ModifiersPlugin is included automatically!

#### Do I need to register ModifiersPlugin?

Nope. ModifiersPlugin and other core plugins are built into the core and don't have to be registered.