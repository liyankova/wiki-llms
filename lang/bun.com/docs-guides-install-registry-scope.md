---
url: https://bun.com/docs/guides/install/registry-scope
title: Configure a private registry for an organization scope with bun install - Bun
source_domain: bun.com
---

# Configure a private registry for an organization scope with bun install - Bun

Private registries can be configured using either [`.npmrc`](https://bun.com/docs/pm/npmrc) or [`bunfig.toml`](https://bun.com/docs/runtime/bunfig#install-registry). While both are supported, we recommend using **bunfig.toml** for enhanced flexibility and Bun-specific options.
To configure a registry for a particular npm scope:

bunfig.toml

Copy

```
[install.scopes]
# as a string
"@myorg1" = "https://usertitle:[email protected]/"

# as an object with username/password
# you can reference environment variables
"@myorg2" = {
  username = "myusername",
  password = "$npm_pass",
  url = "https://registry.myorg.com/"
}

# as an object with token
"@myorg3" = { token = "$npm_token", url = "https://registry.myorg.com/" }
```

---

Your `bunfig.toml` can reference environment variables. Bun automatically loads environment variables from `.env.local`, `.env.[NODE_ENV]`, and `.env`. See [Docs > Environment variables](https://bun.com/docs/runtime/environment-variables) for more information.

bunfig.toml

Copy

```
[install.scopes]
"@myorg3" = { token = "$npm_token", url = "https://registry.myorg.com/" }
```

---

See [Docs > Package manager](https://bun.com/docs/pm/cli/install) for complete documentation of Bun’s package manager.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/install/registry-scope.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/install/registry-scope)

⌘I