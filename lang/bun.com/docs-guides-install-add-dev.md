---
url: https://bun.com/docs/guides/install/add-dev
title: Add a development dependency - Bun
source_domain: bun.com
---

# Add a development dependency - Bun

To add an npm package as a development dependency, use `bun add --development`.

terminal

Copy

```
bun add zod --dev
bun add zod -d # shorthand
```

---

This will add the package to `devDependencies` in `package.json`.

Copy

```
{
  "devDependencies": {
    "zod": "^3.0.0"
  }
}
```

---

See [Docs > Package manager](https://bun.com/docs/pm/cli/install) for complete documentation of Bun’s package manager.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/install/add-dev.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/install/add-dev)

⌘I