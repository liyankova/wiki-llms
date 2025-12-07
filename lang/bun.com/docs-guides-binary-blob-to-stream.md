---
url: https://bun.com/docs/guides/binary/blob-to-stream
title: Convert a Blob to a ReadableStream - Bun
source_domain: bun.com
---

# Convert a Blob to a ReadableStream - Bun

The [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob) class provides a number of methods for consuming its contents in different formats, including `.stream()`. This returns `Promise<ReadableStream>`.

Copy

```
const blob = new Blob(["hello world"]);
const stream = await blob.stream();
```

---

See [Docs > API > Binary Data](https://bun.com/docs/runtime/binary-data#conversion) for complete documentation on manipulating binary data with Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/binary/blob-to-stream.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/binary/blob-to-stream)

⌘I