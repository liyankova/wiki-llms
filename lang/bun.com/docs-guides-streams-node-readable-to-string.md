---
url: https://bun.com/docs/guides/streams/node-readable-to-string
title: Convert a Node.js Readable to a string - Bun
source_domain: bun.com
---

# Convert a Node.js Readable to a string - Bun

To convert a Node.js `Readable` stream to a string in Bun, you can create a new [`Response`](https://developer.mozilla.org/en-US/docs/Web/API/Response) object with the stream as the body, then use [`response.text()`](https://developer.mozilla.org/en-US/docs/Web/API/Response/text) to read the stream into a string.

Copy

```
import { Readable } from "stream";
const stream = Readable.from([Buffer.from("Hello, world!")]);
const text = await new Response(stream).text();
console.log(text); // "Hello, world!"
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/streams/node-readable-to-string.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/streams/node-readable-to-string)

⌘I