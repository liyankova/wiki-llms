---
url: https://bun.com/docs/guides/streams/node-readable-to-arraybuffer
title: Convert a Node.js Readable to an ArrayBuffer - Bun
source_domain: bun.com
---

# Convert a Node.js Readable to an ArrayBuffer - Bun

To convert a Node.js `Readable` stream to an `ArrayBuffer` in Bun, you can create a new `Response` object with the stream as the body, then use `arrayBuffer()` to read the stream into an `ArrayBuffer`.

Copy

```
import { Readable } from "stream";
const stream = Readable.from(["Hello, ", "world!"]);
const buf = await new Response(stream).arrayBuffer();
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/streams/node-readable-to-arraybuffer.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/streams/node-readable-to-arraybuffer)

⌘I