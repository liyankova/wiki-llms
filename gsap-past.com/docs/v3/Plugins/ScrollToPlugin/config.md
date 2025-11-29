---
source_url: "https://gsap.com/docs/v3/Plugins/ScrollToPlugin/config()"
title: "config | GSAP | Docs & Learning"
crawl_date: "2025-11-29T20:18:54.068652Z"
selector: "article"
---

# config | GSAP | Docs & Learning

* more plugins
* [ScrollTo](/docs/v3/Plugins/ScrollToPlugin)
* methods
* .config()

On this page

# ScrollToPlugin.config

### ScrollToPlugin.config( vars:Object )

Allows you to configure the global behavior of ScrollToPlugin like `autoKill`

#### Parameters

* #### **vars**: Object

  A configuration object with the properties you'd like to affect, like `{ autoKill: true }`

### Details[​](#details "Direct link to Details")

Allows you to configure the global behavior of ScrollToPlugin like:

* **autoKill** *[Boolean]* - if `true`, ScrollToPlugin will automatically sense if the scroll position was changed outside of itself (like if the user manually started dragging the scrollbar mid-tween) and cancel that portion of the tween.

### Example[​](#example "Direct link to Example")

```
ScrollToPlugin.config({ autoKill: true })
```

`ScrollToPlugin.config()` was added in version 3.12.6