---
url: https://bun.com/docs/pm/scopes-registries
title: Scopes and registries - Bun
source_domain: bun.com
---

# Scopes and registries - Bun

The default registry is `registry.npmjs.org`. This can be globally configured in `bunfig.toml`:

bunfig.toml

Copy

```
[install]
# set default registry as a string
registry = "https://registry.npmjs.org"
# set a token
registry = { url = "https://registry.npmjs.org", token = "123456" }
# set a username/password
registry = "https://username:[email protected]"
```

To configure a private registry scoped to a particular organization:

bunfig.toml

Copy

```
[install.scopes]
# registry as string
"@myorg1" = "https://username:[email protected]/"

# registry with username/password
# you can reference environment variables
"@myorg2" = { username = "myusername", password = "$NPM_PASS", url = "https://registry.myorg.com/" }

# registry with token
"@myorg3" = { token = "$npm_token", url = "https://registry.myorg.com/" }
```

### [​](https://bun.com/docs/pm/scopes-registries#npmrc) `.npmrc`

Bun also reads `.npmrc` files, [learn more](https://bun.com/docs/pm/npmrc).

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/pm/scopes-registries.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /pm/scopes-registries)

⌘I