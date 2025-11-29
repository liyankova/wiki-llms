---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollTrigger/static.clearMatchMedia()"
title: "static-clearMatchMedia | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:13:25.434709Z"
selector: "article"
---

# static-clearMatchMedia | GSAP | Docs & Learning

* [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/)
* methods
* ScrollTrigger.clearMatchMedia()

Deprecated

Shift to [gsap.matchMedia()](/docs/v3/GSAP/gsap.matchMedia()) functionality in version 3.11.0+

# ScrollTrigger.clearMatchMedia

### ScrollTrigger.clearMatchMedia( query:String )

#### Parameters

* #### **query**: String

  [optional] To clear just one specific break point, provide the media query string here, like `"(min-width: 800px)"`. If none is provided, **ALL** will be cleared.

Clears out breakpoints that were previously set via [ScrollTrigger.matchMedia()](/docs/v3/Plugins/ScrollTrigger/static.matchMedia()). It doesn't kill the associated ScrollTriggers or animations themselves - it just no longer triggers anything at that break point.