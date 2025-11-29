---
source_url: "https://gsap.com/docs/v3/GSAP/Tween/resume()"
title: "resume | GSAP | Docs & Learning"
crawl_date: "2025-11-29T16:57:00.504127Z"
selector: "article"
---

# resume | GSAP | Docs & Learning

* [Tween](/docs/v3/GSAP/Tween)
* methods
* .resume()

On this page

# resume

### resume( ) : self

Resumes playing without altering direction (forward or reversed).

### Returns : self[​](#returns--self "Direct link to Returns : self")

For easier chaining

### Details[​](#details "Direct link to Details")

Resumes playing without altering direction (forward or reversed).

**Note:** if the Tween's timeScale is exactly 0 when resume() is called, it will be changed to 1 (otherwise it wouldn't play). If you're going to tween it up from 0 you can set it to a very small number before calling resume() like `myAnimation.timeScale(myAnimation.timeScale() || 0.001).resume()` so that it doesn't jump to 1.