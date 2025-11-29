---
source_url: "https://gsap.com/docs/v3/Plugins/MorphSVGPlugin/static.defaultUpdateTarget"
title: "static-defaultUpdateTarget | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:18:27.925102Z"
selector: "article"
---

# static-defaultUpdateTarget | GSAP | Docs & Learning

* more plugins
* [MorphSVG](/docs/v3/Plugins/MorphSVGPlugin)
* properties
* MorphSVGPlugin.defaultUpdateTarget

On this page

# MorphSVGPlugin.defaultUpdateTarget

### MorphSVGPlugin.defaultUpdateTarget : Boolean

Sets the default `updateTarget` value for all MorphSVG animations; if `true`, the original tween target (typically an SVG `<path>` element) itself gets updated during the tween.

### Details[​](#details "Direct link to Details")

Sets the default `updateTarget` value for all MorphSVG animations; if `true`, the original tween target (typically an SVG `<path>` element) itself gets updated during the tween. If you've got a render function set up to draw to `<canvas>`, for example, then it may be wasteful to update the original target as well (duplicate efforts). Ultimately this is a performance optimization. Setting it to `false` allows MorphSVG to skip that step.