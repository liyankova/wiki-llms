---
url: https://bun.com/docs/guides/binary/typedarray-to-buffer
title: Convert a Uint8Array to a Buffer - Bun
source_domain: bun.com
---

# Convert a Uint8Array to a Buffer - Bun

The [`Buffer`](https://nodejs.org/api/buffer.html) class extends [`Uint8Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array) with a number of additional methods. Use `Buffer.from()` to create a `Buffer` instance from a `Uint8Array`.

Copy

```
const arr: Uint8Array = ...
const buf = Buffer.from(arr);
```

---

See [Docs > API > Binary Data](https://bun.com/docs/runtime/binary-data#conversion) for complete documentation on manipulating binary data with Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/binary/typedarray-to-buffer.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/binary/typedarray-to-buffer)

⌘I