---
url: https://bun.com/docs/pm/cli/remove
title: bun remove - Bun
source_domain: bun.com
---

# bun remove - Bun

## [​](https://bun.com/docs/pm/cli/remove#basic-usage) Basic Usage

terminal

Copy

```
bun remove ts-node
```

---

## [​](https://bun.com/docs/pm/cli/remove#cli-usage) CLI Usage

terminal

Copy

```
bun remove <package>
```

### [​](https://bun.com/docs/pm/cli/remove#general-information) General Information

[​](https://bun.com/docs/pm/cli/remove#param-help)

--help

boolean

Print this help menu. Alias: `-h`

### [​](https://bun.com/docs/pm/cli/remove#configuration) Configuration

[​](https://bun.com/docs/pm/cli/remove#param-config)

--config

string

Specify path to config file (`bunfig.toml`). Alias: `-c`

### [​](https://bun.com/docs/pm/cli/remove#package-json-interaction) Package.json Interaction

[​](https://bun.com/docs/pm/cli/remove#param-no-save)

--no-save

boolean

Don’t update `package.json` or save a lockfile

[​](https://bun.com/docs/pm/cli/remove#param-save)

--save

boolean

default:"true"

Save to `package.json` (true by default)

[​](https://bun.com/docs/pm/cli/remove#param-trust)

--trust

boolean

Add to `trustedDependencies` in the project’s `package.json` and install the package(s)

### [​](https://bun.com/docs/pm/cli/remove#lockfile-behavior) Lockfile Behavior

[​](https://bun.com/docs/pm/cli/remove#param-yarn)

--yarn

boolean

Write a `yarn.lock` file (yarn v1). Alias: `-y`

[​](https://bun.com/docs/pm/cli/remove#param-frozen-lockfile)

--frozen-lockfile

boolean

Disallow changes to lockfile

[​](https://bun.com/docs/pm/cli/remove#param-save-text-lockfile)

--save-text-lockfile

boolean

Save a text-based lockfile

[​](https://bun.com/docs/pm/cli/remove#param-lockfile-only)

--lockfile-only

boolean

Generate a lockfile without installing dependencies

### [​](https://bun.com/docs/pm/cli/remove#dependency-filtering) Dependency Filtering

[​](https://bun.com/docs/pm/cli/remove#param-production)

--production

boolean

Don’t install devDependencies. Alias: `-p`

[​](https://bun.com/docs/pm/cli/remove#param-omit)

--omit

string

Exclude `dev`, `optional`, or `peer` dependencies from install

### [​](https://bun.com/docs/pm/cli/remove#network-&-registry) Network & Registry

[​](https://bun.com/docs/pm/cli/remove#param-ca)

--ca

string

Provide a Certificate Authority signing certificate

[​](https://bun.com/docs/pm/cli/remove#param-cafile)

--cafile

string

Same as `—ca`, but as a file path to the certificate

[​](https://bun.com/docs/pm/cli/remove#param-registry)

--registry

string

Use a specific registry by default, overriding `.npmrc`, `bunfig.toml` and environment variables

### [​](https://bun.com/docs/pm/cli/remove#execution-control-&-validation) Execution Control & Validation

[​](https://bun.com/docs/pm/cli/remove#param-dry-run)

--dry-run

boolean

Don’t install anything

[​](https://bun.com/docs/pm/cli/remove#param-force)

--force

boolean

Always request the latest versions from the registry & reinstall all dependencies. Alias: `-f`

[​](https://bun.com/docs/pm/cli/remove#param-no-verify)

--no-verify

boolean

Skip verifying integrity of newly downloaded packages

### [​](https://bun.com/docs/pm/cli/remove#output-&-logging) Output & Logging

[​](https://bun.com/docs/pm/cli/remove#param-silent)

--silent

boolean

Don’t log anything

[​](https://bun.com/docs/pm/cli/remove#param-verbose)

--verbose

boolean

Excessively verbose logging

[​](https://bun.com/docs/pm/cli/remove#param-no-progress)

--no-progress

boolean

Disable the progress bar

[​](https://bun.com/docs/pm/cli/remove#param-no-summary)

--no-summary

boolean

Don’t print a summary

### [​](https://bun.com/docs/pm/cli/remove#caching) Caching

[​](https://bun.com/docs/pm/cli/remove#param-cache-dir)

--cache-dir

string

Store & load cached data from a specific directory path

[​](https://bun.com/docs/pm/cli/remove#param-no-cache)

--no-cache

boolean

Ignore manifest cache entirely

### [​](https://bun.com/docs/pm/cli/remove#script-execution) Script Execution

[​](https://bun.com/docs/pm/cli/remove#param-ignore-scripts)

--ignore-scripts

boolean

Skip lifecycle scripts in the project’s `package.json` (dependency scripts are never run)

[​](https://bun.com/docs/pm/cli/remove#param-concurrent-scripts)

--concurrent-scripts

number

default:"5"

Maximum number of concurrent jobs for lifecycle scripts (default 5)

### [​](https://bun.com/docs/pm/cli/remove#scope-&-path) Scope & Path

[​](https://bun.com/docs/pm/cli/remove#param-global)

--global

boolean

Install globally. Alias: `-g`

[​](https://bun.com/docs/pm/cli/remove#param-cwd)

--cwd

string

Set a specific cwd

### [​](https://bun.com/docs/pm/cli/remove#advanced-&-performance) Advanced & Performance

[​](https://bun.com/docs/pm/cli/remove#param-backend)

--backend

string

default:"clonefile"

Platform-specific optimizations for installing dependencies. Possible values: `clonefile` (default),
`hardlink`, `symlink`, `copyfile`

[​](https://bun.com/docs/pm/cli/remove#param-network-concurrency)

--network-concurrency

number

default:"48"

Maximum number of concurrent network requests (default 48)

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/pm/cli/remove.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /pm/cli/remove)

⌘I