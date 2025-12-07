---
url: https://bun.com/docs/guides/binary/buffer-to-typedarray
title: Convert a Buffer to a Uint8Array - Bun
source_domain: bun.com
---

# Convert a Buffer to a Uint8Array - Bun

The Node.js [`Buffer`](https://nodejs.org/api/buffer.html) class extends [`Uint8Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array), so no conversion is needed. All properties and methods on `Uint8Array` are available on `Buffer`.

Copy

```
const buf = Buffer.alloc(64);
buf instanceof Uint8Array; // => true
```

---

See [Docs > API > Binary Data](https://bun.com/docs/runtime/binary-data#conversion) for complete documentation on manipulating binary data with Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/binary/buffer-to-typedarray.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/binary/buffer-to-typedarray)

⌘I