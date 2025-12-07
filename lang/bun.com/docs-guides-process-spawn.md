---
url: https://bun.com/docs/guides/process/spawn
title: Spawn a child process - Bun
source_domain: bun.com
---

# Spawn a child process - Bun

Use [`Bun.spawn()`](https://bun.com/docs/runtime/child-process) to spawn a child process.

Copy

```
const proc = Bun.spawn(["echo", "hello"]);

// await completion
await proc.exited;
```

---

The second argument accepts a configuration object.

Copy

```
const proc = Bun.spawn(["echo", "Hello, world!"], {
  cwd: "/tmp",
  env: { FOO: "bar" },
  onExit(proc, exitCode, signalCode, error) {
    // exit handler
  },
});
```

---

By default, the `stdout` of the child process can be consumed as a `ReadableStream` using `proc.stdout`.

Copy

```
const proc = Bun.spawn(["echo", "hello"]);

const output = await proc.stdout.text();
output; // => "hello\n"
```

---

See [Docs > API > Child processes](https://bun.com/docs/runtime/child-process) for complete documentation.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/process/spawn.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/process/spawn)

⌘I