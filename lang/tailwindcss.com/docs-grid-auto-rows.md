---
url: https://tailwindcss.com/docs/grid-auto-rows
title: grid-auto-rows - Flexbox & Grid - Tailwind CSS
source_domain: tailwindcss.com
---

# grid-auto-rows - Flexbox & Grid - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Flexbox & Grid
2. grid-auto-rows

Flexbox & Grid

# grid-auto-rows

Utilities for controlling the size of implicitly-created grid rows.

| Class | Styles |
| --- | --- |
| `auto-rows-auto` | `grid-auto-rows: auto;` |
| `auto-rows-min` | `grid-auto-rows: min-content;` |
| `auto-rows-max` | `grid-auto-rows: max-content;` |
| `auto-rows-fr` | `grid-auto-rows: minmax(0, 1fr);` |
| `auto-rows-(<custom-property>)` | `grid-auto-rows: var(<custom-property>);` |
| `auto-rows-[<value>]` | `grid-auto-rows: <value>;` |

## [Examples](https://tailwindcss.com/docs/grid-auto-rows#examples)

### [Basic example](https://tailwindcss.com/docs/grid-auto-rows#basic-example)

Use utilities like `auto-rows-min` and `auto-rows-max` to control the size of implicitly-created grid rows:

```
<div class="grid grid-flow-row auto-rows-max">  <div>01</div>  <div>02</div>  <div>03</div></div>
```

### [Using a custom value](https://tailwindcss.com/docs/grid-auto-rows#using-a-custom-value)

Use the `auto-rows-[<value>]` syntax to set the size of implicitly-created grid rows based on a completely custom value:

```
<div class="auto-rows-[minmax(0,2fr)] ...">  <!-- ... --></div>
```

For CSS variables, you can also use the `auto-rows-(<custom-property>)` syntax:

```
<div class="auto-rows-(--my-auto-rows) ...">  <!-- ... --></div>
```

This is just a shorthand for `auto-rows-[var(<custom-property>)]` that adds the `var()` function for you automatically.

### [Responsive design](https://tailwindcss.com/docs/grid-auto-rows#responsive-design)

Prefix a `grid-auto-rows` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<div class="grid grid-flow-row auto-rows-max md:auto-rows-min ...">  <!-- ... --></div>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/grid-auto-rows#quick-reference)
* [Examples](https://tailwindcss.com/docs/grid-auto-rows#examples)
  + [Basic example](https://tailwindcss.com/docs/grid-auto-rows#basic-example)
  + [Using a custom value](https://tailwindcss.com/docs/grid-auto-rows#using-a-custom-value)
  + [Responsive design](https://tailwindcss.com/docs/grid-auto-rows#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)