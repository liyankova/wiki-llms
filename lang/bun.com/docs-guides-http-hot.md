---
url: https://bun.com/docs/guides/http/hot
title: Hot reload an HTTP server - Bun
source_domain: bun.com
---

# Hot reload an HTTP server - Bun

Bun supports the [`--hot`](https://bun.com/docs/runtime/watch-mode#hot-mode) flag to run a file with hot reloading enabled. When any module or file changes, Bun re-runs the file.

terminal

Copy

```
bun --hot run index.ts
```

---

Bun detects when you are running an HTTP server with `Bun.serve()`. It reloads your fetch handler when source files change, *without* restarting the `bun` process. This makes hot reloads nearly instantaneous.

Note that this doesn’t reload the page on your browser.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
Bun.serve({
  port: 3000,
  fetch(req) {
    return new Response("Hello world");
  },
});
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/http/hot.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/http/hot)

⌘I