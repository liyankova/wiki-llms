---
url: https://bun.com/docs/guides/read-file/exists
title: Check if a file exists - Bun
source_domain: bun.com
---

# Check if a file exists - Bun

The `Bun.file()` function accepts a path and returns a `BunFile` instance. Use the `.exists()` method to check if a file exists at the given path.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
const path = "/path/to/package.json";
const file = Bun.file(path);

await file.exists(); // boolean;
```

---

Refer to [API > File I/O](https://bun.com/docs/runtime/file-io) for more information on working with `BunFile`.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/read-file/exists.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/read-file/exists)

⌘I