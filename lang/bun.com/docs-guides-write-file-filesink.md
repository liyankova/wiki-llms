---
url: https://bun.com/docs/guides/write-file/filesink
title: Write a file incrementally - Bun
source_domain: bun.com
---

# Write a file incrementally - Bun

Bun provides an API for incrementally writing to a file. This is useful for writing large files, or for writing to a file over a long period of time.
Call `.writer()` on a `BunFile` to retrieve a `FileSink` instance. This instance can be used to efficiently buffer data and periodically “flush” it to disk. You can write & flush many times.

Copy

```
const file = Bun.file("/path/to/file.txt");
const writer = file.writer();

writer.write("lorem");
writer.write("ipsum");
writer.write("dolor");

writer.flush();

// continue writing & flushing
```

---

The `.write()` method can accept strings or binary data.

Copy

```
w.write("hello");
w.write(Buffer.from("there"));
w.write(new Uint8Array([0, 255, 128]));
writer.flush();
```

---

The `FileSink` will also auto-flush when its internal buffer is full. You can configure the buffer size with the `highWaterMark` option.

Copy

```
const file = Bun.file("/path/to/file.txt");
const writer = file.writer({ highWaterMark: 1024 * 1024 }); // 1MB
```

---

When you’re done writing to the file, call `.end()` to auto-flush the buffer and close the file.

Copy

```
writer.end();
```

---

Full documentation: [FileSink](https://bun.com/docs/runtime/file-io#incremental-writing-with-filesink).

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/write-file/filesink.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/write-file/filesink)

⌘I