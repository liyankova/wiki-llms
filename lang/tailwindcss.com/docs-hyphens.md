---
url: https://tailwindcss.com/docs/hyphens
title: hyphens - Typography - Tailwind CSS
source_domain: tailwindcss.com
---

# hyphens - Typography - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Typography
2. hyphens

Typography

# hyphens

Utilities for controlling how words should be hyphenated.

| Class | Styles |
| --- | --- |
| `hyphens-none` | `hyphens: none;` |
| `hyphens-manual` | `hyphens: manual;` |
| `hyphens-auto` | `hyphens: auto;` |

## [Examples](https://tailwindcss.com/docs/hyphens#examples)

### [Preventing hyphenation](https://tailwindcss.com/docs/hyphens#preventing-hyphenation)

Use the `hyphens-none` utility to prevent words from being hyphenated even if the line break suggestion `&shy;` is used:

Officially recognized by the Duden dictionary as the longest word in German, Kraftfahrzeug­haftpflichtversicherung is a 36 letter word for motor vehicle liability insurance.

```
<p class="hyphens-none">  ... Kraftfahrzeug&shy;haftpflichtversicherung is a ...</p>
```

### [Manual hyphenation](https://tailwindcss.com/docs/hyphens#manual-hyphenation)

Use the `hyphens-manual` utility to only set hyphenation points where the line break suggestion `&shy;` is used:

Officially recognized by the Duden dictionary as the longest word in German, Kraftfahrzeug­haftpflichtversicherung is a 36 letter word for motor vehicle liability insurance.

```
<p class="hyphens-manual">  ... Kraftfahrzeug&shy;haftpflichtversicherung is a ...</p>
```

This is the default browser behavior.

### [Automatic hyphenation](https://tailwindcss.com/docs/hyphens#automatic-hyphenation)

Use the `hyphens-auto` utility to allow the browser to automatically choose hyphenation points based on the language:

Officially recognized by the Duden dictionary as the longest word in German, Kraftfahrzeughaftpflichtversicherung is a 36 letter word for motor vehicle liability insurance.

```
<p class="hyphens-auto" lang="de">  ... Kraftfahrzeughaftpflichtversicherung is a ...</p>
```

The line break suggestion `&shy;` will be preferred over automatic hyphenation points.

### [Responsive design](https://tailwindcss.com/docs/hyphens#responsive-design)

Prefix a `hyphens` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<p class="hyphens-none md:hyphens-auto ...">  Lorem ipsum dolor sit amet...</p>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/hyphens#quick-reference)
* [Examples](https://tailwindcss.com/docs/hyphens#examples)
  + [Preventing hyphenation](https://tailwindcss.com/docs/hyphens#preventing-hyphenation)
  + [Manual hyphenation](https://tailwindcss.com/docs/hyphens#manual-hyphenation)
  + [Automatic hyphenation](https://tailwindcss.com/docs/hyphens#automatic-hyphenation)
  + [Responsive design](https://tailwindcss.com/docs/hyphens#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)