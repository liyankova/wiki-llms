---
url: https://bun.com/docs/guides/runtime/tsconfig-paths
title: Re-map import paths - Bun
source_domain: bun.com
---

# Re-map import paths - Bun

Bun reads the `paths` field in your `tsconfig.json` to re-write import paths. This is useful for aliasing package names or avoiding long relative paths.

tsconfig.json

Copy

```
{
  "compilerOptions": {
    "paths": {
      "my-custom-name": ["zod"],
      "@components/*": ["./src/components/*"]
    }
  }
}
```

---

With the above `tsconfig.json`, the following imports will be re-written:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)tsconfig.ts

Copy

```
import { z } from "my-custom-name"; // imports from "zod"
import { Button } from "@components/Button"; // imports from "./src/components/Button"
```

---

See [Docs > Runtime > TypeScript](https://bun.com/docs/runtime/typescript) for more information on using TypeScript with Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/runtime/tsconfig-paths.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/runtime/tsconfig-paths)

⌘I