---
source_url: "https://gsap.com/docs/v3/Plugins/Observer/disable()"
title: "disable | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:20:26.815388Z"
selector: "article"
---

# disable | GSAP | Docs & Learning

* more plugins
* [Observer](/docs/v3/Plugins/Observer/)
* methods
* .disable()

On this page

# disable

### disable( ) : void

Disables the Observer, removing the necessary event listeners and firing the `onDisable` callback if the Observer wasn't already disabled.

### Details[​](#details "Direct link to Details")

Disables the Observer, removing the necessary event listeners and firing the `onDisable` callback if the Observer wasn't already disabled. If you plan to disable it permanently, use `kill()` instead so that it also gets removed from the internal Array and can be made available for garbage collection.