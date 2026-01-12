---
url: https://tailwindcss.com/docs/background-repeat
title: background-repeat - Backgrounds - Tailwind CSS
source_domain: tailwindcss.com
---

# background-repeat - Backgrounds - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Backgrounds
2. background-repeat

Backgrounds

# background-repeat

Utilities for controlling the repetition of an element's background image.

| Class | Styles |
| --- | --- |
| `bg-repeat` | `background-repeat: repeat;` |
| `bg-repeat-x` | `background-repeat: repeat-x;` |
| `bg-repeat-y` | `background-repeat: repeat-y;` |
| `bg-repeat-space` | `background-repeat: space;` |
| `bg-repeat-round` | `background-repeat: round;` |
| `bg-no-repeat` | `background-repeat: no-repeat;` |

## [Examples](https://tailwindcss.com/docs/background-repeat#examples)

### [Basic example](https://tailwindcss.com/docs/background-repeat#basic-example)

Use the `bg-repeat` utility to repeat the background image both vertically and horizontally:

```
<div class="bg-[url(/img/clouds.svg)] bg-center bg-repeat ..."></div>
```

### [Repeating horizontally](https://tailwindcss.com/docs/background-repeat#repeating-horizontally)

Use the `bg-repeat-x` utility to only repeat the background image horizontally:

```
<div class="bg-[url(/img/clouds.svg)] bg-center bg-repeat-x ..."></div>
```

### [Repeating vertically](https://tailwindcss.com/docs/background-repeat#repeating-vertically)

Use the `bg-repeat-y` utility to only repeat the background image vertically:

```
<div class="bg-[url(/img/clouds.svg)] bg-center bg-repeat-y ..."></div>
```

### [Preventing clipping](https://tailwindcss.com/docs/background-repeat#preventing-clipping)

Use the `bg-repeat-space` utility to repeat the background image without clipping:

```
<div class="bg-[url(/img/clouds.svg)] bg-center bg-repeat-space ..."></div>
```

### [Preventing clipping and gaps](https://tailwindcss.com/docs/background-repeat#preventing-clipping-and-gaps)

Use the `bg-repeat-round` utility to repeat the background image without clipping, stretching if needed to avoid gaps:

```
<div class="bg-[url(/img/clouds.svg)] bg-center bg-repeat-round ..."></div>
```

### [Disabling repeating](https://tailwindcss.com/docs/background-repeat#disabling-repeating)

Use the `bg-no-repeat` utility to prevent a background image from repeating:

```
<div class="bg-[url(/img/clouds.svg)] bg-center bg-no-repeat ..."></div>
```

### [Responsive design](https://tailwindcss.com/docs/background-repeat#responsive-design)

Prefix a `background-repeat` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<div class="bg-repeat md:bg-repeat-x ...">  <!-- ... --></div>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/background-repeat#quick-reference)
* [Examples](https://tailwindcss.com/docs/background-repeat#examples)
  + [Basic example](https://tailwindcss.com/docs/background-repeat#basic-example)
  + [Repeating horizontally](https://tailwindcss.com/docs/background-repeat#repeating-horizontally)
  + [Repeating vertically](https://tailwindcss.com/docs/background-repeat#repeating-vertically)
  + [Preventing clipping](https://tailwindcss.com/docs/background-repeat#preventing-clipping)
  + [Preventing clipping and gaps](https://tailwindcss.com/docs/background-repeat#preventing-clipping-and-gaps)
  + [Disabling repeating](https://tailwindcss.com/docs/background-repeat#disabling-repeating)
  + [Responsive design](https://tailwindcss.com/docs/background-repeat#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)