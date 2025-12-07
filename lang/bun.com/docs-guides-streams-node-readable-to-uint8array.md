---
url: https://bun.com/docs/guides/streams/node-readable-to-uint8array
title: Convert a Node.js Readable to an Uint8Array - Bun
source_domain: bun.com
---

# Convert a Node.js Readable to an Uint8Array - Bun

To convert a Node.js `Readable` stream to an `Uint8Array` in Bun, you can create a new `Response` object with the stream as the body, then use `bytes()` to read the stream into an `Uint8Array`.

Copy

```
import { Readable } from "stream";
const stream = Readable.from(["Hello, ", "world!"]);
const buf = await new Response(stream).bytes();
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/streams/node-readable-to-uint8array.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/streams/node-readable-to-uint8array)

⌘I