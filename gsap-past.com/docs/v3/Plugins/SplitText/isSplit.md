---
source_url: "https://gsap.com/docs/v3/Plugins/SplitText/isSplit"
title: "isSplit | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:14:56.549000Z"
selector: "article"
---

# isSplit | GSAP | Docs & Learning

* [SplitText](/docs/v3/Plugins/SplitText/)
* properties
* .isSplit

On this page

# isSplit

### isSplit : Boolean

Whether the text is currently split.

### Details[​](#details "Direct link to Details")

A boolean that indicates whether the element is currently split. When `true`, the SplitText instance has performed a split and (depending on which types you split by) the `.chars`, `.words`, `.lines`, or `.masks` arrays will be populated. Use `.revert()` to undo the split and reset `isSplit` to `false`.