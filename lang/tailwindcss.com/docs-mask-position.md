---
url: https://tailwindcss.com/docs/mask-position
title: mask-position - Effects - Tailwind CSS
source_domain: tailwindcss.com
---

# mask-position - Effects - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Effects
2. mask-position

Effects

# mask-position

Utilities for controlling the position of an element's mask image.

| Class | Styles |
| --- | --- |
| `mask-top-left` | `mask-position: top left;` |
| `mask-top` | `mask-position: top;` |
| `mask-top-right` | `mask-position: top right;` |
| `mask-left` | `mask-position: left;` |
| `mask-center` | `mask-position: center;` |
| `mask-right` | `mask-position: right;` |
| `mask-bottom-left` | `mask-position: bottom left;` |
| `mask-bottom` | `mask-position: bottom;` |
| `mask-bottom-right` | `mask-position: bottom right;` |
| `mask-position-(<custom-property>)` | `mask-position: var(<custom-property>);` |
| `mask-position-[<value>]` | `mask-position: <value>;` |

## [Examples](https://tailwindcss.com/docs/mask-position#examples)

### [Basic example](https://tailwindcss.com/docs/mask-position#basic-example)

Use utilities like `mask-center`, `mask-right`, and `mask-left-top` to control the position of an element's mask image:

mask-top-left

mask-top

mask-top-right

mask-left

mask-center

mask-right

mask-bottom-left

mask-bottom

mask-bottom-right

```
<div class="mask-top-left mask-[url(/img/circle.png)] mask-size-[50%] bg-[url(/img/mountains.jpg)] ..."></div><div class="mask-top mask-[url(/img/circle.png)] mask-size-[50%] bg-[url(/img/mountains.jpg)] ..."></div><div class="mask-top-right mask-[url(/img/circle.png)] mask-size-[50%] bg-[url(/img/mountains.jpg)] ..."></div><div class="mask-left mask-[url(/img/circle.png)] mask-size-[50%] bg-[url(/img/mountains.jpg)] ..."></div><div class="mask-center mask-[url(/img/circle.png)] mask-size-[50%] bg-[url(/img/mountains.jpg)] ..."></div><div class="mask-right mask-[url(/img/circle.png)] mask-size-[50%] bg-[url(/img/mountains.jpg)] ..."></div><div class="mask-bottom-left mask-[url(/img/circle.png)] mask-size-[50%] bg-[url(/img/mountains.jpg)] ..."></div><div class="mask-bottom mask-[url(/img/circle.png)] mask-size-[50%] bg-[url(/img/mountains.jpg)] ..."></div><div class="mask-bottom-right mask-[url(/img/circle.png)] mask-size-[50%] bg-[url(/img/mountains.jpg)] ..."></div>
```

### [Using a custom value](https://tailwindcss.com/docs/mask-position#using-a-custom-value)

Use the `mask-position-[<value>]` syntax to set the mask position based on a completely custom value:

```
<div class="mask-position-[center_top_1rem] ...">  <!-- ... --></div>
```

For CSS variables, you can also use the `mask-position-(<custom-property>)` syntax:

```
<div class="mask-position-(--my-mask-position) ...">  <!-- ... --></div>
```

This is just a shorthand for `mask-position-[var(<custom-property>)]` that adds the `var()` function for you automatically.

### [Responsive design](https://tailwindcss.com/docs/mask-position#responsive-design)

Prefix a `mask-position` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<div class="mask-center md:mask-top ...">  <!-- ... --></div>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/mask-position#quick-reference)
* [Examples](https://tailwindcss.com/docs/mask-position#examples)
  + [Basic example](https://tailwindcss.com/docs/mask-position#basic-example)
  + [Using a custom value](https://tailwindcss.com/docs/mask-position#using-a-custom-value)
  + [Responsive design](https://tailwindcss.com/docs/mask-position#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)