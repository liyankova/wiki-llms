---
url: https://bun.com/docs/guides/install/add-peer
title: Add a peer dependency - Bun
source_domain: bun.com
---

# Add a peer dependency - Bun

To add an npm package as a peer dependency, use the `--peer` flag.

terminal

Copy

```
bun add @types/bun --peer
```

---

This will add the package to `peerDependencies` in `package.json`.

package.json

Copy

```
{
  "peerDependencies": {
    "@types/bun": "^1.3.3"
  }
}
```

---

Running `bun install` will install peer dependencies by default, unless marked optional in `peerDependenciesMeta`.

package.json

Copy

```
{
  "peerDependencies": {
    "@types/bun": "^1.3.3"
  },
  "peerDependenciesMeta": {
    "@types/bun": { 
      "optional": true
    } 
  }
}
```

---

See [Docs > Package manager](https://bun.com/docs/pm/cli/install) for complete documentation of Bun’s package manager.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/install/add-peer.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/install/add-peer)

⌘I