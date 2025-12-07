---
url: https://bun.com/docs/guides/binary/blob-to-arraybuffer
title: Convert a Blob to an ArrayBuffer - Bun
source_domain: bun.com
---

# Convert a Blob to an ArrayBuffer - Bun

The [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob) class provides a number of methods for consuming its contents in different formats, including `.arrayBuffer()`.

Copy

```
const blob = new Blob(["hello world"]);
const buf = await blob.arrayBuffer();
```

---

See [Docs > API > Binary Data](https://bun.com/docs/runtime/binary-data#conversion) for complete documentation on manipulating binary data with Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/binary/blob-to-arraybuffer.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/binary/blob-to-arraybuffer)

⌘I