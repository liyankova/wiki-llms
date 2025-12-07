---
url: https://bun.com/docs/guides/process/os-signals
title: Listen to OS signals - Bun
source_domain: bun.com
---

# Listen to OS signals - Bun

Bun supports the Node.js `process` global, including the `process.on()` method for listening to OS signals.

Copy

```
process.on("SIGINT", () => {
  console.log("Received SIGINT");
});
```

---

If you don’t know which signal to listen for, you listen to the umbrella `"exit"` event.

Copy

```
process.on("exit", code => {
  console.log(`Process exited with code ${code}`);
});
```

---

If you don’t know which signal to listen for, you listen to the [`"beforeExit"`](https://nodejs.org/api/process.html#event-beforeexit) and [`"exit"`](https://nodejs.org/api/process.html#event-exit) events.

Copy

```
process.on("beforeExit", code => {
  console.log(`Event loop is empty!`);
});

process.on("exit", code => {
  console.log(`Process is exiting with code ${code}`);
});
```

---

See [Docs > API > Utils](https://bun.com/docs/runtime/utils) for more useful utilities.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/process/os-signals.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/process/os-signals)

⌘I