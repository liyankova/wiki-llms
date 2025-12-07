---
url: https://bun.com/docs/guides/runtime/delete-directory
title: Delete directories - Bun
source_domain: bun.com
---

# Delete directories - Bun

To recursively delete a directory and all its contents, use `rm` from `node:fs/promises`. This is like running `rm -rf` in JavaScript.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)delete-directory.ts

Copy

```
import { rm } from "node:fs/promises";

// Delete a directory and all its contents
await rm("path/to/directory", { recursive: true, force: true });
```

---

These options configure the deletion behavior:

* `recursive: true` - Delete subdirectories and their contents
* `force: true` - Don’t throw errors if the directory doesn’t exist

You can also use it without `force` to ensure the directory exists:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)delete-directory.ts

Copy

```
try {
  await rm("path/to/directory", { recursive: true });
} catch (error) {
  if (error.code === "ENOENT") {
    console.log("Directory doesn't exist");
  } else {
    throw error;
  }
}
```

---

See [Docs > API > FileSystem](https://bun.com/docs/runtime/file-io) for more filesystem operations.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/runtime/delete-directory.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/runtime/delete-directory)

⌘I