---
url: https://tailwindcss.com/docs/text-decoration-thickness
title: text-decoration-thickness - Typography - Tailwind CSS
source_domain: tailwindcss.com
---

# text-decoration-thickness - Typography - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Typography
2. text-decoration-thickness

Typography

# text-decoration-thickness

Utilities for controlling the thickness of text decorations.

| Class | Styles |
| --- | --- |
| `decoration-<number>` | `text-decoration-thickness: <number>px;` |
| `decoration-from-font` | `text-decoration-thickness: from-font;` |
| `decoration-auto` | `text-decoration-thickness: auto;` |
| `decoration-(length:<custom-property>)` | `text-decoration-thickness: var(<custom-property>);` |
| `decoration-[<value>]` | `text-decoration-thickness: <value>;` |

## [Examples](https://tailwindcss.com/docs/text-decoration-thickness#examples)

### [Basic example](https://tailwindcss.com/docs/text-decoration-thickness#basic-example)

Use `decoration-<number>` utilities like `decoration-2` and `decoration-4` to change the [text decoration](https://tailwindcss.com/docs/text-decoration-line) thickness of an element:

decoration-1

The quick brown fox jumps over the lazy dog.

decoration-2

The quick brown fox jumps over the lazy dog.

decoration-4

The quick brown fox jumps over the lazy dog.

```
<p class="underline decoration-1">The quick brown fox...</p><p class="underline decoration-2">The quick brown fox...</p><p class="underline decoration-4">The quick brown fox...</p>
```

### [Using a custom value](https://tailwindcss.com/docs/text-decoration-thickness#using-a-custom-value)

Use the `decoration-[<value>]` syntax to set the text decoration thickness based on a completely custom value:

```
<p class="decoration-[0.25rem] ...">  Lorem ipsum dolor sit amet...</p>
```

For CSS variables, you can also use the `decoration-(length:<custom-property>)` syntax:

```
<p class="decoration-(length:--my-decoration-thickness) ...">  Lorem ipsum dolor sit amet...</p>
```

This is just a shorthand for `decoration-[length:var(<custom-property>)]` that adds the `var()` function for you automatically.

### [Responsive design](https://tailwindcss.com/docs/text-decoration-thickness#responsive-design)

Prefix a `text-decoration-thickness` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<p class="underline md:decoration-4 ...">  Lorem ipsum dolor sit amet...</p>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/text-decoration-thickness#quick-reference)
* [Examples](https://tailwindcss.com/docs/text-decoration-thickness#examples)
  + [Basic example](https://tailwindcss.com/docs/text-decoration-thickness#basic-example)
  + [Using a custom value](https://tailwindcss.com/docs/text-decoration-thickness#using-a-custom-value)
  + [Responsive design](https://tailwindcss.com/docs/text-decoration-thickness#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)