---
url: https://bun.com/docs/guides/install/custom-registry
title: Override the default npm registry for bun install - Bun
source_domain: bun.com
---

# Override the default npm registry for bun install - Bun

The default registry is `registry.npmjs.org`. This can be globally configured in `bunfig.toml`.

bunfig.toml

Copy

```
[install]
# set default registry as a string
registry = "https://registry.npmjs.org"

# if needed, set a token
registry = { url = "https://registry.npmjs.org", token = "123456" }

# if needed, set a username/password
registry = "https://usertitle:[email protected]"
```

---

Your `bunfig.toml` can reference environment variables. Bun automatically loads environment variables from `.env.local`, `.env.[NODE_ENV]`, and `.env`. See [Docs > Environment variables](https://bun.com/docs/runtime/environment-variables) for more information.

bunfig.toml

Copy

```
[install]
registry = { url = "https://registry.npmjs.org", token = "$npm_token" }
```

---

See [Docs > Package manager](https://bun.com/docs/pm/cli/install) for complete documentation of Bun’s package manager.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/install/custom-registry.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/install/custom-registry)

⌘I