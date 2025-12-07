---
url: https://bun.com/docs/pm/npmrc
title: .npmrc support - Bun
source_domain: bun.com
---

# .npmrc support - Bun

Bun supports loading configuration options from [`.npmrc`](https://docs.npmjs.com/cli/v10/configuring-npm/npmrc) files, allowing you to reuse existing registry/scope configurations.

We recommend migrating your `.npmrc` file to Bun’s [`bunfig.toml`](https://bun.com/docs/runtime/bunfig) format, as it provides more
flexible options and can let you configure Bun-specific options.

---

## [​](https://bun.com/docs/pm/npmrc#supported-options) Supported options

### [​](https://bun.com/docs/pm/npmrc#set-the-default-registry) Set the default registry

The default registry is used to resolve packages, its default value is `npm`’s official registry (`https://registry.npmjs.org/`).
To change it, you can set the `registry` option in `.npmrc`:

.npmrc

Copy

```
registry=http://localhost:4873/
```

The equivalent `bunfig.toml` option is [`install.registry`](https://bun.com/docs/runtime/bunfig#install-registry):

bunfig.toml

Copy

```
install.registry = "http://localhost:4873/"
```

### [​](https://bun.com/docs/pm/npmrc#set-the-registry-for-a-specific-scope) Set the registry for a specific scope

`@<scope>:registry` allows you to set the registry for a specific scope:

.npmrc

Copy

```
@myorg:registry=http://localhost:4873/
```

The equivalent `bunfig.toml` option is to add a key in [`install.scopes`](https://bun.com/docs/runtime/bunfig#install-registry):

bunfig.toml

Copy

```
[install.scopes]
myorg = "http://localhost:4873/"
```

### [​](https://bun.com/docs/pm/npmrc#configure-options-for-a-specific-registry) Configure options for a specific registry

`//<registry_url>/:<key>=<value>` allows you to set options for a specific registry:

.npmrc

Copy

```
# set an auth token for the registry
# ${...} is a placeholder for environment variables
//http://localhost:4873/:_authToken=${NPM_TOKEN}

# or you could set a username and password
# note that the password is base64 encoded
//http://localhost:4873/:username=myusername

//http://localhost:4873/:_password=${NPM_PASSWORD}

# or use _auth, which is your username and password
# combined into a single string, which is then base 64 encoded
//http://localhost:4873/:_auth=${NPM_AUTH}
```

The following options are supported:

* `_authToken`
* `username`
* `_password` (base64 encoded password)
* `_auth` (base64 encoded username:password, e.g. `btoa(username + ":" + password)`)

The equivalent `bunfig.toml` option is to add a key in [`install.scopes`](https://bun.com/docs/runtime/bunfig#install-registry):

bunfig.toml

Copy

```
[install.scopes]
myorg = { url = "http://localhost:4873/", username = "myusername", password = "$NPM_PASSWORD" }
```

### [​](https://bun.com/docs/pm/npmrc#link-workspace-packages:-control-workspace-package-installation) `link-workspace-packages`: Control workspace package installation

Controls how workspace packages are installed when available locally:

.npmrc

Copy

```
link-workspace-packages=true
```

The equivalent `bunfig.toml` option is [`install.linkWorkspacePackages`](https://bun.com/docs/runtime/bunfig#install-linkworkspacepackages):

bunfig.toml

Copy

```
[install]
linkWorkspacePackages = true
```

### [​](https://bun.com/docs/pm/npmrc#save-exact:-save-exact-versions) `save-exact`: Save exact versions

Always saves exact versions without the `^` prefix:

.npmrc

Copy

```
save-exact=true
```

The equivalent `bunfig.toml` option is [`install.exact`](https://bun.com/docs/runtime/bunfig#install-exact):

bunfig.toml

Copy

```
[install]
exact = true
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/pm/npmrc.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /pm/npmrc)

⌘I