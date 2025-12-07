---
url: https://bun.com/docs/guides/test/bail
title: Bail early with the Bun test runner - Bun
source_domain: bun.com
---

# Bail early with the Bun test runner - Bun

Use the `--bail` flag to bail on a test run after a single failure. This is useful for aborting as soon as possible in a continuous integration environment.

terminal

Copy

```
bun test --bail
```

---

To bail after a certain threshold of failures, optionally specify a number after the flag.

terminal

Copy

```
# bail after 10 failures
bun test --bail=10
```

---

See [Docs > Test runner](https://bun.com/docs/test) for complete documentation of `bun test`.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/test/bail.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/test/bail)

⌘I