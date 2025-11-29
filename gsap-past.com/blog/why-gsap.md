---
source_url: "https://gsap.com/blog/why-gsap/"
title: "What's so special about GSAP? | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:18:38.543581Z"
selector: "article"
---

# What's so special about GSAP? | GSAP | Docs & Learning

info

Feature lists don't always tell the story in a way that's relevant to you as the developer/designer in the trenches, trying to get **real work done** for **real clients**. You hear about theoretical benefits of CSS animations or some fancy new library that claims to solve various challenges, but then you discover things fall apart when you actually try to use it or the API is exceedingly cumbersome. You need things to **just work**.

#### loading...

The animation above uses GSAP to animate DOM elements. Try recreating it using CSS animations or another library. It would be a nightmare (or impossible). This illustrates why...

* GSAP has become the industry standard.
* Most award-winning sites use it.
* Google recommends GSAP for JavaScript animations.
* Over **11 million sites use GSAP**!

Here are some practical, real-world reasons why GSAP is so popular (click items to expand):

## Community![​](#community "Direct link to Community!")

Isn't it nice to know that if you find yourself in a bind, there's a huge community eager to help? GreenSock's large friendly community is one of its best features ***by far***. People rave about the outstanding support and warmth of [the forums](https://gsap.com/community/) which are full of generous developers who are passionate about animation. Swing by and see how active things are (over 100,000 posts!). Most open source projects have zero dedicated support whatsoever, or they force you to pay very high fees to get support. Not GreenSock.

## Performance[​](#performance "Direct link to Performance")

