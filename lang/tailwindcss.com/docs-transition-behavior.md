---
url: https://tailwindcss.com/docs/transition-behavior
title: transition-behavior - Transitions & Animation - Tailwind CSS
source_domain: tailwindcss.com
---

# transition-behavior - Transitions & Animation - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Transitions & Animation
2. transition-behavior

Transitions & Animation

# transition-behavior

Utilities to control the behavior of CSS transitions.

| Class | Styles |
| --- | --- |
| `transition-normal` | `transition-behavior: normal;` |
| `transition-discrete` | `transition-behavior: allow-discrete;` |

## [Examples](https://tailwindcss.com/docs/transition-behavior#examples)

### [Basic example](https://tailwindcss.com/docs/transition-behavior#basic-example)

Use the `transition-discrete` utility to start transitions when changing properties with a discrete set of values, such as elements that change from `hidden` to `block`:

Interact with the checkboxes to see the expected behavior

transition-normal

transition-discrete

```
<label class="peer ...">  <input type="checkbox" checked /></label><button class="hidden transition-all not-peer-has-checked:opacity-0 peer-has-checked:block ...">  I hide</button><label class="peer ...">  <input type="checkbox" checked /></label><button class="hidden transition-all transition-discrete not-peer-has-checked:opacity-0 peer-has-checked:block ...">  I fade out</button>
```

### [Responsive design](https://tailwindcss.com/docs/transition-behavior#responsive-design)

Prefix a `transition-behavior` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<button class="transition-discrete md:transition-normal ...">  <!-- ... --></button>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/transition-behavior#quick-reference)
* [Examples](https://tailwindcss.com/docs/transition-behavior#examples)
  + [Basic example](https://tailwindcss.com/docs/transition-behavior#basic-example)
  + [Responsive design](https://tailwindcss.com/docs/transition-behavior#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)