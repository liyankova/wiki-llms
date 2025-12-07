---
url: https://bun.com/docs/guides/install/add-git
title: Add a Git dependency - Bun
source_domain: bun.com
---

# Add a Git dependency - Bun

Bun supports directly adding GitHub repositories as dependencies of your project.

terminal

Copy

```
bun add github:lodash/lodash
```

---

This will add the following line to your `package.json`:

package.json

Copy

```
{
  "dependencies": {
    "lodash": "github:lodash/lodash"
  }
}
```

---

Bun supports a number of protocols for specifying Git dependencies.

terminal

Copy

```
bun add git+https://github.com/lodash/lodash.git
bun add git+ssh://github.com/lodash/lodash.git#4.17.21
bun add [email protected]:lodash/lodash.git
bun add github:colinhacks/zod
```

**Note:** GitHub dependencies download via HTTP tarball when possible for faster installation.

---

See [Docs > Package manager](https://bun.com/docs/pm/cli/install) for complete documentation of Bun’s package manager.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/install/add-git.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/install/add-git)

⌘I