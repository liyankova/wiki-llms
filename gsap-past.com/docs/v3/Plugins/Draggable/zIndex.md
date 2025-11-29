---
source_url: "https://gsap.com/docs/v3/Plugins/Draggable/zIndex"
title: "zIndex | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:17:50.036426Z"
selector: "article"
---

# zIndex | GSAP | Docs & Learning

* more plugins
* [Draggable](/docs/v3/Plugins/Draggable/)
* properties
* .zIndex

On this page

# zIndex

### zIndex : Number

[static] The starting zIndex that gets applied by default when an element is pressed/touched (for positional types, like `"x,y"`, `"top,left"`, etc.

### Details[​](#details "Direct link to Details")

*Number* - The starting `zIndex` that gets applied by default when an element is pressed/touched (for positional types, like `"x,y"`, `"top,left"`, etc. but not `"rotation"` or `"scroll"`) and this number gets incremented and applied to each new element that gets pressed/touched so that the stacking order looks correct (newly pressed objects rise to the top) unless `zIndexBoost: false` is set in a particular Draggable's `vars` parameter. You can set this `zIndex` to whatever you want, but `1000` is the default.

```
Draggable.zIndex = 500;
```