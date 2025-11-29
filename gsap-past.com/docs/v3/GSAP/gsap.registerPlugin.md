---
source_url: "https://gsap.com/docs/v3/GSAP/gsap.registerPlugin()/"
title: "gsap.registerPlugin() | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:52:58.438220Z"
selector: "article"
---

# gsap.registerPlugin() | GSAP | Docs & Learning

* [GSAP](/docs/v3/GSAP/)
* methods
* gsap.registerPlugin()

On this page

Registering a plugin with the GSAP core ensures that the two work seamlessly together and also prevents tree shaking issues in build tools/bundlers. You only need to register a plugin once **before** using it, like:

```
//list as many as you'd like  
gsap.registerPlugin(MotionPathPlugin, TextPlugin);
```

There is no harm in registering the same plugin multiple times (but it doesn't help either).

The non ES module versions of GSAP plugins (like the minified files on the CDN) attempt to automatically register themselves upon load and that typically works great in the browser as long as they're loaded AFTER the core GSAP engine, but it's still a good habit to register plugins because in build environments (outside the browser), tree shaking can bite you.

Keep in mind that this is **not** a replacement for loading or importing the plugins themselves. This method is to be used after you have loaded the plugin simply to make GSAP's core aware of the plugin and to prevent tree shaking from occurring when using a build tool.

note

A note for React users to register the [useGSAP()](/resources/React) hook to avoid version conflicts.

## What's a plugin?[​](#whats-a-plugin "Direct link to What's a plugin?")

A [plugin](/docs/v3/Plugins) adds extra capabilities to GSAP's core. Some plugins make it easier to work with certain rendering libraries (like PIXI.js or EaselJS) while other plugins add the ability to do special things like [morphing](/docs/v3/Plugins/MorphSVGPlugin) SVG, adding [drag and drop](/docs/v3/Plugins/Draggable) functionality, etc.). This allows the GSAP core to remain relatively small and lets you add features when you need them.