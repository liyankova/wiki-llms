---
url: https://bun.com/docs/guides/util/which-path-to-executable-bin
title: Get the path to an executable bin file - Bun
source_domain: bun.com
---

# Get the path to an executable bin file - Bun

`Bun.which` is a utility function to find the absolute path of an executable file. It is similar to the `which` command in Unix-like systems.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)foo.ts

Copy

```
Bun.which("sh"); // => "/bin/sh"
Bun.which("notfound"); // => null
Bun.which("bun"); // => "/home/user/.bun/bin/bun"
```

---

See [Docs > API > Utils](https://bun.com/docs/runtime/utils#bun-which) for complete documentation.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/util/which-path-to-executable-bin.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/util/which-path-to-executable-bin)

⌘I