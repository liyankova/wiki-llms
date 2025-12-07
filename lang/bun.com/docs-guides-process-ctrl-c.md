---
url: https://bun.com/docs/guides/process/ctrl-c
title: Listen for CTRL+C - Bun
source_domain: bun.com
---

# Listen for CTRL+C - Bun

The `ctrl+c` shortcut sends an *interrupt signal* to the running process. This signal can be intercepted by listening for the `SIGINT` event. If you want to close the process, you must explicitly call `process.exit()`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)process.ts

Copy

```
process.on("SIGINT", () => {
  console.log("Ctrl-C was pressed");
  process.exit();
});
```

---

See [Docs > API > Utils](https://bun.com/docs/runtime/utils) for more useful utilities.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/process/ctrl-c.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/process/ctrl-c)

⌘I