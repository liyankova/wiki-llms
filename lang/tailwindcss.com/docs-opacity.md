---
url: https://tailwindcss.com/docs/opacity
title: opacity - Effects - Tailwind CSS
source_domain: tailwindcss.com
---

# opacity - Effects - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Effects
2. opacity

Effects

# opacity

Utilities for controlling the opacity of an element.

| Class | Styles |
| --- | --- |
| `opacity-<number>` | `opacity: <number>%;` |
| `opacity-(<custom-property>)` | `opacity: var(<custom-property>);` |
| `opacity-[<value>]` | `opacity: <value>;` |

## [Examples](https://tailwindcss.com/docs/opacity#examples)

### [Basic example](https://tailwindcss.com/docs/opacity#basic-example)

Use `opacity-<number>` utilities like `opacity-25` and `opacity-100` to set the opacity of an element:

opacity-100

opacity-75

opacity-50

opacity-25

```
<button class="bg-indigo-500 opacity-100 ..."></button><button class="bg-indigo-500 opacity-75 ..."></button><button class="bg-indigo-500 opacity-50 ..."></button><button class="bg-indigo-500 opacity-25 ..."></button>
```

### [Applying conditionally](https://tailwindcss.com/docs/opacity#applying-conditionally)

Prefix an `opacity` utility with a variant like `disabled:*` to only apply the utility in that state:

```
<input class="opacity-100 disabled:opacity-75 ..." type="text" />
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### [Using a custom value](https://tailwindcss.com/docs/opacity#using-a-custom-value)

Use the `opacity-[<value>]` syntax to set the opacity based on a completely custom value:

```
<button class="opacity-[.67] ...">  <!-- ... --></button>
```

For CSS variables, you can also use the `opacity-(<custom-property>)` syntax:

```
<button class="opacity-(--my-opacity) ...">  <!-- ... --></button>
```

This is just a shorthand for `opacity-[var(<custom-property>)]` that adds the `var()` function for you automatically.

### [Responsive design](https://tailwindcss.com/docs/opacity#responsive-design)

Prefix an `opacity` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<button class="opacity-50 md:opacity-100 ...">  <!-- ... --></button>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/opacity#quick-reference)
* [Examples](https://tailwindcss.com/docs/opacity#examples)
  + [Basic example](https://tailwindcss.com/docs/opacity#basic-example)
  + [Applying conditionally](https://tailwindcss.com/docs/opacity#applying-conditionally)
  + [Using a custom value](https://tailwindcss.com/docs/opacity#using-a-custom-value)
  + [Responsive design](https://tailwindcss.com/docs/opacity#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)