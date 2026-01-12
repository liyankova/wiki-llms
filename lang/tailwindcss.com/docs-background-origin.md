---
url: https://tailwindcss.com/docs/background-origin
title: background-origin - Backgrounds - Tailwind CSS
source_domain: tailwindcss.com
---

# background-origin - Backgrounds - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Backgrounds
2. background-origin

Backgrounds

# background-origin

Utilities for controlling how an element's background is positioned relative to borders, padding, and content.

| Class | Styles |
| --- | --- |
| `bg-origin-border` | `background-origin: border-box;` |
| `bg-origin-padding` | `background-origin: padding-box;` |
| `bg-origin-content` | `background-origin: content-box;` |

## [Examples](https://tailwindcss.com/docs/background-origin#examples)

### [Basic example](https://tailwindcss.com/docs/background-origin#basic-example)

Use the `bg-origin-border`, `bg-origin-padding`, and `bg-origin-content` utilities to control where an element's background is rendered:

bg-origin-border

bg-origin-padding

bg-origin-content

```
<div class="border-4 bg-[url(/img/mountains.jpg)] bg-origin-border p-3 ..."></div><div class="border-4 bg-[url(/img/mountains.jpg)] bg-origin-padding p-3 ..."></div><div class="border-4 bg-[url(/img/mountains.jpg)] bg-origin-content p-3 ..."></div>
```

### [Responsive design](https://tailwindcss.com/docs/background-origin#responsive-design)

Prefix a `background-origin` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<div class="bg-origin-border md:bg-origin-padding ...">  <!-- ... --></div>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/background-origin#quick-reference)
* [Examples](https://tailwindcss.com/docs/background-origin#examples)
  + [Basic example](https://tailwindcss.com/docs/background-origin#basic-example)
  + [Responsive design](https://tailwindcss.com/docs/background-origin#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)