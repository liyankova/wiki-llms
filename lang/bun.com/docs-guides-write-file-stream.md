---
url: https://bun.com/docs/guides/write-file/stream
title: Write a ReadableStream to a file - Bun
source_domain: bun.com
---

# Write a ReadableStream to a file - Bun

To write a `ReadableStream` to disk, first create a `Response` instance from the stream. This `Response` can then be written to disk using [`Bun.write()`](https://bun.com/docs/runtime/file-io#writing-files-bun-write).

Copy

```
const stream: ReadableStream = ...;
const path = "./file.txt";
const response = new Response(stream);

await Bun.write(path, response);
```

---

See [Docs > API > File I/O](https://bun.com/docs/runtime/file-io#writing-files-bun-write) for complete documentation of `Bun.write()`.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/write-file/stream.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/write-file/stream)

⌘I