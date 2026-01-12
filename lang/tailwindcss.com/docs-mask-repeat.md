---
url: https://tailwindcss.com/docs/mask-repeat
title: mask-repeat - Effects - Tailwind CSS
source_domain: tailwindcss.com
---

# mask-repeat - Effects - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Effects
2. mask-repeat

Effects

# mask-repeat

Utilities for controlling the repetition of an element's mask image.

| Class | Styles |
| --- | --- |
| `mask-repeat` | `mask-repeat: repeat;` |
| `mask-no-repeat` | `mask-repeat: no-repeat;` |
| `mask-repeat-x` | `mask-repeat: repeat-x;` |
| `mask-repeat-y` | `mask-repeat: repeat-y;` |
| `mask-repeat-space` | `mask-repeat: space;` |
| `mask-repeat-round` | `mask-repeat: round;` |

## [Examples](https://tailwindcss.com/docs/mask-repeat#examples)

### [Basic example](https://tailwindcss.com/docs/mask-repeat#basic-example)

Use the `mask-repeat` utility to repeat the mask image both vertically and horizontally:

```
<div class="mask-repeat mask-[url(/img/circle.png)] mask-size-[50px_50px] bg-[url(/img/mountains.jpg)] ..."></div>
```

### [Repeating horizontally](https://tailwindcss.com/docs/mask-repeat#repeating-horizontally)

Use the `mask-repeat-x` utility to only repeat the mask image horizontally:

```
<div class="mask-repeat-x mask-[url(/img/circle.png)] mask-size-[50px_50px] bg-[url(/img/mountains.jpg)]..."></div>
```

### [Repeating vertically](https://tailwindcss.com/docs/mask-repeat#repeating-vertically)

Use the `mask-repeat-y` utility to only repeat the mask image vertically:

```
<div class="mask-repeat-y mask-[url(/img/circle.png)] mask-size-[50px_50px] bg-[url(/img/mountains.jpg)]..."></div>
```

### [Preventing clipping](https://tailwindcss.com/docs/mask-repeat#preventing-clipping)

Use the `mask-repeat-space` utility to repeat the mask image without clipping:

```
<div class="mask-repeat-space mask-[url(/img/circle.png)] mask-size-[50px_50px] bg-[url(/img/mountains.jpg)] ..."></div>
```

### [Preventing clipping and gaps](https://tailwindcss.com/docs/mask-repeat#preventing-clipping-and-gaps)

Use the `mask-repeat-round` utility to repeat the mask image without clipping, stretching if needed to avoid gaps:

```
<div class="mask-repeat-round mask-[url(/img/circle.png)] mask-size-[50px_50px] bg-[url(/img/mountains.jpg)] ..."></div>
```

### [Disabling repeating](https://tailwindcss.com/docs/mask-repeat#disabling-repeating)

Use the `mask-no-repeat` utility to prevent a mask image from repeating:

```
<div class="mask-no-repeat mask-[url(/img/circle.png)] mask-size-[50px_50px] bg-[url(/img/mountains.jpg)] ..."></div>
```

### [Responsive design](https://tailwindcss.com/docs/mask-repeat#responsive-design)

Prefix a `mask-repeat` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<div class="mask-repeat md:mask-repeat-x ...">  <!-- ... --></div>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/mask-repeat#quick-reference)
* [Examples](https://tailwindcss.com/docs/mask-repeat#examples)
  + [Basic example](https://tailwindcss.com/docs/mask-repeat#basic-example)
  + [Repeating horizontally](https://tailwindcss.com/docs/mask-repeat#repeating-horizontally)
  + [Repeating vertically](https://tailwindcss.com/docs/mask-repeat#repeating-vertically)
  + [Preventing clipping](https://tailwindcss.com/docs/mask-repeat#preventing-clipping)
  + [Preventing clipping and gaps](https://tailwindcss.com/docs/mask-repeat#preventing-clipping-and-gaps)
  + [Disabling repeating](https://tailwindcss.com/docs/mask-repeat#disabling-repeating)
  + [Responsive design](https://tailwindcss.com/docs/mask-repeat#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)