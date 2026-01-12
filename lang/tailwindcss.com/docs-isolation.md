---
url: https://tailwindcss.com/docs/isolation
title: isolation - Layout - Tailwind CSS
source_domain: tailwindcss.com
---

# isolation - Layout - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Layout
2. isolation

Layout

# isolation

Utilities for controlling whether an element should explicitly create a new stacking context.

| Class | Styles |
| --- | --- |
| `isolate` | `isolation: isolate;` |
| `isolation-auto` | `isolation: auto;` |

## [Examples](https://tailwindcss.com/docs/isolation#examples)

### [Basic example](https://tailwindcss.com/docs/isolation#basic-example)

Use the `isolate` and `isolation-auto` utilities to control whether an element should explicitly create a new stacking context:

```
<div class="isolate ...">  <!-- ... --></div>
```

### [Responsive design](https://tailwindcss.com/docs/isolation#responsive-design)

Prefix an `isolation` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<div class="isolate md:isolation-auto ...">  <!-- ... --></div>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/isolation#quick-reference)
* [Examples](https://tailwindcss.com/docs/isolation#examples)
  + [Basic example](https://tailwindcss.com/docs/isolation#basic-example)
  + [Responsive design](https://tailwindcss.com/docs/isolation#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)