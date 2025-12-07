---
url: https://bun.com/docs/guides/binary/blob-to-dataview
title: Convert a Blob to a DataView - Bun
source_domain: bun.com
---

# Convert a Blob to a DataView - Bun

The [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob) class provides a number of methods for consuming its contents in different formats. This snippets reads the contents to an `ArrayBuffer`, then creates a `DataView` from the buffer.

Copy

```
const blob = new Blob(["hello world"]);
const arr = new DataView(await blob.arrayBuffer());
```

---

See [Docs > API > Binary Data](https://bun.com/docs/runtime/binary-data#conversion) for complete documentation on manipulating binary data with Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/binary/blob-to-dataview.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/binary/blob-to-dataview)

⌘I