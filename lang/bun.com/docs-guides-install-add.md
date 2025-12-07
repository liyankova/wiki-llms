---
url: https://bun.com/docs/guides/install/add
title: Add a dependency - Bun
source_domain: bun.com
---

# Add a dependency - Bun

To add an npm package as a dependency, use `bun add`.

terminal

Copy

```
bun add zod
```

---

This will add the package to `dependencies` in `package.json`. By default, the `^` range specifier will be used, to indicate that any future minor or patch versions are acceptable.

package.json

Copy

```
{
  "dependencies": {
    "zod": "^3.0.0"
  }
}
```

---

To “pin” to an exact version of the package, use `--exact`. This will add the package to `dependencies` without the `^`, pinning your project to the exact version you installed.

terminal

Copy

```
bun add zod --exact
```

---

To specify an exact version or a tag:

terminal

Copy

```
bun add [email protected]
bun add zod@next
```

---

See [Docs > Package manager](https://bun.com/docs/pm/cli/install) for complete documentation of Bun’s package manager.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/install/add.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/install/add)

⌘I