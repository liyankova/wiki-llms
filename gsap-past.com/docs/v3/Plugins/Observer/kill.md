---
source_url: "https://gsap.com/docs/v3/Plugins/Observer/kill()"
title: "kill | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:20:30.904685Z"
selector: "article"
---

# kill | GSAP | Docs & Learning

* more plugins
* [Observer](/docs/v3/Plugins/Observer/)
* methods
* .kill()

On this page

# kill

### kill( ) : void

Kills the Observer instance, calling `disable()` and removing it from the internal Array so that it can no longer be found via .getAll() or .getById(), making it available for garbage collection. This is permanent. If you plan on enabling the instance again later, just use `disable()` instead of `kill()`.

### Details[​](#details "Direct link to Details")

Kills the Observer instance, calling `disable()` and removing it from the internal Array so that it can no longer be found via .getAll() or .getById(), making it available for garbage collection. This is permanent. If you plan on enabling the instance again later, just use `disable()` instead of `kill()`.