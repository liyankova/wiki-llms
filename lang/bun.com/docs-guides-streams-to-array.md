---
url: https://bun.com/docs/guides/streams/to-array
title: Convert a ReadableStream to an array of chunks - Bun
source_domain: bun.com
---

# Convert a ReadableStream to an array of chunks - Bun

Bun provides a number of convenience functions for reading the contents of a [`ReadableStream`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream) into different formats. The `Bun.readableStreamToArray` function reads the contents of a `ReadableStream` to an array of chunks.

Copy

```
const stream = new ReadableStream();
const str = await Bun.readableStreamToArray(stream);
```

---

See [Docs > API > Utils](https://bun.com/docs/runtime/utils#bun-readablestreamto) for documentation on Bun’s other `ReadableStream` conversion functions.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/streams/to-array.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/streams/to-array)

⌘I