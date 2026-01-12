---
url: https://tailwindcss.com/docs/break-before
title: break-before - Layout - Tailwind CSS
source_domain: tailwindcss.com
---

# break-before - Layout - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Layout
2. break-before

Layout

# break-before

Utilities for controlling how a column or page should break before an element.

| Class | Styles |
| --- | --- |
| `break-before-auto` | `break-before: auto;` |
| `break-before-avoid` | `break-before: avoid;` |
| `break-before-all` | `break-before: all;` |
| `break-before-avoid-page` | `break-before: avoid-page;` |
| `break-before-page` | `break-before: page;` |
| `break-before-left` | `break-before: left;` |
| `break-before-right` | `break-before: right;` |
| `break-before-column` | `break-before: column;` |

## [Examples](https://tailwindcss.com/docs/break-before#examples)

### [Basic example](https://tailwindcss.com/docs/break-before#basic-example)

Use utilities like `break-before-column` and `break-before-page` to control how a column or page break should behave before an element:

```
<div class="columns-2">  <p>Well, let me tell you something, ...</p>  <p class="break-before-column">Sure, go ahead, laugh...</p>  <p>Maybe we can live without...</p>  <p>Look. If you think this is...</p></div>
```

### [Responsive design](https://tailwindcss.com/docs/break-before#responsive-design)

Prefix a `break-before` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<div class="break-before-column md:break-before-auto ...">  <!-- ... --></div>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/break-before#quick-reference)
* [Examples](https://tailwindcss.com/docs/break-before#examples)
  + [Basic example](https://tailwindcss.com/docs/break-before#basic-example)
  + [Responsive design](https://tailwindcss.com/docs/break-before#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)