---
url: https://bun.com/docs/guides/http/stream-file
title: Stream a file as an HTTP Response - Bun
source_domain: bun.com
---

# Stream a file as an HTTP Response - Bun

This snippet reads a file from disk using [`Bun.file()`](https://bun.com/docs/runtime/file-io#reading-files-bun-file). This returns a `BunFile` instance, which can be passed directly into the `new Response` constructor.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)server.ts

Copy

```
const path = "/path/to/file.txt";
const file = Bun.file(path);
const resp = new Response(file);
```

---

The `Content-Type` is read from the file and automatically set on the `Response`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)server.ts

Copy

```
new Response(Bun.file("./package.json")).headers.get("Content-Type");
// => application/json;charset=utf-8

new Response(Bun.file("./test.txt")).headers.get("Content-Type");
// => text/plain;charset=utf-8

new Response(Bun.file("./index.tsx")).headers.get("Content-Type");
// => text/javascript;charset=utf-8

new Response(Bun.file("./img.png")).headers.get("Content-Type");
// => image/png
```

---

Putting it all together with [`Bun.serve()`](https://bun.com/docs/runtime/http/server).

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)server.ts

Copy

```
// static file server
Bun.serve({
  async fetch(req) {
    const path = new URL(req.url).pathname;
    const file = Bun.file(path);
    return new Response(file);
  },
});
```

---

See [Docs > API > File I/O](https://bun.com/docs/runtime/file-io#writing-files-bun-write) for complete documentation of `Bun.write()`.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/http/stream-file.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/http/stream-file)

⌘I