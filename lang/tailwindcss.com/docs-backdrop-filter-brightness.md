---
url: https://tailwindcss.com/docs/backdrop-filter-brightness
title: backdrop-filter: brightness() - Filters - Tailwind CSS
source_domain: tailwindcss.com
---

# backdrop-filter: brightness() - Filters - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Filters
2. brightness

Filters

# backdrop-filter: brightness()

Utilities for applying backdrop brightness filters to an element.

| Class | Styles |
| --- | --- |
| `backdrop-brightness-<number>` | `backdrop-filter: brightness(<number>%);` |
| `backdrop-brightness-(<custom-property>)` | `backdrop-filter: brightness(var(<custom-property>));` |
| `backdrop-brightness-[<value>]` | `backdrop-filter: brightness(<value>);` |

## [Examples](https://tailwindcss.com/docs/backdrop-filter-brightness#examples)

### [Basic example](https://tailwindcss.com/docs/backdrop-filter-brightness#basic-example)

Use utilities like `backdrop-brightness-50` and `backdrop-brightness-100` to control an element's backdrop brightness:

backdrop-brightness-50

![](https://images.unsplash.com/photo-1554629947-334ff61d85dc?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1000&h=1000&q=90)

backdrop-brightness-150

![](https://images.unsplash.com/photo-1554629947-334ff61d85dc?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1000&h=1000&q=90)

```
<div class="bg-[url(/img/mountains.jpg)]">  <div class="bg-white/30 backdrop-brightness-50 ..."></div></div><div class="bg-[url(/img/mountains.jpg)]">  <div class="bg-white/30 backdrop-brightness-150 ..."></div></div>
```

### [Using a custom value](https://tailwindcss.com/docs/backdrop-filter-brightness#using-a-custom-value)

Use the `backdrop-brightness-[<value>]` syntax to set the backdrop brightness based on a completely custom value:

```
<div class="backdrop-brightness-[1.75] ...">  <!-- ... --></div>
```

For CSS variables, you can also use the `backdrop-brightness-(<custom-property>)` syntax:

```
<div class="backdrop-brightness-(--my-backdrop-brightness) ...">  <!-- ... --></div>
```

This is just a shorthand for `backdrop-brightness-[var(<custom-property>)]` that adds the `var()` function for you automatically.

### [Responsive design](https://tailwindcss.com/docs/backdrop-filter-brightness#responsive-design)

Prefix a `backdrop-filter: brightness()` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<div class="backdrop-brightness-110 md:backdrop-brightness-150 ...">  <!-- ... --></div>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/backdrop-filter-brightness#quick-reference)
* [Examples](https://tailwindcss.com/docs/backdrop-filter-brightness#examples)
  + [Basic example](https://tailwindcss.com/docs/backdrop-filter-brightness#basic-example)
  + [Using a custom value](https://tailwindcss.com/docs/backdrop-filter-brightness#using-a-custom-value)
  + [Responsive design](https://tailwindcss.com/docs/backdrop-filter-brightness#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)