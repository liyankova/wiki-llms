---
url: https://tailwindcss.com/docs/font-smoothing
title: font-smoothing - Typography - Tailwind CSS
source_domain: tailwindcss.com
---

# font-smoothing - Typography - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Typography
2. font-smoothing

Typography

# font-smoothing

Utilities for controlling the font smoothing of an element.

| Class | Styles |
| --- | --- |
| `antialiased` | `-webkit-font-smoothing: antialiased; -moz-osx-font-smoothing: grayscale;` |
| `subpixel-antialiased` | `-webkit-font-smoothing: auto; -moz-osx-font-smoothing: auto;` |

## [Examples](https://tailwindcss.com/docs/font-smoothing#examples)

### [Grayscale antialiasing](https://tailwindcss.com/docs/font-smoothing#grayscale-antialiasing)

Use the `antialiased` utility to render text using grayscale antialiasing:

The quick brown fox jumps over the lazy dog.

```
<p class="antialiased ...">The quick brown fox ...</p>
```

### [Subpixel antialiasing](https://tailwindcss.com/docs/font-smoothing#subpixel-antialiasing)

Use the `subpixel-antialiased` utility to render text using subpixel antialiasing:

The quick brown fox jumps over the lazy dog.

```
<p class="subpixel-antialiased ...">The quick brown fox ...</p>
```

### [Responsive design](https://tailwindcss.com/docs/font-smoothing#responsive-design)

Prefix `-webkit-font-smoothing` and `-moz-osx-font-smoothing` utilities with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<p class="antialiased md:subpixel-antialiased ...">  Lorem ipsum dolor sit amet...</p>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/font-smoothing#quick-reference)
* [Examples](https://tailwindcss.com/docs/font-smoothing#examples)
  + [Grayscale antialiasing](https://tailwindcss.com/docs/font-smoothing#grayscale-antialiasing)
  + [Subpixel antialiasing](https://tailwindcss.com/docs/font-smoothing#subpixel-antialiasing)
  + [Responsive design](https://tailwindcss.com/docs/font-smoothing#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)