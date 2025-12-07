---
url: https://bun.com/docs/guides/write-file/stdout
title: Write to stdout - Bun
source_domain: bun.com
---

# Write to stdout - Bun

The `console.log` function writes to `stdout`. It will automatically append a line break at the end of the printed data.

Copy

```
console.log("Lorem ipsum");
```

---

For more advanced use cases, Bun exposes `stdout` as a `BunFile` via the `Bun.stdout` property. This can be used as a destination for [`Bun.write()`](https://bun.com/docs/runtime/file-io#writing-files-bun-write).

Copy

```
await Bun.write(Bun.stdout, "Lorem ipsum");
```

---

See [Docs > API > File I/O](https://bun.com/docs/runtime/file-io#writing-files-bun-write) for complete documentation of `Bun.write()`.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/write-file/stdout.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/write-file/stdout)

⌘I