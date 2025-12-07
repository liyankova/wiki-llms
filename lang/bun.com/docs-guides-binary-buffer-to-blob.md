---
url: https://bun.com/docs/guides/binary/buffer-to-blob
title: Convert a Buffer to a blob - Bun
source_domain: bun.com
---

# Convert a Buffer to a blob - Bun

A [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob) can be constructed from an array of “chunks”, where each chunk is a string, binary data structure (including `Buffer`), or another `Blob`.

Copy

```
const buf = Buffer.from("hello");
const blob = new Blob([buf]);
```

---

See [Docs > API > Binary Data](https://bun.com/docs/runtime/binary-data#conversion) for complete documentation on manipulating binary data with Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/binary/buffer-to-blob.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/binary/buffer-to-blob)

⌘I