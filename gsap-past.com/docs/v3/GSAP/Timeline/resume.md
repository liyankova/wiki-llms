---
source_url: "https://gsap.com/docs/v3/GSAP/Timeline/resume()"
title: "resume | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:12:04.963332Z"
selector: "article"
---

# resume | GSAP | Docs & Learning

* [Timeline](/docs/v3/GSAP/Timeline)
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

**Note:** if the Timeline's timeScale is exactly 0 when resume() is called, it will be changed to 1 (otherwise it wouldn't play). If you're going to tween it up from 0 you can set it to a very small number before calling resume() like `tl.timeScale(tl.timeScale() || 0.001).resume()` so that it doesn't jump to 1.