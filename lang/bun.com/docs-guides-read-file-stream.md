---
url: https://bun.com/docs/guides/read-file/stream
title: Read a file as a ReadableStream - Bun
source_domain: bun.com
---

# Read a file as a ReadableStream - Bun

The `Bun.file()` function accepts a path and returns a `BunFile` instance. The `BunFile` class extends `Blob` and allows you to lazily read the file in a variety of formats. Use `.stream()` to consume the file incrementally as a `ReadableStream`.

Copy

```
const path = "/path/to/package.json";
const file = Bun.file(path);

const stream = file.stream();
```

---

The chunks of the stream can be consumed as an [async iterable](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols#the_async_iterator_and_async_iterable_protocols) using `for await`.

Copy

```
for await (const chunk of stream) {
  chunk; // => Uint8Array
}
```

---

Refer to the [Streams](https://bun.com/docs/runtime/streams) documentation for more information on working with streams in Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/read-file/stream.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/read-file/stream)

⌘I