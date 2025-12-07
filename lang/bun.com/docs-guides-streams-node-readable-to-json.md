---
url: https://bun.com/docs/guides/streams/node-readable-to-json
title: Convert a Node.js Readable to JSON - Bun
source_domain: bun.com
---

# Convert a Node.js Readable to JSON - Bun

To convert a Node.js `Readable` stream to a JSON object in Bun, you can create a new [`Response`](https://developer.mozilla.org/en-US/docs/Web/API/Response) object with the stream as the body, then use [`response.json()`](https://developer.mozilla.org/en-US/docs/Web/API/Response/json) to read the stream into a JSON object.

Copy

```
import { Readable } from "stream";
const stream = Readable.from([JSON.stringify({ hello: "world" })]);
const json = await new Response(stream).json();
console.log(json); // { hello: "world" }
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/streams/node-readable-to-json.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/streams/node-readable-to-json)

⌘I