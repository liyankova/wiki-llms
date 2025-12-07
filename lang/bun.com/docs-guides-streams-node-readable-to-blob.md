---
url: https://bun.com/docs/guides/streams/node-readable-to-blob
title: Convert a Node.js Readable to a Blob - Bun
source_domain: bun.com
---

# Convert a Node.js Readable to a Blob - Bun

To convert a Node.js `Readable` stream to a [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob) in Bun, you can create a new [`Response`](https://developer.mozilla.org/en-US/docs/Web/API/Response) object with the stream as the body, then use [`response.blob()`](https://developer.mozilla.org/en-US/docs/Web/API/Response/blob) to read the stream into a [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob).

Copy

```
import { Readable } from "stream";
const stream = Readable.from(["Hello, ", "world!"]);
const blob = await new Response(stream).blob();
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/streams/node-readable-to-blob.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/streams/node-readable-to-blob)

⌘I