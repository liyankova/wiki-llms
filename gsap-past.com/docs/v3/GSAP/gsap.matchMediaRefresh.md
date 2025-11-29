---
source_url: "https://gsap.com/docs/v3/GSAP/gsap.matchMediaRefresh()"
title: "gsap.matchMediaRefresh() | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:55:36.453061Z"
selector: "article"
---

# gsap.matchMediaRefresh() | GSAP | Docs & Learning

* [GSAP](/docs/v3/GSAP/)
* methods
* gsap.matchMediaRefresh()

On this page

Immediately reverts all active/matching [MatchMedia](/docs/v3/GSAP/gsap.matchMedia()) objects and then runs any that currently match. This can be particularly useful when you need to accommodate a UI checkbox that toggles something like "reduce motion":

## Demo[​](#demo "Direct link to Demo")

#### loading...

note

Note that it does **not** destroy any gsap.matchMedia() instances. It simply reverts any currently matching ones, and then re-runs any that match. Think of it almost like what would happen if you completely resized the window in such a way that all currently matching ones no longer matched, and then the window got resized back to the original size so that they match again.