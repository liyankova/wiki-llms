---
url: https://bun.com/docs/guides/install/npm-alias
title: Install a package under a different name - Bun
source_domain: bun.com
---

# Install a package under a different name - Bun

To install an npm package under an alias:

terminal

Copy

```
bun add my-custom-name@npm:zod
```

---

The `zod` package can now be imported as `my-custom-name`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
import { z } from "my-custom-name";

z.string();
```

---

See [Docs > Package manager](https://bun.com/docs/pm/cli/install) for complete documentation of Bun’s package manager.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/install/npm-alias.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/install/npm-alias)

⌘I