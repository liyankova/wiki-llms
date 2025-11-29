---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollTrigger/static.maxScroll()"
title: "static-maxScroll | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:13:50.334421Z"
selector: "article"
---

# static-maxScroll | GSAP | Docs & Learning

* [ScrollTrigger](/docs/v3/Plugins/ScrollTrigger/)
* methods
* ScrollTrigger.maxScroll()

On this page

# ScrollTrigger.maxScroll

### ScrollTrigger.maxScroll( scroller:Element | window, horizontal:Boolean ) : Number

A utility function for getting the maximum scroll value for a particular element/scroller. For example, if the element/scroller is 500px tall and contains 800px of content, maxScroll() would return 300.

#### Parameters

* #### **scroller**: Element | window

  The element whose maximum scroll should be returned
* #### **horizontal**: Boolean

  By default, vertical scrolling is assumed, but if you'd like to find the maximum horizontal scroll, set horizontal to `true`

### Returns : Number[​](#returns--number "Direct link to Returns : Number")

The maximum scroll value (in pixels)

### Details[​](#details "Direct link to Details")

A utility function for getting the maximum scroll value for a particular element/scroller. For example, if the element/scroller is 500px tall and contains 800px of content, maxScroll() would return 300.