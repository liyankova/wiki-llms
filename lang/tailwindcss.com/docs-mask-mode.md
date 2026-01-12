---
url: https://tailwindcss.com/docs/mask-mode
title: mask-mode - Effects - Tailwind CSS
source_domain: tailwindcss.com
---

# mask-mode - Effects - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Effects
2. mask-mode

Effects

# mask-mode

Utilities for controlling an element's mask mode.

| Class | Styles |
| --- | --- |
| `mask-alpha` | `mask-mode: alpha;` |
| `mask-luminance` | `mask-mode: luminance;` |
| `mask-match` | `mask-mode: match-source;` |

## [Examples](https://tailwindcss.com/docs/mask-mode#examples)

### [Basic example](https://tailwindcss.com/docs/mask-mode#basic-example)

Use the `mask-alpha`, `mask-luminance` and `mask-match` utilities to control the mode of an element's mask:

mask-alpha

mask-luminance

```
<div class="mask-alpha mask-r-from-black mask-r-from-50% mask-r-to-transparent bg-[url(/img/mountains.jpg)] ..."></div><div class="mask-luminance mask-r-from-white mask-r-from-50% mask-r-to-black bg-[url(/img/mountains.jpg)] ..."></div>
```

When using `mask-luminance` the luminance value of the mask determines visibility, so sticking with grayscale colors will produce the most predictable results. With `mask-alpha`, the opacity of the mask determines the visibility of the masked element.

### [Responsive design](https://tailwindcss.com/docs/mask-mode#responsive-design)

Prefix a `mask-mode` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<div class="mask-alpha md:mask-luminance ...">  <!-- ... --></div>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/mask-mode#quick-reference)
* [Examples](https://tailwindcss.com/docs/mask-mode#examples)
  + [Basic example](https://tailwindcss.com/docs/mask-mode#basic-example)
  + [Responsive design](https://tailwindcss.com/docs/mask-mode#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)