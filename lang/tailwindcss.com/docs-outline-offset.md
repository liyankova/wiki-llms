---
url: https://tailwindcss.com/docs/outline-offset
title: outline-offset - Borders - Tailwind CSS
source_domain: tailwindcss.com
---

# outline-offset - Borders - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Borders
2. outline-offset

Borders

# outline-offset

Utilities for controlling the offset of an element's outline.

| Class | Styles |
| --- | --- |
| `outline-offset-<number>` | `outline-offset: <number>px;` |
| `-outline-offset-<number>` | `outline-offset: calc(<number>px * -1);` |
| `outline-offset-(<custom-property>)` | `outline-offset: var(<custom-property>);` |
| `outline-offset-[<value>]` | `outline-offset: <value>;` |

## [Examples](https://tailwindcss.com/docs/outline-offset#examples)

### [Basic example](https://tailwindcss.com/docs/outline-offset#basic-example)

Use utilities like `outline-offset-2` and `outline-offset-4` to change the offset of an element's outline:

outline-offset-0

outline-offset-2

outline-offset-4

```
<button class="outline-2 outline-offset-0 ...">Button A</button><button class="outline-2 outline-offset-2 ...">Button B</button><button class="outline-2 outline-offset-4 ...">Button C</button>
```

### [Using a custom value](https://tailwindcss.com/docs/outline-offset#using-a-custom-value)

Use the `outline-offset-[<value>]` syntax to set the outline offset based on a completely custom value:

```
<div class="outline-offset-[2vw] ...">  <!-- ... --></div>
```

For CSS variables, you can also use the `outline-offset-(<custom-property>)` syntax:

```
<div class="outline-offset-(--my-outline-offset) ...">  <!-- ... --></div>
```

This is just a shorthand for `outline-offset-[var(<custom-property>)]` that adds the `var()` function for you automatically.

### [Responsive design](https://tailwindcss.com/docs/outline-offset#responsive-design)

Prefix an `outline-offset` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<div class="outline md:outline-offset-2 ...">  <!-- ... --></div>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/outline-offset#quick-reference)
* [Examples](https://tailwindcss.com/docs/outline-offset#examples)
  + [Basic example](https://tailwindcss.com/docs/outline-offset#basic-example)
  + [Using a custom value](https://tailwindcss.com/docs/outline-offset#using-a-custom-value)
  + [Responsive design](https://tailwindcss.com/docs/outline-offset#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)