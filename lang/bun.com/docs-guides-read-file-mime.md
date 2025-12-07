---
url: https://bun.com/docs/guides/read-file/mime
title: Get the MIME type of a file - Bun
source_domain: bun.com
---

# Get the MIME type of a file - Bun

The `Bun.file()` function accepts a path and returns a `BunFile` instance. The `BunFile` class extends `Blob`, so use the `.type` property to read the MIME type.

Copy

```
const file = Bun.file("./package.json");
file.type; // application/json

const file = Bun.file("./index.html");
file.type; // text/html

const file = Bun.file("./image.png");
file.type; // image/png
```

---

Refer to [API > File I/O](https://bun.com/docs/runtime/file-io) for more information on working with `BunFile`.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/read-file/mime.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/read-file/mime)

⌘I