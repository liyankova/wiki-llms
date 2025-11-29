---
source_url: "https://gsap.com/docs/v3/Plugins/SplitText/masks"
title: "masks | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:15:00.647498Z"
selector: "article"
---

# masks | GSAP | Docs & Learning

* [SplitText](/docs/v3/Plugins/SplitText/)
* properties
* .masks

On this page

# masks

### masks : Array<Element>

Wrapper elements created when using `mask: "lines"`, `"words"` or `"chars"`.

### Details[​](#details "Direct link to Details")

An array containing all of the wrapper elements created by the `mask` feature. When you use `mask: "lines"`, `"words"`, or `"chars"`, SplitText wraps each corresponding part in an extra `<div>` with `overflow: clip`, allowing for simple masked reveal animations.
Access them in a "masks" Array on the SplitText instance. If you set a class name for the `lines/words/chars`, it'll append `"-mask"` for easy selecting.

#### loading...