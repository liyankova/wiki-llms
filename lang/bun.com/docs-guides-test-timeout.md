---
url: https://bun.com/docs/guides/test/timeout
title: Set a per-test timeout with the Bun test runner - Bun
source_domain: bun.com
---

# Set a per-test timeout with the Bun test runner - Bun

Use the `--timeout` flag to set a timeout for each test in milliseconds. If any test exceeds this timeout, it will be marked as failed.
The default timeout is `5000` (5 seconds).

terminal

Copy

```
bun test --timeout 3000 # 3 seconds
```

---

See [Docs > Test runner](https://bun.com/docs/test) for complete documentation of `bun test`.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/test/timeout.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/test/timeout)

⌘I