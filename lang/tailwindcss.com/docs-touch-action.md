---
url: https://tailwindcss.com/docs/touch-action
title: touch-action - Interactivity - Tailwind CSS
source_domain: tailwindcss.com
---

# touch-action - Interactivity - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Interactivity
2. touch-action

Interactivity

# touch-action

Utilities for controlling how an element can be scrolled and zoomed on touchscreens.

| Class | Styles |
| --- | --- |
| `touch-auto` | `touch-action: auto;` |
| `touch-none` | `touch-action: none;` |
| `touch-pan-x` | `touch-action: pan-x;` |
| `touch-pan-left` | `touch-action: pan-left;` |
| `touch-pan-right` | `touch-action: pan-right;` |
| `touch-pan-y` | `touch-action: pan-y;` |
| `touch-pan-up` | `touch-action: pan-up;` |
| `touch-pan-down` | `touch-action: pan-down;` |
| `touch-pinch-zoom` | `touch-action: pinch-zoom;` |
| `touch-manipulation` | `touch-action: manipulation;` |

## [Examples](https://tailwindcss.com/docs/touch-action#examples)

### [Basic example](https://tailwindcss.com/docs/touch-action#basic-example)

Use utilities like `touch-pan-y` and `touch-pinch-zoom` to control how an element can be scrolled (panned) and zoomed (pinched) on touchscreens:

Try panning these images on a touchscreen

touch-auto

![](https://images.unsplash.com/photo-1554629947-334ff61d85dc?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=600&h=400&q=80)

touch-none

![](https://images.unsplash.com/photo-1554629947-334ff61d85dc?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=600&h=400&q=80)

touch-pan-x

![](https://images.unsplash.com/photo-1554629947-334ff61d85dc?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=600&h=400&q=80)

touch-pan-y

![](https://images.unsplash.com/photo-1554629947-334ff61d85dc?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=600&h=400&q=80)

```
<div class="h-48 w-full touch-auto overflow-auto ...">  <img class="h-auto w-[150%] max-w-none" src="..." /></div><div class="h-48 w-full touch-none overflow-auto ...">  <img class="h-auto w-[150%] max-w-none" src="..." /></div><div class="h-48 w-full touch-pan-x overflow-auto ...">  <img class="h-auto w-[150%] max-w-none" src="..." /></div><div class="h-48 w-full touch-pan-y overflow-auto ...">  <img class="h-auto w-[150%] max-w-none" src="..." /></div>
```

### [Responsive design](https://tailwindcss.com/docs/touch-action#responsive-design)

Prefix a `touch-action` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<div class="touch-pan-x md:touch-auto ...">  <!-- ... --></div>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/touch-action#quick-reference)
* [Examples](https://tailwindcss.com/docs/touch-action#examples)
  + [Basic example](https://tailwindcss.com/docs/touch-action#basic-example)
  + [Responsive design](https://tailwindcss.com/docs/touch-action#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)