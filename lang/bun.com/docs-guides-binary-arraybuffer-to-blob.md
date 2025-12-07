---
url: https://bun.com/docs/guides/binary/arraybuffer-to-blob
title: Convert an ArrayBuffer to a Blob - Bun
source_domain: bun.com
---

# Convert an ArrayBuffer to a Blob - Bun

A [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob) can be constructed from an array of “chunks”, where each chunk is a string, binary data structure, or another `Blob`.

Copy

```
const buf = new ArrayBuffer(64);
const blob = new Blob([buf]);
```

---

By default the `type` of the resulting `Blob` will be unset. This can be set manually.

Copy

```
const buf = new ArrayBuffer(64);
const blob = new Blob([buf], { type: "application/octet-stream" });
blob.type; // => "application/octet-stream"
```

---

See [Docs > API > Binary Data](https://bun.com/docs/runtime/binary-data#conversion) for complete documentation on manipulating binary data with Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/binary/arraybuffer-to-blob.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/binary/arraybuffer-to-blob)

⌘I