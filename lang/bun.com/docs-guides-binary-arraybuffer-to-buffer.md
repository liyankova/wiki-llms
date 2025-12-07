---
url: https://bun.com/docs/guides/binary/arraybuffer-to-buffer
title: Convert an ArrayBuffer to a Buffer - Bun
source_domain: bun.com
---

# Convert an ArrayBuffer to a Buffer - Bun

The Node.js [`Buffer`](https://nodejs.org/api/buffer.html) API predates the introduction of `ArrayBuffer` into the JavaScript language. Bun implements both.
Use the static `Buffer.from()` method to create a `Buffer` from an `ArrayBuffer`.

Copy

```
const arrBuffer = new ArrayBuffer(64);
const nodeBuffer = Buffer.from(arrBuffer);
```

---

To create a `Buffer` that only views a portion of the underlying buffer, pass the offset and length to the constructor.

Copy

```
const arrBuffer = new ArrayBuffer(64);
const nodeBuffer = Buffer.from(arrBuffer, 0, 16); // view first 16 bytes
```

---

See [Docs > API > Binary Data](https://bun.com/docs/runtime/binary-data#conversion) for complete documentation on manipulating binary data with Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/binary/arraybuffer-to-buffer.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/binary/arraybuffer-to-buffer)

⌘I