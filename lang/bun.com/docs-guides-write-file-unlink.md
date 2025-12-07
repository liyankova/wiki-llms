---
url: https://bun.com/docs/guides/write-file/unlink
title: Delete a file - Bun
source_domain: bun.com
---

# Delete a file - Bun

The `Bun.file()` function accepts a path and returns a `BunFile` instance. Use the `.delete()` method to delete the file.

Copy

```
const path = "/path/to/file.txt";
const file = Bun.file(path);

await file.delete();
```

---

See [Docs > API > File I/O](https://bun.com/docs/runtime/file-io#reading-files-bun-file) for complete documentation of `Bun.file()`.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/write-file/unlink.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/write-file/unlink)

⌘I