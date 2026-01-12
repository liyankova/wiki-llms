---
url: https://tailwindcss.com/docs/content
title: content - Typography - Tailwind CSS
source_domain: tailwindcss.com
---

# content - Typography - Tailwind CSS

[Docs](https://tailwindcss.com/docs)[Blog](https://tailwindcss.com/blog)[Showcase](https://tailwindcss.com/showcase)[Sponsor](https://tailwindcss.com/sponsor)[Plus](https://tailwindcss.com/plus?ref=top)

1. Typography
2. content

Typography

# content

Utilities for controlling the content of the before and after pseudo-elements.

| Class | Styles |
| --- | --- |
| `content-[<value>]` | `content: <value>;` |
| `content-(<custom-property>)` | `content: var(<custom-property>);` |
| `content-none` | `content: none;` |

## [Examples](https://tailwindcss.com/docs/content#examples)

### [Basic example](https://tailwindcss.com/docs/content#basic-example)

Use the `content-[<value>]` syntax, along with the `before` and `after` variants, to set the contents of the `::before` and `::after` pseudo-elements:

Higher resolution means more than just a better-quality image. With a Retina 6K display, [Pro Display XDR](https://www.apple.com/pro-display-xdr/) gives you nearly 40 percent more screen real estate than a 5K display.

```
<p>Higher resolution means more than just a better-quality image. With aRetina 6K display, <a class="text-blue-600 after:content-['_↗']" href="...">Pro Display XDR</a> gives you nearly 40 percent more screen real estate thana 5K display.</p>
```

### [Referencing an attribute value](https://tailwindcss.com/docs/content#referencing-an-attribute-value)

Use the `content-[attr(<name>)]` syntax to reference a value stored in an attribute using the `attr()` CSS function:

```
<p before="Hello World" class="before:content-[attr(before)] ...">  <!-- ... --></p>
```

### [Using spaces and underscores](https://tailwindcss.com/docs/content#using-spaces-and-underscores)

Since whitespace denotes the end of a class in HTML, replace any spaces in an arbitrary value with an underscore:

```
<p class="before:content-['Hello_World'] ..."></p>
```

If you need to include an actual underscore, you can do this by escaping it with a backslash:

```
<p class="before:content-['Hello\_World']"></p>
```

### [Using a CSS variable](https://tailwindcss.com/docs/content#using-a-css-variable)

Use the `content-(<custom-property>)` syntax to control the contents of the `::before` and `::after` pseudo-elements using a CSS variable:

```
<p class="content-(--my-content)"></p>
```

This is just a shorthand for `content-[var(<custom-property>)]` that adds the `var()` function for you automatically.

### [Responsive design](https://tailwindcss.com/docs/content#responsive-design)

Prefix a `content` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<p class="before:content-['Mobile'] md:before:content-['Desktop'] ..."></p>
```

Learn more about using variants in the [variants documentation](https://tailwindcss.com/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](https://tailwindcss.com/docs/content#quick-reference)
* [Examples](https://tailwindcss.com/docs/content#examples)
  + [Basic example](https://tailwindcss.com/docs/content#basic-example)
  + [Referencing an attribute value](https://tailwindcss.com/docs/content#referencing-an-attribute-value)
  + [Using spaces and underscores](https://tailwindcss.com/docs/content#using-spaces-and-underscores)
  + [Using a CSS variable](https://tailwindcss.com/docs/content#using-a-css-variable)
  + [Responsive design](https://tailwindcss.com/docs/content#responsive-design)

Copyright © 2025 Tailwind Labs Inc.·[Trademark Policy](https://tailwindcss.com/brand)