---
url: https://tailwindcss.com/docs/transform
title: transform - Transforms - Tailwind CSS
source_domain: tailwindcss.com
---

# transform - Transforms - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Transforms
2. transform

Transforms

# transform

Utilities for transforming elements.

| Class | Styles |
| --- | --- |
| `transform-(<custom-property>)` | `transform: var(<custom-property>);` |
| `transform-[<value>]` | `transform: <value>;` |
| `transform-none` | `transform: none;` |
| `transform-gpu` | `transform: translateZ(0) var(--tw-rotate-x) var(--tw-rotate-y) var(--tw-rotate-z) var(--tw-skew-x) var(--tw-skew-y);` |
| `transform-cpu` | `transform: var(--tw-rotate-x) var(--tw-rotate-y) var(--tw-rotate-z) var(--tw-skew-x) var(--tw-skew-y);` |

## [Examples](https://tailwindcss.com/docs/transform#examples)

### [Hardware acceleration](https://tailwindcss.com/docs/transform#hardware-acceleration)

If your transition performs better when rendered by the GPU instead of the CPU, you can force hardware acceleration by adding the `transform-gpu` utility:

```
<div class="scale-150 transform-gpu">  <!-- ... --></div>
```

Use the `transform-cpu` utility to force things back to the CPU if you need to undo this conditionally.

### [Removing transforms](https://tailwindcss.com/docs/transform#removing-transforms)

Use the `transform-none` utility to remove all of the transforms on an element at once:

```
<div class="skew-y-3 md:transform-none">  <!-- ... --></div>
```

### [Using a custom value](https://tailwindcss.com/docs/transform#using-a-custom-value)

Use the `transform-[<value>]` syntax to set the transform based on a completely custom value:

```
<div class="transform-[matrix(1,2,3,4,5,6)] ...">  <!-- ... --></div>
```

For CSS variables, you can also use the `transform-(<custom-property>)` syntax:

```
<div class="transform-(--my-transform) ...">  <!-- ... --></div>
```

This is just a shorthand for `transform-[var(<custom-property>)]` that adds the `var()` function for you automatically.

### On this page

* [Quick reference](https://tailwindcss.com/docs/transform#quick-reference)
* [Examples](https://tailwindcss.com/docs/transform#examples)
  + [Hardware acceleration](https://tailwindcss.com/docs/transform#hardware-acceleration)
  + [Removing transforms](https://tailwindcss.com/docs/transform#removing-transforms)
  + [Using a custom value](https://tailwindcss.com/docs/transform#using-a-custom-value)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)