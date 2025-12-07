---
url: https://bun.com/docs/guides/http/stream-node-streams-in-bun
title: Streaming HTTP Server with Node.js Streams - Bun
source_domain: bun.com
---

# Streaming HTTP Server with Node.js Streams - Bun

In Bun, [`Response`](https://developer.mozilla.org/en-US/docs/Web/API/Response) objects can accept a Node.js [`Readable`](https://nodejs.org/api/stream.html#stream_readable_streams).
This works because Bun’s `Response` object allows any async iterable as its body. Node.js streams are async iterables, so you can pass them directly to `Response`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)server.ts

Copy

```
import { Readable } from "stream";
import { serve } from "bun";
serve({
  port: 3000,
  fetch(req) {
    return new Response(Readable.from(["Hello, ", "world!"]), {
      headers: { "Content-Type": "text/plain" },
    });
  },
});
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/http/stream-node-streams-in-bun.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/http/stream-node-streams-in-bun)

⌘I