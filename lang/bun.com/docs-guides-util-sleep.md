---
url: https://bun.com/docs/guides/util/sleep
title: Sleep for a fixed number of milliseconds - Bun
source_domain: bun.com
---

# Sleep for a fixed number of milliseconds - Bun

The `Bun.sleep` method provides a convenient way to create a void `Promise` that resolves in a fixed number of milliseconds.

Copy

```
// sleep for 1 second
await Bun.sleep(1000);
```

---

Internally, this is equivalent to the following snippet that uses [`setTimeout`](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout).

Copy

```
await new Promise(resolve => setTimeout(resolve, ms));
```

---

See [Docs > API > Utils](https://bun.com/docs/runtime/utils) for more useful utilities.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/util/sleep.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/util/sleep)

⌘I