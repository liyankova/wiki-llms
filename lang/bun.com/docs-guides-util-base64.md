---
url: https://bun.com/docs/guides/util/base64
title: Encode and decode base64 strings - Bun
source_domain: bun.com
---

# Encode and decode base64 strings - Bun

Bun implements the Web-standard [`atob`](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/atob) and [`btoa`](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/btoa) functions for encoding and decoding base64 strings.

Copy

```
const data = "hello world";
const encoded = btoa(data); // => "aGVsbG8gd29ybGQ="
const decoded = atob(encoded); // => "hello world"
```

---

See [Docs > Web APIs](https://bun.com/docs/runtime/web-apis) for a complete breakdown of the Web APIs implemented in Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/util/base64.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/util/base64)

⌘I