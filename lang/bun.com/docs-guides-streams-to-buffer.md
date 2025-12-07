---
url: https://bun.com/docs/guides/streams/to-buffer
title: Convert a ReadableStream to a Buffer - Bun
source_domain: bun.com
---

# Convert a ReadableStream to a Buffer - Bun

Bun provides a number of convenience functions for reading the contents of a [`ReadableStream`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream) into different formats. This snippet reads the contents of a `ReadableStream` to an [`ArrayBuffer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer), then creates a [`Buffer`](https://nodejs.org/api/buffer.html) that points to it.

Copy

```
const stream = new ReadableStream();
const arrBuf = await Bun.readableStreamToArrayBuffer(stream);
const nodeBuf = Buffer.from(arrBuf);
```

---

See [Docs > API > Utils](https://bun.com/docs/runtime/utils#bun-readablestreamto) for documentation on Bun’s other `ReadableStream` conversion functions.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/streams/to-buffer.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/streams/to-buffer)

⌘I