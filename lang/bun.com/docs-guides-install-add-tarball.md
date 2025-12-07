---
url: https://bun.com/docs/guides/install/add-tarball
title: Add a tarball dependency - Bun
source_domain: bun.com
---

# Add a tarball dependency - Bun

Bun’s package manager can install any publicly available tarball URL as a dependency of your project.

terminal

Copy

```
bun add zod@https://registry.npmjs.org/zod/-/zod-3.21.4.tgz
```

---

Running this command will download, extract, and install the tarball to your project’s `node_modules` directory. It will also add the following line to your `package.json`:

package.json

Copy

```
{
  "dependencies": {
    "zod": "https://registry.npmjs.org/zod/-/zod-3.21.4.tgz"
  }
}
```

---

The package `"zod"` can now be imported as usual.

Copy

```
import { z } from "zod";
```

---

See [Docs > Package manager](https://bun.com/docs/pm/cli/install) for complete documentation of Bun’s package manager.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/install/add-tarball.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/install/add-tarball)

⌘I