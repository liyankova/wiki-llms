---
url: https://bun.com/docs/guides/process/spawn-stderr
title: Read stderr from a child process - Bun
source_domain: bun.com
---

# Read stderr from a child process - Bun

When using [`Bun.spawn()`](https://bun.com/docs/runtime/child-process), the child process inherits the `stderr` of the spawning process. If instead you’d prefer to read and handle `stderr`, set the `stderr` option to `"pipe"`.

Copy

```
const proc = Bun.spawn(["echo", "hello"], {
  stderr: "pipe",
});

proc.stderr; // => ReadableStream
```

---

To read `stderr` until the child process exits, use .text()

Copy

```
const proc = Bun.spawn(["echo", "hello"], {
  stderr: "pipe",
});

const errors: string = await proc.stderr.text();
if (errors) {
  // handle errors
}
```

---

See [Docs > API > Child processes](https://bun.com/docs/runtime/child-process) for complete documentation.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/process/spawn-stderr.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/process/spawn-stderr)

⌘I