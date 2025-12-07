---
url: https://bun.com/docs/guides/binary/typedarray-to-blob
title: Convert a Uint8Array to a Blob - Bun
source_domain: bun.com
---

# Convert a Uint8Array to a Blob - Bun

A [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob) can be constructed from an array of “chunks”, where each chunk is a string, binary data structure (including `Uint8Array`), or another `Blob`.

Copy

```
const arr = new Uint8Array([0x68, 0x65, 0x6c, 0x6c, 0x6f]);
const blob = new Blob([arr]);
console.log(await blob.text());
// => "hello"
```

---

See [Docs > API > Binary Data](https://bun.com/docs/runtime/binary-data#conversion) for complete documentation on manipulating binary data with Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/binary/typedarray-to-blob.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/binary/typedarray-to-blob)

⌘I