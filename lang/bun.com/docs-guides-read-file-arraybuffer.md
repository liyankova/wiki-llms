---
url: https://bun.com/docs/guides/read-file/arraybuffer
title: Read a file to an ArrayBuffer - Bun
source_domain: bun.com
---

# Read a file to an ArrayBuffer - Bun

The `Bun.file()` function accepts a path and returns a `BunFile` instance. The `BunFile` class extends `Blob` and allows you to lazily read the file in a variety of formats. Use `.arrayBuffer()` to read the file as an `ArrayBuffer`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
const path = "/path/to/package.json";
const file = Bun.file(path);

const buffer = await file.arrayBuffer();
```

---

The binary content in the `ArrayBuffer` can then be read as a typed array, such as `Int8Array`. For `Uint8Array`, use [`.bytes()`](https://bun.com/docs/guides/read-file/uint8array).

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
const buffer = await file.arrayBuffer();
const bytes = new Int8Array(buffer);

bytes[0];
bytes.length;
```

---

Refer to the [Typed arrays](https://bun.com/docs/runtime/binary-data#typedarray) docs for more information on working with typed arrays in Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/read-file/arraybuffer.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/read-file/arraybuffer)

⌘I