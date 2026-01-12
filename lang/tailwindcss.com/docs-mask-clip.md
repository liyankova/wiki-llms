---
url: https://tailwindcss.com/docs/mask-clip
title: mask-clip - Effects - Tailwind CSS
source_domain: tailwindcss.com
---

# mask-clip - Effects - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Effects
2. mask-clip

Effects

# mask-clip

Utilities for controlling the bounding box of an element's mask.

| Class | Styles |
| --- | --- |
| `mask-clip-border` | `mask-clip: border-box;` |
| `mask-clip-padding` | `mask-clip: padding-box;` |
| `mask-clip-content` | `mask-clip: content-box;` |
| `mask-clip-fill` | `mask-clip: fill-box;` |
| `mask-clip-stroke` | `mask-clip: stroke-box;` |
| `mask-clip-view` | `mask-clip: view-box;` |
| `mask-no-clip` | `mask-clip: no-clip;` |

## [Examples](https://tailwindcss.com/docs/mask-clip#examples)

### [Basic example](https://tailwindcss.com/docs/mask-clip#basic-example)

Use utilities like `mask-clip-border`, `mask-clip-padding`, and `mask-clip-content` to control the bounding box of an element's mask:

mask-clip-border

mask-clip-padding

mask-clip-content

```
<div class="mask-clip-border border-3 p-1.5 mask-[url(/img/circle.png)] bg-[url(/img/mountains.jpg)] ..."></div><div class="mask-clip-padding border-3 p-1.5 mask-[url(/img/circle.png)] bg-[url(/img/mountains.jpg)] ..."></div><div class="mask-clip-content border-3 p-1.5 mask-[url(/img/circle.png)] bg-[url(/img/mountains.jpg)] ..."></div>
```

### [Responsive design](https://tailwindcss.com/docs/mask-clip#responsive-design)

Prefix a `mask-clip` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<div class="mask-clip-border md:mask-clip-padding ...">  <!-- ... --></div>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/mask-clip#quick-reference)
* [Examples](https://tailwindcss.com/docs/mask-clip#examples)
  + [Basic example](https://tailwindcss.com/docs/mask-clip#basic-example)
  + [Responsive design](https://tailwindcss.com/docs/mask-clip#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)