---
url: https://bun.com/docs/pm/cli/link
title: bun link - Bun
source_domain: bun.com
---

# bun link - Bun

Use `bun link` in a local directory to register the current package as a “linkable” package.

terminal

Copy

```
cd /path/to/cool-pkg
cat package.json
bun link
```

Copy

```
bun link v1.3.3 (7416672e)
Success! Registered "cool-pkg"

To use cool-pkg in a project, run:
  bun link cool-pkg

Or add it in dependencies in your package.json file:
  "cool-pkg": "link:cool-pkg"
```

This package can now be “linked” into other projects using `bun link cool-pkg`. This will create a symlink in the `node_modules` directory of the target project, pointing to the local directory.

terminal

Copy

```
cd /path/to/my-app
bun link cool-pkg
```

In addition, the `--save` flag can be used to add `cool-pkg` to the `dependencies` field of your app’s package.json with a special version specifier that tells Bun to load from the registered local directory instead of installing from `npm`:

package.json

Copy

```
{
  "name": "my-app",
  "version": "1.0.0",
  "dependencies": {
    "cool-pkg": "link:cool-pkg"
  }
}
```

## [​](https://bun.com/docs/pm/cli/link#unlinking) Unlinking

Use `bun unlink` in the root directory to unregister a local package.

terminal

Copy

```
cd /path/to/cool-pkg
bun unlink
```

Copy

```
bun unlink v1.3.3 (7416672e)
```

---

# [​](https://bun.com/docs/pm/cli/link#cli-usage) CLI Usage

Copy

```
bun link <packages>
```

### [​](https://bun.com/docs/pm/cli/link#installation-scope) Installation Scope

[​](https://bun.com/docs/pm/cli/link#param-global)

--global

boolean

Install globally. Alias: `-g`

### [​](https://bun.com/docs/pm/cli/link#dependency-management) Dependency Management

[​](https://bun.com/docs/pm/cli/link#param-production)

--production

boolean

Don’t install devDependencies. Alias: `-p`

[​](https://bun.com/docs/pm/cli/link#param-omit)

--omit

string

Exclude `dev`, `optional`, or `peer` dependencies from install

### [​](https://bun.com/docs/pm/cli/link#project-files-&-lockfiles) Project Files & Lockfiles

[​](https://bun.com/docs/pm/cli/link#param-yarn)

--yarn

boolean

Write a `yarn.lock` file (yarn v1). Alias: `-y`

[​](https://bun.com/docs/pm/cli/link#param-frozen-lockfile)

--frozen-lockfile

boolean

Disallow changes to lockfile

[​](https://bun.com/docs/pm/cli/link#param-save-text-lockfile)

--save-text-lockfile

boolean

Save a text-based lockfile

[​](https://bun.com/docs/pm/cli/link#param-lockfile-only)

--lockfile-only

boolean

Generate a lockfile without installing dependencies

[​](https://bun.com/docs/pm/cli/link#param-no-save)

--no-save

boolean

Don’t update `package.json` or save a lockfile

[​](https://bun.com/docs/pm/cli/link#param-save)

--save

boolean

default:"true"

Save to `package.json` (true by default)

[​](https://bun.com/docs/pm/cli/link#param-trust)

--trust

boolean

Add to `trustedDependencies` in the project’s `package.json` and install the package(s)

### [​](https://bun.com/docs/pm/cli/link#installation-control) Installation Control

[​](https://bun.com/docs/pm/cli/link#param-force)

--force

boolean

Always request the latest versions from the registry & reinstall all dependencies. Alias: `-f`

[​](https://bun.com/docs/pm/cli/link#param-no-verify)

--no-verify

boolean

Skip verifying integrity of newly downloaded packages

[​](https://bun.com/docs/pm/cli/link#param-backend)

--backend

string

default:"clonefile"

Platform-specific optimizations for installing dependencies. Possible values: `clonefile` (default),
`hardlink`, `symlink`, `copyfile`

[​](https://bun.com/docs/pm/cli/link#param-linker)

--linker

string

Linker strategy (one of `isolated` or `hoisted`)

[​](https://bun.com/docs/pm/cli/link#param-dry-run)

--dry-run

boolean

Don’t install anything

[​](https://bun.com/docs/pm/cli/link#param-ignore-scripts)

--ignore-scripts

boolean

Skip lifecycle scripts in the project’s `package.json` (dependency scripts are never run)

### [​](https://bun.com/docs/pm/cli/link#network-&-registry) Network & Registry

[​](https://bun.com/docs/pm/cli/link#param-ca)

--ca

string

Provide a Certificate Authority signing certificate

[​](https://bun.com/docs/pm/cli/link#param-cafile)

--cafile

string

Same as `—ca`, but as a file path to the certificate

[​](https://bun.com/docs/pm/cli/link#param-registry)

--registry

string

Use a specific registry by default, overriding `.npmrc`, `bunfig.toml`, and environment
variables

[​](https://bun.com/docs/pm/cli/link#param-network-concurrency)

--network-concurrency

number

default:"48"

Maximum number of concurrent network requests (default 48)

### [​](https://bun.com/docs/pm/cli/link#performance-&-resource) Performance & Resource

[​](https://bun.com/docs/pm/cli/link#param-concurrent-scripts)

--concurrent-scripts

number

default:"5"

Maximum number of concurrent jobs for lifecycle scripts (default 5)

### [​](https://bun.com/docs/pm/cli/link#caching) Caching

[​](https://bun.com/docs/pm/cli/link#param-cache-dir)

--cache-dir

string

Store & load cached data from a specific directory path

[​](https://bun.com/docs/pm/cli/link#param-no-cache)

--no-cache

boolean

Ignore manifest cache entirely

### [​](https://bun.com/docs/pm/cli/link#output-&-logging) Output & Logging

[​](https://bun.com/docs/pm/cli/link#param-silent)

--silent

boolean

Don’t log anything

[​](https://bun.com/docs/pm/cli/link#param-quiet)

--quiet

boolean

Only show tarball name when packing

[​](https://bun.com/docs/pm/cli/link#param-verbose)

--verbose

boolean

Excessively verbose logging

[​](https://bun.com/docs/pm/cli/link#param-no-progress)

--no-progress

boolean

Disable the progress bar

[​](https://bun.com/docs/pm/cli/link#param-no-summary)

--no-summary

boolean

Don’t print a summary

### [​](https://bun.com/docs/pm/cli/link#platform-targeting) Platform Targeting

[​](https://bun.com/docs/pm/cli/link#param-cpu)

--cpu

string

Override CPU architecture for optional dependencies (e.g., `x64`, `arm64`, `*` for
all)

[​](https://bun.com/docs/pm/cli/link#param-os)

--os

string

Override operating system for optional dependencies (e.g., `linux`, `darwin`, `*` for
all)

### [​](https://bun.com/docs/pm/cli/link#global-configuration-&-context) Global Configuration & Context

[​](https://bun.com/docs/pm/cli/link#param-config)

--config

string

Specify path to config file (`bunfig.toml`). Alias: `-c`

[​](https://bun.com/docs/pm/cli/link#param-cwd)

--cwd

string

Set a specific current working directory

### [​](https://bun.com/docs/pm/cli/link#help) Help

[​](https://bun.com/docs/pm/cli/link#param-help)

--help

boolean

Print this help menu. Alias: `-h`

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/pm/cli/link.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /pm/cli/link)

⌘I