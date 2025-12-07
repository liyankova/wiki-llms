---
url: https://bun.com/docs/guides/write-file/file-cp
title: Copy a file to another location - Bun
source_domain: bun.com
---

# Copy a file to another location - Bun

This code snippet copies a file to another location on disk.
It uses the fast [`Bun.write()`](https://bun.com/docs/runtime/file-io#writing-files-bun-write) API to efficiently write data to disk. The first argument is a *destination*, like an absolute path or `BunFile` instance. The second argument is the *data* to write.

Copy

```
const file = Bun.file("/path/to/original.txt");
await Bun.write("/path/to/copy.txt", file);
```

---

See [Docs > API > File I/O](https://bun.com/docs/runtime/file-io#writing-files-bun-write) for complete documentation of `Bun.write()`.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/write-file/file-cp.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/write-file/file-cp)

⌘I