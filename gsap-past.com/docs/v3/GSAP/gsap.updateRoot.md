---
source_url: "https://gsap.com/docs/v3/GSAP/gsap.updateRoot()"
title: "gsap.updateRoot() | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:56:00.914110Z"
selector: "article"
---

# gsap.updateRoot() | GSAP | Docs & Learning

* [GSAP](/docs/v3/GSAP/)
* methods
* gsap.updateRoot()

Normally GSAP handles all of its timing internally using a `requestAnimationFrame` loop (or falls back to `setTimeout()` if rAF isn't available), but some game developers requested a way to manually update the root (global) timeline which is exactly what `gsap.updateRoot()` permits. This is only intended for **advanced** users. First, you'd need to unhook GSAP's ticker like this:

```
//unhooks the GSAP ticker  
gsap.ticker.remove(gsap.updateRoot);
```

And then you can update it with your own custom time like:

```
//sets the root time to 20 seconds manually  
gsap.updateRoot(20);
```