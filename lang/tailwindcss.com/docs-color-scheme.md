---
url: https://tailwindcss.com/docs/color-scheme
title: color-scheme - Interactivity - Tailwind CSS
source_domain: tailwindcss.com
---

# color-scheme - Interactivity - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Interactivity
2. color-scheme

Interactivity

# color-scheme

Utilities for controlling the color scheme of an element.

| Class | Styles |
| --- | --- |
| `scheme-normal` | `color-scheme: normal;` |
| `scheme-dark` | `color-scheme: dark;` |
| `scheme-light` | `color-scheme: light;` |
| `scheme-light-dark` | `color-scheme: light dark;` |
| `scheme-only-dark` | `color-scheme: only dark;` |
| `scheme-only-light` | `color-scheme: only light;` |

## [Examples](https://tailwindcss.com/docs/color-scheme#examples)

### [Basic example](https://tailwindcss.com/docs/color-scheme#basic-example)

Use utilities like `scheme-light` and `scheme-light-dark` to control how element should be rendered:

Try switching your system color scheme to see the difference

scheme-light

scheme-dark

scheme-light-dark

```
<div class="scheme-light ...">  <input type="date" /></div><div class="scheme-dark ...">  <input type="date" /></div><div class="scheme-light-dark ...">  <input type="date" /></div>
```

### [Applying in dark mode](https://tailwindcss.com/docs/color-scheme#applying-in-dark-mode)

Prefix a `color-scheme` utility with a variant like `dark:*` to only apply the utility in that state:

```
<html class="scheme-light dark:scheme-dark ...">  <!-- ... --></html>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/color-scheme#quick-reference)
* [Examples](https://tailwindcss.com/docs/color-scheme#examples)
  + [Basic example](https://tailwindcss.com/docs/color-scheme#basic-example)
  + [Applying in dark mode](https://tailwindcss.com/docs/color-scheme#applying-in-dark-mode)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)