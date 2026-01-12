---
url: https://tailwindcss.com/docs/box-decoration-break
title: box-decoration-break - Layout - Tailwind CSS
source_domain: tailwindcss.com
---

# box-decoration-break - Layout - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Layout
2. box-decoration-break

Layout

# box-decoration-break

Utilities for controlling how element fragments should be rendered across multiple lines, columns, or pages.

| Class | Styles |
| --- | --- |
| `box-decoration-clone` | `box-decoration-break: clone;` |
| `box-decoration-slice` | `box-decoration-break: slice;` |

## [Examples](https://tailwindcss.com/docs/box-decoration-break#examples)

### [Basic example](https://tailwindcss.com/docs/box-decoration-break#basic-example)

Use the `box-decoration-slice` and `box-decoration-clone` utilities to control whether properties like background, border, border-image, box-shadow, clip-path, margin, and padding should be rendered as if the element were one continuous fragment, or distinct blocks:

box-decoration-slice

Hello  
World

box-decoration-clone

Hello  
World

```
<span class="box-decoration-slice bg-linear-to-r from-indigo-600 to-pink-500 px-2 text-white ...">  Hello<br />World</span><span class="box-decoration-clone bg-linear-to-r from-indigo-600 to-pink-500 px-2 text-white ...">  Hello<br />World</span>
```

### [Responsive design](https://tailwindcss.com/docs/box-decoration-break#responsive-design)

Prefix a `box-decoration-break` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<div class="box-decoration-clone md:box-decoration-slice ...">  <!-- ... --></div>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/box-decoration-break#quick-reference)
* [Examples](https://tailwindcss.com/docs/box-decoration-break#examples)
  + [Basic example](https://tailwindcss.com/docs/box-decoration-break#basic-example)
  + [Responsive design](https://tailwindcss.com/docs/box-decoration-break#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)