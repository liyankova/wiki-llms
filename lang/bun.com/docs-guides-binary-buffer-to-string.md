---
url: https://bun.com/docs/guides/binary/buffer-to-string
title: Convert a Buffer to a string - Bun
source_domain: bun.com
---

# Convert a Buffer to a string - Bun

The [`Buffer`](https://nodejs.org/api/buffer.html) class provides a built-in `.toString()` method that converts a `Buffer` to a string.

Copy

```
const buf = Buffer.from("hello");
const str = buf.toString();
// => "hello"
```

---

You can optionally specify an encoding and byte range.

Copy

```
const buf = Buffer.from("hello world!");
const str = buf.toString("utf8", 0, 5);
// => "hello"
```

---

See [Docs > API > Binary Data](https://bun.com/docs/runtime/binary-data#conversion) for complete documentation on manipulating binary data with Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/binary/buffer-to-string.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/binary/buffer-to-string)

⌘I