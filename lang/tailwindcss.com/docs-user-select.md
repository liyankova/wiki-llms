---
url: https://tailwindcss.com/docs/user-select
title: user-select - Interactivity - Tailwind CSS
source_domain: tailwindcss.com
---

# user-select - Interactivity - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Interactivity
2. user-select

Interactivity

# user-select

Utilities for controlling whether the user can select text in an element.

| Class | Styles |
| --- | --- |
| `select-none` | `user-select: none;` |
| `select-text` | `user-select: text;` |
| `select-all` | `user-select: all;` |
| `select-auto` | `user-select: auto;` |

## [Examples](https://tailwindcss.com/docs/user-select#examples)

### [Disabling text selection](https://tailwindcss.com/docs/user-select#disabling-text-selection)

Use the `select-none` utility to prevent selecting text in an element and its children:

Try selecting the text to see the expected behavior

The quick brown fox jumps over the lazy dog.

```
<div class="select-none ...">The quick brown fox jumps over the lazy dog.</div>
```

### [Allowing text selection](https://tailwindcss.com/docs/user-select#allowing-text-selection)

Use the `select-text` utility to allow selecting text in an element and its children:

Try selecting the text to see the expected behavior

The quick brown fox jumps over the lazy dog.

```
<div class="select-text ...">The quick brown fox jumps over the lazy dog.</div>
```

### [Selecting all text in one click](https://tailwindcss.com/docs/user-select#selecting-all-text-in-one-click)

Use the `select-all` utility to automatically select all the text in an element when a user clicks:

Try clicking the text to see the expected behavior

The quick brown fox jumps over the lazy dog.

```
<div class="select-all ...">The quick brown fox jumps over the lazy dog.</div>
```

### [Using auto select behavior](https://tailwindcss.com/docs/user-select#using-auto-select-behavior)

Use the `select-auto` utility to use the default browser behavior for selecting text:

Try selecting the text to see the expected behavior

The quick brown fox jumps over the lazy dog.

```
<div class="select-auto ...">The quick brown fox jumps over the lazy dog.</div>
```

### [Responsive design](https://tailwindcss.com/docs/user-select#responsive-design)

Prefix an `user-select` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<div class="select-none md:select-all ...">  <!-- ... --></div>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/user-select#quick-reference)
* [Examples](https://tailwindcss.com/docs/user-select#examples)
  + [Disabling text selection](https://tailwindcss.com/docs/user-select#disabling-text-selection)
  + [Allowing text selection](https://tailwindcss.com/docs/user-select#allowing-text-selection)
  + [Selecting all text in one click](https://tailwindcss.com/docs/user-select#selecting-all-text-in-one-click)
  + [Using auto select behavior](https://tailwindcss.com/docs/user-select#using-auto-select-behavior)
  + [Responsive design](https://tailwindcss.com/docs/user-select#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)