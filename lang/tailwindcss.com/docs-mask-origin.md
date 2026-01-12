---
url: https://tailwindcss.com/docs/mask-origin
title: mask-origin - Effects - Tailwind CSS
source_domain: tailwindcss.com
---

# mask-origin - Effects - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Effects
2. mask-origin

Effects

# mask-origin

Utilities for controlling how an element's mask image is positioned relative to borders, padding, and content.

| Class | Styles |
| --- | --- |
| `mask-origin-border` | `mask-origin: border-box;` |
| `mask-origin-padding` | `mask-origin: padding-box;` |
| `mask-origin-content` | `mask-origin: content-box;` |
| `mask-origin-fill` | `mask-origin: fill-box;` |
| `mask-origin-stroke` | `mask-origin: stroke-box;` |
| `mask-origin-view` | `mask-origin: view-box;` |

## [Examples](https://tailwindcss.com/docs/mask-origin#examples)

### [Basic example](https://tailwindcss.com/docs/mask-origin#basic-example)

Use utilities like `mask-origin-border`, `mask-origin-padding`, and `mask-origin-content` to control where an element's mask is rendered:

mask-origin-border

mask-origin-padding

mask-origin-content

```
<div class="mask-origin-border border-3 p-1.5 mask-[url(/img/circle.png)] bg-[url(/img/mountains.jpg)] ..."></div><div class="mask-origin-padding border-3 p-1.5 mask-[url(/img/circle.png)] bg-[url(/img/mountains.jpg)] ..."></div><div class="mask-origin-content border-3 p-1.5 mask-[url(/img/circle.png)] bg-[url(/img/mountains.jpg)] ..."></div>
```

### [Responsive design](https://tailwindcss.com/docs/mask-origin#responsive-design)

Prefix a `mask-origin` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<div class="mask-origin-border md:mask-origin-padding ...">  <!-- ... --></div>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/mask-origin#quick-reference)
* [Examples](https://tailwindcss.com/docs/mask-origin#examples)
  + [Basic example](https://tailwindcss.com/docs/mask-origin#basic-example)
  + [Responsive design](https://tailwindcss.com/docs/mask-origin#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)