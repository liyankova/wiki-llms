---
url: https://bun.com/docs/guides/binary/buffer-to-arraybuffer
title: Convert a Buffer to an ArrayBuffer - Bun
source_domain: bun.com
---

# Convert a Buffer to an ArrayBuffer - Bun

The Node.js [`Buffer`](https://nodejs.org/api/buffer.html) class provides a way to view and manipulate data in an underlying `ArrayBuffer`, which is available via the `buffer` property.

Copy

```
const nodeBuf = Buffer.alloc(64);
const arrBuf = nodeBuf.buffer;
```

---

See [Docs > API > Binary Data](https://bun.com/docs/runtime/binary-data#conversion) for complete documentation on manipulating binary data with Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/binary/buffer-to-arraybuffer.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/binary/buffer-to-arraybuffer)

⌘I