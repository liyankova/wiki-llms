---
url: https://bun.com/docs/guides/util/escape-html
title: Escape an HTML string - Bun
source_domain: bun.com
---

# Escape an HTML string - Bun

The `Bun.escapeHTML()` utility can be used to escape HTML characters in a string. The following replacements are made.

* `"` becomes `"&quot;"`
* `&` becomes `"&amp;"`
* `'` becomes `"&#x27;"`
* `<` becomes `"&lt;"`
* `>` becomes `"&gt;"`

This function is optimized for large input. Non-string types will be converted to a string before escaping.

Copy

```
Bun.escapeHTML("<script>alert('Hello World!')</script>");
// &lt;script&gt;alert(&#x27;Hello World!&#x27;)&lt;&#x2F;script&gt;
```

---

See [Docs > API > Utils](https://bun.com/docs/runtime/utils) for more useful utilities.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/util/escape-html.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/util/escape-html)

⌘I