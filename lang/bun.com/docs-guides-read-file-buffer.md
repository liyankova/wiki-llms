---
url: https://bun.com/docs/guides/read-file/buffer
title: Read a file to a Buffer - Bun
source_domain: bun.com
---

# Read a file to a Buffer - Bun

The `Bun.file()` function accepts a path and returns a `BunFile` instance. The `BunFile` class extends `Blob` and allows you to lazily read the file in a variety of formats.
To read the file into a `Buffer` instance, first use `.arrayBuffer()` to consume the file as an `ArrayBuffer`, then use `Buffer.from()` to create a `Buffer` from the `ArrayBuffer`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
const path = "/path/to/package.json";
const file = Bun.file(path);

const arrbuf = await file.arrayBuffer();
const buffer = Buffer.from(arrbuf);
```

---

Refer to [Binary data > Buffer](https://bun.com/docs/runtime/binary-data#buffer) for more information on working with `Buffer` and other binary data formats in Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/read-file/buffer.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/read-file/buffer)

⌘I