---
url: https://bun.com/docs/guides/write-file/response
title: Write a Response to a file - Bun
source_domain: bun.com
---

# Write a Response to a file - Bun

This code snippet writes a `Response` to disk at a particular path. Bun will consume the `Response` body according to its `Content-Type` header.
It uses the fast [`Bun.write()`](https://bun.com/docs/runtime/file-io#writing-files-bun-write) API to efficiently write data to disk. The first argument is a *destination*, like an absolute path or `BunFile` instance. The second argument is the *data* to write.

Copy

```
const result = await fetch("https://bun.com");
const path = "./file.txt";
await Bun.write(path, result);
```

---

See [Docs > API > File I/O](https://bun.com/docs/runtime/file-io#writing-files-bun-write) for complete documentation of `Bun.write()`.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/write-file/response.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/write-file/response)

⌘I