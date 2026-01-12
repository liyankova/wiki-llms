---
url: https://tailwindcss.com/docs/list-style-position
title: list-style-position - Typography - Tailwind CSS
source_domain: tailwindcss.com
---

# list-style-position - Typography - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Typography
2. list-style-position

Typography

# list-style-position

Utilities for controlling the position of bullets and numbers in lists.

| Class | Styles |
| --- | --- |
| `list-inside` | `list-style-position: inside;` |
| `list-outside` | `list-style-position: outside;` |

## [Examples](https://tailwindcss.com/docs/list-style-position#examples)

### [Basic example](https://tailwindcss.com/docs/list-style-position#basic-example)

Use utilities like `list-inside` and `list-outside` to control the position of the markers and text indentation in a list:

list-inside

* 5 cups chopped Porcini mushrooms
* 1/2 cup of olive oil
* 3lb of celery

list-outside

* 5 cups chopped Porcini mushrooms
* 1/2 cup of olive oil
* 3lb of celery

```
<ul class="list-inside">  <li>5 cups chopped Porcini mushrooms</li>  <!-- ... --></ul><ul class="list-outside">  <li>5 cups chopped Porcini mushrooms</li>  <!-- ... --></ul>
```

### [Responsive design](https://tailwindcss.com/docs/list-style-position#responsive-design)

Prefix a `list-style-position` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<ul class="list-outside md:list-inside ...">  <!-- ... --></ul>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/list-style-position#quick-reference)
* [Examples](https://tailwindcss.com/docs/list-style-position#examples)
  + [Basic example](https://tailwindcss.com/docs/list-style-position#basic-example)
  + [Responsive design](https://tailwindcss.com/docs/list-style-position#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)