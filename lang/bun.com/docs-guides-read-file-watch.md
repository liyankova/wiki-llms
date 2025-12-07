---
url: https://bun.com/docs/guides/read-file/watch
title: Watch a directory for changes - Bun
source_domain: bun.com
---

# Watch a directory for changes - Bun

Bun implements the `node:fs` module, including the `fs.watch` function for listening for file system changes.
This code block listens for changes to files in the current directory. By default this operation is *shallow*, meaning that changes to files in subdirectories will not be detected.

Copy

```
import { watch } from "fs";

const watcher = watch(import.meta.dir, (event, filename) => {
  console.log(`Detected ${event} in ${filename}`);
});
```

---

To listen to changes in subdirectories, pass the `recursive: true` option to `fs.watch`.

Copy

```
import { watch } from "fs";

const watcher = watch(import.meta.dir, { recursive: true }, (event, relativePath) => {
  console.log(`Detected ${event} in ${relativePath}`);
});
```

---

Using the `node:fs/promises` module, you can listen for changes using `for await...of` instead of a callback.

Copy

```
import { watch } from "fs/promises";

const watcher = watch(import.meta.dir);
for await (const event of watcher) {
  console.log(`Detected ${event.eventType} in ${event.filename}`);
}
```

---

To stop listening for changes, call `watcher.close()`. It’s common to do this when the process receives a `SIGINT` signal, such as when the user presses Ctrl-C.

Copy

```
import { watch } from "fs";

const watcher = watch(import.meta.dir, (event, filename) => {
  console.log(`Detected ${event} in ${filename}`);
});

process.on("SIGINT", () => {
  // close watcher when Ctrl-C is pressed
  console.log("Closing watcher...");
  watcher.close();

  process.exit(0);
});
```

---

Refer to [API > Binary data > Typed arrays](https://bun.com/docs/runtime/binary-data#typedarray) for more information on working with `Uint8Array` and other binary data formats in Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/read-file/watch.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/read-file/watch)

⌘I