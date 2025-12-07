---
url: https://bun.com/docs/guides/util/gzip
title: Compress and decompress data with gzip - Bun
source_domain: bun.com
---

# Compress and decompress data with gzip - Bun

Use `Bun.gzipSync()` to compress a `Uint8Array` with gzip.

Copy

```
const data = Buffer.from("Hello, world!");
const compressed = Bun.gzipSync(data);
// => Uint8Array

const decompressed = Bun.gunzipSync(compressed);
// => Uint8Array
```

---

See [Docs > API > Utils](https://bun.com/docs/runtime/utils) for more useful utilities.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/util/gzip.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/util/gzip)

⌘I