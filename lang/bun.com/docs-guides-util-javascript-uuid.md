---
url: https://bun.com/docs/guides/util/javascript-uuid
title: Generate a UUID - Bun
source_domain: bun.com
---

# Generate a UUID - Bun

Use `crypto.randomUUID()` to generate a UUID v4. This API works in Bun, Node.js, and browsers. It requires no dependencies.

Copy

```
crypto.randomUUID();
// => "123e4567-e89b-42d3-a456-426614174000"
```

---

In Bun, you can also use `Bun.randomUUIDv7()` to generate a [UUID v7](https://www.ietf.org/archive/id/draft-peabody-dispatch-new-uuid-format-01.html).

Copy

```
Bun.randomUUIDv7();
// => "0196a000-bb12-7000-905e-8039f5d5b206"
```

---

See [Docs > API > Utils](https://bun.com/docs/runtime/utils) for more useful utilities.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/util/javascript-uuid.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/util/javascript-uuid)

⌘I