---
url: https://tailwindcss.com/docs/outline-width
title: outline-width - Borders - Tailwind CSS
source_domain: tailwindcss.com
---

# outline-width - Borders - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Borders
2. outline-width

Borders

# outline-width

Utilities for controlling the width of an element's outline.

| Class | Styles |
| --- | --- |
| `outline` | `outline-width: 1px;` |
| `outline-<number>` | `outline-width: <number>px;` |
| `outline-(length:<custom-property>)` | `outline-width: var(<custom-property>);` |
| `outline-[<value>]` | `outline-width: <value>;` |

## [Examples](https://tailwindcss.com/docs/outline-width#examples)

### [Basic example](https://tailwindcss.com/docs/outline-width#basic-example)

Use `outline` or `outline-<number>` utilities like `outline-2` and `outline-4` to set the width of an element's outline:

outline

outline-2

outline-4

```
<button class="outline outline-offset-2 ...">Button A</button><button class="outline-2 outline-offset-2 ...">Button B</button><button class="outline-4 outline-offset-2 ...">Button C</button>
```

### [Applying on focus](https://tailwindcss.com/docs/outline-width#applying-on-focus)

Prefix an `outline-width` utility with a variant like `focus:*` to only apply the utility in that state:

Focus the button to see the outline added

```
<button class="outline-offset-2 outline-sky-500 focus:outline-2 ...">Save Changes</button>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### [Using a custom value](https://tailwindcss.com/docs/outline-width#using-a-custom-value)

Use the `outline-[<value>]` syntax to set the outline width based on a completely custom value:

```
<div class="outline-[2vw] ...">  <!-- ... --></div>
```

For CSS variables, you can also use the `outline-(length:<custom-property>)` syntax:

```
<div class="outline-(length:--my-outline-width) ...">  <!-- ... --></div>
```

This is just a shorthand for `outline-[length:var(<custom-property>)]` that adds the `var()` function for you automatically.

### [Responsive design](https://tailwindcss.com/docs/outline-width#responsive-design)

Prefix an `outline-width` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<div class="outline md:outline-2 ...">  <!-- ... --></div>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/outline-width#quick-reference)
* [Examples](https://tailwindcss.com/docs/outline-width#examples)
  + [Basic example](https://tailwindcss.com/docs/outline-width#basic-example)
  + [Applying on focus](https://tailwindcss.com/docs/outline-width#applying-on-focus)
  + [Using a custom value](https://tailwindcss.com/docs/outline-width#using-a-custom-value)
  + [Responsive design](https://tailwindcss.com/docs/outline-width#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)