See the [speed comparison](https://codepen.io/GreenSock/full/srfxA) for yourself. GSAP is the fastest full-featured scripted animation tool on the planet. It's even faster than CSS animations/transitions and WAAPI in many cases. Get buttery smooth 60fps requestAnimationFrame-driven animations.

`lagSmoothing`

lagSmoothing automatically heals from CPU spikes while maintaining perfect synchronization.

What happens when the CPU gets bogged down and there's a lag between renders? Most other animation engines (including CSS animations in some browsers) slide the start time forward to compensate but there's a major drawback to that approach: it sacrifices synchronization and can mangle delays so that when you try to neatly stagger animations, they [spew out in clumps/groups](http://codepen.io/GreenSock/full/e3ac33404937de0eb77c789323367da8/). GSAP automatically implements lagSmoothing to heal from CPU spikes without those side effects.

Avoid layout thrashing

Some browsers ([notably Webkit](http://codepen.io/GreenSock/pen/16438623257ec198107d561a9456e95d?editors=001)) impose a performance penalty for sequential read/write/read/write of DOM-related properties, forcing a costly style recalculation for each cycle so it is better to group reading and then writing tasks (read/read/write/write is faster than read/write/read/write). GSAP takes special measures to solve these problems. Again, it's all automatic.

GPU acceleration, debouncing, grouped updates, and other optimizations

We obsess about performance optimizations so you don't have to. There are too many of these optimizations under the hood to list here, but hopefully you get the picture. Nothing is more sensitive to performance problems than animation especially on mobile devices, so make sure you choose a technology that minimizes the CPU load. GSAP delivers in spades.

## Jaw-dropping [scroll-effects](https://gsap.com/scroll/)[​](#jaw-dropping-scroll-effects "Direct link to jaw-dropping-scroll-effects")

[ScrollTrigger](https://gsap.com/docs/v3/Plugins/ScrollTrigger/) is unrivaled in terms of features and ease of use. Pinning, velocity tracking, smooth scrubbing, snapping, automatic resize handling, and LOTS more. Don't take our word for it - here are a few comments from the [YouTube Premiere](https://www.youtube.com/watch?v=X7IBa7vZjmo):

> "I've been in the industry for 20 years and I'm speechless"

> "I have never been so excited about a technology"

> "I must say the performance of this is great! Really silky smooth compared to anything else."

Looking for scroll smoothing? [We've got that covered](https://gsap.com/docs/v3/Plugins/ScrollSmoother/) too.

## Responsive, accessibility-friendly animations![​](#responsive-accessibility-friendly-animations "Direct link to Responsive, accessibility-friendly animations!")

With [gsap.matchMedia()](/docs/v3/GSAP/gsap.matchMedia()) you can easily customize animations for mobile and desktop devices and even honor "prefers-reduced-motion" settings. No other library has a feature like this.

Video Walkthrough

## Scale, rotate, skew, and move without the headaches[​](#scale-rotate-skew-and-move-without-the-headaches "Direct link to Scale, rotate, skew, and move without the headaches")

Animate each property distinctly (impossible with CSS animations/transitions)

Transforms are some of the most common properties to animate, but they're all lumped into one "transform" CSS3 property, making them almost impossible to [manage distinctly](http://codepen.io/GreenSock/full/kingu/). For example, what if you want to animate "rotation" and "scale" independently, with different timings and eases? This type of thing is incredibly common for animators, but it's impossible with most other systems including native CSS transitions/animations. Even WAAPI can't split apart x and y translation or scale. GSAP handles animating scaleX, scaleY, skewX, skewY, rotation, rotationX, rotationY, xPercent, yPercent, x, y, and z independently. You can also use 2D or 3D transformOrigin values. *IE9 (and earlier) doesn't support 3D transforms but 2D works great*.

Directional rotation (clockwise, counter-clockwise, or shortest)

GSAP is the only system that makes it simple to do [directional rotation](http://codepen.io/GreenSock/full/jiEyG/). For example, let's say you want to rotate to a particular value but you want it to go in the clockwise direction, or maybe counter-clockwise, or automatically choose the shortest path? With GSAP, you can add a "\_cw" (clockwise), "\_ccw" (counter-clockwise), or "\_short" (whichever is shortest) suffix and it handles things for you.

3D transforms work in modern browsers, 2D works back to IE9!

You don't need to apologize to your clients anymore, trying to explain why your cool animations break in IE9. GSAP just works.

* Make SVG transforms work consistently across browsers (including transform-origin)

Chrome, Firefox, IE, and Safari all handle CSS transforms (and transform-origin) applied to SVG elements in very different ways. So without GSAP the same rotation or scale animation would look completely different. GSAP does all the math behind the scenes to correctly apply the transform-origin and transform values so that you can animate SVG elements just like regular DOM elements. See Jack's [guest post on css-tricks.com](http://css-tricks.com/svg-animation-on-css-transforms/) for details.

## Animate anything[​](#animate-anything "Direct link to Animate anything")

DOM elements? Canvas library objects? Generic JS objects? No problem.

CSS3 animations/transitions only handle DOM elements, but what if you need to animate canvas library elements, like those from [PIXI.js](http://www.pixijs.com/) or [EaselJS](http://www.createjs.com)? What if you create your own objects and need to animate their properties or methods? Do you really want to have to switch toolsets and learn something completely new with a different animation syntax? Wouldn't it be nice if your code and toolset could be consistent? No other library handles such a wide variety of targets - GSAP can animate anything JavaScript can touch.

You're not locked into building your entire UI in a highly opinionated, proprietary API.

GSAP fits into just about any workflow. React, Vue, Angular, PixiJS, ThreeJS, canvas, whatever. GSAP fits anywhere.

Colors, complex values like boxShadow, and almost any css property

GSAP allows you to define your css values in the same format you normally would in regular css and it handles the interpolation and browser differences for you. For example, backgroundColor could be "#F00" or "red" or hsl(0,100%,50%) or "#FF0000" or "rgb(255,0,0)". And boxShadow could be "10px 10px black" or "50px 50px 20px black" or "50px 50px 50px 20px blue".

Properties or methods

Animate any property of any object like `obj.prop`, or even use method-based getters/setters where `obj.prop()` is a getter and `obj.prop(value)` is a setter. GSAP automatically senses whether it's a property or method and handles it accordingly.

Interpolate units

Animating a %-based width to px? No problem. How about em to %? GSAP handles conversion for you internally. Same for color values in various formats.

Animate Arrays, use selector text or direct Element references

Pass almost anything to GSAP as the target, and it'll figure out how to handle it. Got an Array of 100 elements? No problem. A React ref? Sure. You don't need to loop through them yourself and create a bunch of tweens. And if you pass selector text as the target, it'll use `document.querySelectorAll()`. Again, it "just works".

## Easy workflow, refined tools, total control[​](#easy-workflow-refined-tools-total-control "Direct link to Easy workflow, refined tools, total control")

This is a **major** difference that most people don't even realize until they spend some time with GSAP. It's like when smart phones first came out and nobody realized how limited their "dumb phones" were until they saw what was possible with new technology.

Advanced playback controls and debugging with [GSDevTools](/docs/v3/Plugins/GSDevTools/)

Get a visual UI for interacting with and debugging GSAP animations, complete with advanced playback controls, keyboard shortcuts, global synchronization and more. Jump to specific scenes, set in/out points, play in slow motion to reveal intricate details, and even switch to a "minimal" mode on small screens. GSDevTools makes building and reviewing GSAP animations simply delightful.

Video Walkthrough

Unparalleled sequencing (pardon the pun)

In GSAP, you can chain sequences together in no time, even with overlaps and/or gaps (most systems only accommodate one-after-the-other sequencing with no overlaps or everything runs in parallel) and then control the whole thing as a single instance. GSAP's timeline delivers unprecedented control.

Polymorphism, object-oriented architecture, and nesting

Tween and Timeline classes extend a common "Animation" class, so they share common methods like pause(), resume(), reverse(), restart(), play(), seek(), and even timeScale(). That's a big deal workflow-wise because you can write methods that spit back any animation (a tween or timeline) that can get nested into another timeline which can also be nested, etc. There's no limit. Then you can control that master timeline very easily and everything remains perfectly synchronized. This allows modularized code that is much easier to maintain.

Advanced staggering

Advanced staggering makes it surprisingly simple to get rich, organic timing effects with very little code. Each tween's start time can be distributed according to any ease and/or based on how close each element is to a position in the list. For example, you can have things emanate outward from the "center" or a certain index. It'll even accommodate grids, complete with auto-calculated columns and rows (great for responsive layouts)!

Video Walkthrough

Repeat, yoyo, restart(), seek(), reverse() entire sequences on the fly

You have complete control over the animation at runtime. You can build an entire banner ad, for example, tuck it in a Timeline and set it to repeat a certain number of times or indefinitely. The `seek()` method can be great during production because if you're building a lengthy animation, you can add a seek() call to jump to the spot you're working on so that you don't have to keep watching the first part over and over again while you're tweaking timings toward the end. Then remove that seek() call when you want it to run from the beginning.

 Rich callback system

It's pretty common for other frameworks to only offer an onComplete callback, but GSAP also offers onStart, onUpdate, onRepeat, and onReverseComplete. You can even pass any number of parameters, including a self-reference to the tween itself using `self`. Add any of these callbacks to timelines too so that they run after all child tweens are done rendering.

Animate along Bezier paths with auto rotation, momentum, physics, and advanced effects

Plugins are available that make some very advanced effects simple. MotionPathPlugin will even allow you to feed it some points and it'll draw a smooth Bezier through those points and then animate your object along that path. InertiasPlugin is great for things like flick-scrolling, complete with smooth handling of boundaries, elegant bounce-back, automatic velocity tracking, and more.

FLIP technique taken to a whole new level

GSAP's [Flip plugin](/docs/v3/Plugins/Flip/) accomplishes feats that no other tool can. It elegantly handles nested transforms and makes movement of even reparented elements seamless. Watch the video and prepare to be amazed.

Video Walkthrough

Relative values using "+=" and "-=" prefixes

Instead of defining an absolute end value for your tween, you can make it relative to whatever it is when the tween starts. For example, y:"+=100" would add 100 to whatever "y" is when the tween starts.

Intelligent overwriting, gc management, and more

Want to kill all tweens of a particular object? Easy. How about killing individual portions of a tween (like just the “rotation”, but let the “scale” keep animating)? No problem. Intelligent overwriting with various modes to choose from? Of course. Automatic garbage collection management? You betcha. An architecture that keeps the timing of every tween perfectly synchronized with the others? Yep. How about repeats that don't suffer time slips from gaps that build up like in other systems. Check. A global ticker that you can tap into for running your own logic on each frame? Sure. There are all sorts of little features and refinements that came from years of usage in the trenches that other engines don't address.

## Custom Easing![​](#custom-easing "Direct link to Custom Easing!")

Imagine literally **\*\*any\*\*** easing curve, with as many control points as you want...that's what GSAP's [CustomEase](/docs/v3/Eases/CustomEase) delivers. All of the standard easing options are available too, of course, plus some exclusive ones like [ExpoScaleEase](/docs/Eases/ExpoScaleEase), SlowMo, RoughEase, [CustomWiggle & CustomBounce](/docs/v3/Eases/CustomWiggle/) and SteppedEase which are completely configurable, giving you just the "feel" that you want. See the unique [Ease Visualizer](/docs/v3/Eases) for all the options.

## Physics[​](#physics "Direct link to Physics")

Check out [Draggable](/docs/v3/Plugins/Draggable/) to see some of our most impressive work related to physics. Notice how smooth and natural the interaction is, and how you can impose boundaries, snapping, and even ensure that properties land on exact values or within ranges that you define. Flick, spin, or scroll, all with delightful responsiveness. This isn't limited to dragging, though - InertiaPlugin lets you get this kind of incredible momentum-based animation on **ANY** property of **ANY** object.

## Solve browser compatibility issues[​](#solve-browser-compatibility-issues "Direct link to Solve browser compatibility issues")

SVG quirks vanish

When you start animating SVG, you'll quickly run into frustrating browser inconsistencies and bugs like transform-origin glitches, stroke-dasharray rendering oddities, and lots more...unless you're using GSAP which automatically works around many of those issues.

Avoid browser bugs

GSAP works around scores of browser bugs. For example, if you try to animate 3D transforms in Firefox, objects will flicker in many cases. iOS Safari sometimes stops dispatching requestAnimationFrame events in certain scenarios which would cause other engines to completely break. If you don't set a zIndex, iOS won't render transforms correctly in some scenarios, and there's a major bug in Safari's 3D transformOrigin behavior. GSAP implements workarounds under the hood, so things "just work". Again, you write clean code and let GSAP juggle the tough stuff.

CSS transitions/animations or WAAPI won't work in some browsers; GSAP does

People can talk all they want about theoretical benefits of CSS animations/transitions or WAAPI but in the real world, clients need things to actually work even in older browsers. GSAP delivers the compatibility you need.

## Exclusive SVG wizardry (with cross-browser support)[​](#exclusive-svg-wizardry-with-cross-browser-support "Direct link to Exclusive SVG wizardry (with cross-browser support)")

No other animation tool supports SVG as well or as intuitively as GSAP. Neither CSS animations nor SVG's very own SMIL (soon to be deprecated by some browsers) deliver cross-browser support. Plus GSAP's powerful [DrawSVGPlugin](/docs/v3/Plugins/DrawSVGPlugin) and [MorphSVGPlugin](https://gsap.com/morphSVG) open up a whole new world of SVG animation effects.

Morphing (shape tweening)

[MorphSVG](https://gsap.com/morphSVG) allows you to morph any SVG `<path>` regardless of how many points are in the starting and ending paths. You will be blown away by the results

transformOrigin

The way browsers handle transformOrigin (the point around which scale and rotation occur) is very different due to the SVG spec and its buggy implementation. GSAP normalizes behavior by allowing you to set transformOrigin in the exact same way you would with a DOM element and get the same results.

Animate SVG strokes

[DrawSVG](/docs/v3/Plugins/DrawSVGPlugin) gives you precise control over how SVG strokes are revealed. In addition to just making a stroke reveal from end to end, you can reveal from center and use any segment length you choose.

Percentage-based transforms

The SVG spec doesn't even allow for percentage-based transforms, but GSAP does! You can easily move an SVG element based on a percentage of its width or height. This feature is great for responsive designs.

  

For more details and tons of demo's illustrating GSAP's unique SVG support read [SVG Power Tips](/resources/svg/).

## But what about file size?[​](#but-what-about-file-size "Direct link to But what about file size?")

Definitely check out the [Rethinking Kilobytes](/blog/size) article that explains why you shouldn't adopt a simplistic "aggregate total file size" mindset from yesteryear. There are some very [important factors](/blog/size) that loading GSAP a very wise choice in most cases.

Zero dependencies

GSAP will integrate nicely with React, Vue, Angular, or virtually any other framework.

Lightweight & modular

The core GSAP may be all you need because it's got a surprising amount of functionality packed in, but there are also plugins available that add features while keeping the core small.

Robust CDN Deliverys

GSAP is hosted on the [CDNJS](http://www.cdnjs.com) CDN network, so you can get excellent load times and leverage browser caching. The more sites that use the CDN files, the more everyone will benefit. Imagine if the banner ad networks standardized on GSAP - not only would everything load faster because it'd be cached so pervasively, but they could choose not to count GSAP's file size against the banner ad's cap which would be a huge win for banner ad creators. Or at least it could be a competitive advantage for the networks who adopt that policy.

Less code

"But wait," you may say, "CSS animations and transitions don't require any js files, so aren't they better for load times?" In some cases when you're not doing much animation, yes, although you give up a lot in terms of compatibility and workflow. But CSS animations are far more verbose, so the file size advantage shifts quickly back to GSAP the more animation you do. The other thing to keep in mind is that GSAP’s JS file(s) are typically cached by the browser, so the savings page-to-page is much larger since the code you write on each page is far more concise. In other words, think of how much js/css the browser must actually request from the server over the course of your users' multi-page visit to your site.

Don't take our word for it

If you're still wondering what the big deal about GSAP is, we'd encourage you to find someone who is proficient with it and ask about their experience. Usually people who take the time to learn it have a "light bulb" moment pretty quickly and never want to go back to using other libraries or CSS. It's difficult to explain to the uninitiated - lists of features don't really do it justice. It's about feeling empowered to animate almost anything you can imagine with minimal code.

## Conclusion[​](#conclusion "Direct link to Conclusion")

GSAP was engineered and refined over a decade by professional animators in the trenches with practical concerns in mind. It's built to handle everything from simple fades to rich, immersive experiences packed with all sorts of animation. It's not a throwaway one-trick-pony library that you toss into a project here and there; it's built to give you a rock-solid animation workflow across all of your projects. And it's crazy fast. Perhaps that's why Google recommends GSAP for JavaScript animations and it's used in over **12 million sites**. GSAP has been actively maintained and developed for 14+ years, and there are no plans to stop. We've got lots of exciting things planned.