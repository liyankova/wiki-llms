---
url: https://bun.com/docs/guides/streams/to-blob
title: Convert a ReadableStream to a Blob - Bun
source_domain: bun.com
---

# Convert a ReadableStream to a Blob - Bun

Bun provides a number of convenience functions for reading the contents of a [`ReadableStream`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream) into different formats.

Copy

```
const stream = new ReadableStream();
const blob = await Bun.readableStreamToBlob(stream);
```

---

See [Docs > API > Utils](https://bun.com/docs/runtime/utils#bun-readablestreamto) for documentation on Bun’s other `ReadableStream` conversion functions.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/streams/to-blob.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/streams/to-blob)

⌘I