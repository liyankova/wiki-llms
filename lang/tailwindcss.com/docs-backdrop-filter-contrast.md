---
url: https://tailwindcss.com/docs/backdrop-filter-contrast
title: backdrop-filter: contrast() - Filters - Tailwind CSS
source_domain: tailwindcss.com
---

# backdrop-filter: contrast() - Filters - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Filters
2. contrast

Filters

# backdrop-filter: contrast()

Utilities for applying backdrop contrast filters to an element.

| Class | Styles |
| --- | --- |
| `backdrop-contrast-<number>` | `backdrop-filter: contrast(<number>%);` |
| `backdrop-contrast-(<custom-property>)` | `backdrop-filter: contrast(var(<custom-property>));` |
| `backdrop-contrast-[<value>]` | `backdrop-filter: contrast(<value>);` |

## [Examples](https://tailwindcss.com/docs/backdrop-filter-contrast#examples)

### [Basic example](https://tailwindcss.com/docs/backdrop-filter-contrast#basic-example)

Use utilities like `backdrop-contrast-50` and `backdrop-contrast-100` to control an element's backdrop contrast:

backdrop-contrast-50

![](https://images.unsplash.com/photo-1554629947-334ff61d85dc?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1000&h=1000&q=90)

backdrop-contrast-200

![](https://images.unsplash.com/photo-1554629947-334ff61d85dc?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1000&h=1000&q=90)

```
<div class="bg-[url(/img/mountains.jpg)]">  <div class="bg-white/30 backdrop-contrast-50 ..."></div></div><div class="bg-[url(/img/mountains.jpg)]">  <div class="bg-white/30 backdrop-contrast-200 ..."></div></div>
```

### [Using a custom value](https://tailwindcss.com/docs/backdrop-filter-contrast#using-a-custom-value)

Use the `backdrop-contrast-[<value>]` syntax to set the backdrop contrast based on a completely custom value:

```
<div class="backdrop-contrast-[.25] ...">  <!-- ... --></div>
```

For CSS variables, you can also use the `backdrop-contrast-(<custom-property>)` syntax:

```
<div class="backdrop-contrast-(--my-backdrop-contrast) ...">  <!-- ... --></div>
```

This is just a shorthand for `backdrop-contrast-[var(<custom-property>)]` that adds the `var()` function for you automatically.

### [Responsive design](https://tailwindcss.com/docs/backdrop-filter-contrast#responsive-design)

Prefix a `backdrop-filter: contrast()` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<div class="backdrop-contrast-125 md:backdrop-contrast-150 ...">  <!-- ... --></div>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/backdrop-filter-contrast#quick-reference)
* [Examples](https://tailwindcss.com/docs/backdrop-filter-contrast#examples)
  + [Basic example](https://tailwindcss.com/docs/backdrop-filter-contrast#basic-example)
  + [Using a custom value](https://tailwindcss.com/docs/backdrop-filter-contrast#using-a-custom-value)
  + [Responsive design](https://tailwindcss.com/docs/backdrop-filter-contrast#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)