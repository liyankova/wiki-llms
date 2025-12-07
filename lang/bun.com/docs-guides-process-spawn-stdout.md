---
url: https://bun.com/docs/guides/process/spawn-stdout
title: Read stdout from a child process - Bun
source_domain: bun.com
---

# Read stdout from a child process - Bun

When using [`Bun.spawn()`](https://bun.com/docs/runtime/child-process), the `stdout` of the child process can be consumed as a `ReadableStream` via `proc.stdout`.

Copy

```
const proc = Bun.spawn(["echo", "hello"]);

const output = await proc.stdout.text();
output; // => "hello"
```

---

To instead pipe the `stdout` of the child process to `stdout` of the parent process, set “inherit”.

Copy

```
const proc = Bun.spawn(["echo", "hello"], {
  stdout: "inherit",
});
```

---

See [Docs > API > Child processes](https://bun.com/docs/runtime/child-process) for complete documentation.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/process/spawn-stdout.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/process/spawn-stdout)

⌘I