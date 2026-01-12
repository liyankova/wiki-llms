---
url: https://tailwindcss.com/docs/z-index
title: z-index - Layout - Tailwind CSS
source_domain: tailwindcss.com
---

# z-index - Layout - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Layout
2. z-index

Layout

# z-index

Utilities for controlling the stack order of an element.

| Class | Styles |
| --- | --- |
| `z-<number>` | `z-index: <number>;` |
| `z-auto` | `z-index: auto;` |
| `z-[<value>]` | `z-index: <value>;` |
| `z-(<custom-property>)` | `z-index: var(<custom-property>);` |

## [Examples](https://tailwindcss.com/docs/z-index#examples)

### [Basic example](https://tailwindcss.com/docs/z-index#basic-example)

Use the `z-<number>` utilities like `z-10` and `z-50` to control the stack order (or three-dimensional positioning) of an element, regardless of the order it has been displayed:

05

04

03

02

01

```
<div class="z-40 ...">05</div><div class="z-30 ...">04</div><div class="z-20 ...">03</div><div class="z-10 ...">02</div><div class="z-0 ...">01</div>
```

### [Using negative values](https://tailwindcss.com/docs/z-index#using-negative-values)

To use a negative z-index value, prefix the class name with a dash to convert it to a negative value:

01

02

03

04

05

```
<div class="...">05</div><div class="...">04</div><div class="-z-10 ...">03</div><div class="...">02</div><div class="...">01</div>
```

### [Using a custom value](https://tailwindcss.com/docs/z-index#using-a-custom-value)

Use the `z-[<value>]` syntax to set the stack order based on a completely custom value:

```
<div class="z-[calc(var(--index)+1)] ...">  <!-- ... --></div>
```

For CSS variables, you can also use the `z-(<custom-property>)` syntax:

```
<div class="z-(--my-z) ...">  <!-- ... --></div>
```

This is just a shorthand for `z-[var(<custom-property>)]` that adds the `var()` function for you automatically.

### [Responsive design](https://tailwindcss.com/docs/z-index#responsive-design)

Prefix a `z-index` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<div class="z-0 md:z-50 ...">  <!-- ... --></div>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/z-index#quick-reference)
* [Examples](https://tailwindcss.com/docs/z-index#examples)
  + [Basic example](https://tailwindcss.com/docs/z-index#basic-example)
  + [Using negative values](https://tailwindcss.com/docs/z-index#using-negative-values)
  + [Using a custom value](https://tailwindcss.com/docs/z-index#using-a-custom-value)
  + [Responsive design](https://tailwindcss.com/docs/z-index#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)