---
url: https://bun.com/docs/guides/install/add-optional
title: Add an optional dependency - Bun
source_domain: bun.com
---

# Add an optional dependency - Bun

To add an npm package as an optional dependency, use the `--optional` flag.

terminal

Copy

```
bun add zod --optional
```

---

This will add the package to `optionalDependencies` in `package.json`.

package.json

Copy

```
{
  "optionalDependencies": {
    "zod": "^3.0.0"
  }
}
```

---

See [Docs > Package manager](https://bun.com/docs/pm/cli/install) for complete documentation of Bun’s package manager.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/install/add-optional.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/install/add-optional)

⌘I