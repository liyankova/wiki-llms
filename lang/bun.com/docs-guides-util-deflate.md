---
url: https://bun.com/docs/guides/util/deflate
title: Compress and decompress data with DEFLATE - Bun
source_domain: bun.com
---

# Compress and decompress data with DEFLATE - Bun

Use `Bun.deflateSync()` to compress a `Uint8Array` with DEFLATE.

Copy

```
const data = Buffer.from("Hello, world!");
const compressed = Bun.deflateSync("Hello, world!");
// => Uint8Array

const decompressed = Bun.inflateSync(compressed);
// => Uint8Array
```

---

See [Docs > API > Utils](https://bun.com/docs/runtime/utils) for more useful utilities.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/util/deflate.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/util/deflate)

⌘I