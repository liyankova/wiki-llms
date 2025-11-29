---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollTrigger/static.saveStyles()"
title: "static-saveStyles | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:14:03.229175Z"
selector: "article"
---

# static-saveStyles | GSAP | Docs & Learning

* [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/)
* methods
* ScrollTrigger.saveStyles()

On this page

# ScrollTrigger.saveStyles

### ScrollTrigger.saveStyles( targets:String | Element | Array )

Internally records the current inline CSS styles for the given elements so that when ScrollTrigger reverts (typically for a refresh() or matchMedia() change) those elements will be reverted accordingly even if they had animations that added/changed inline styles. Think of it like taking a snapshot of the inline CSS and telling ScrollTrigger "re-apply these inline styles only and dump all others when you revert internally".

#### Parameters

* #### **targets**: String | Element | Array

  Selector text like `".panel, #logo"` or an element or an Array of elements whose current inline CSS styles should be recorded internally.

### Details[​](#details "Direct link to Details")

Internally records the current inline CSS styles for the given elements so that when ScrollTrigger reverts (typically for a [refresh()](/docs/v3/Plugins/ScrollTrigger/static.refresh()) or [matchMedia()](/docs/v3/Plugins/ScrollTrigger/static.matchMedia()) change) those elements will be reverted accordingly even if they had animations that added/changed inline styles. Think of it like taking a snapshot of the inline CSS and telling ScrollTrigger *"re-apply these inline styles only and dump all others when you revert internally"*.

Walkthrough

## Example[​](#example "Direct link to Example")

```
ScrollTrigger.saveStyles(".panel, #logo");
```

ScrollTrigger.saveStyles() was added in GSAP **3.4.0**