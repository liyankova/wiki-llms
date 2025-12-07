---
url: https://bun.com/docs/pm/cli/outdated
title: bun outdated - Bun
source_domain: bun.com
---

# bun outdated - Bun

Use `bun outdated` to check for outdated dependencies in your project. This command displays a table of dependencies that have newer versions available.

terminal

Copy

```
bun outdated
```

Copy

```
| Package                        | Current | Update    | Latest     |
| ------------------------------ | ------- | --------- | ---------- |
| @sinclair/typebox              | 0.34.15 | 0.34.16   | 0.34.16    |
| @types/bun (dev)               | 1.3.0   | 1.3.3     | 1.3.3      |
| eslint (dev)                   | 8.57.1  | 8.57.1    | 9.20.0     |
| eslint-plugin-security (dev)   | 2.1.1   | 2.1.1     | 3.0.1      |
| eslint-plugin-sonarjs (dev)    | 0.23.0  | 0.23.0    | 3.0.1      |
| expect-type (dev)              | 0.16.0  | 0.16.0    | 1.1.0      |
| prettier (dev)                 | 3.4.2   | 3.5.0     | 3.5.0      |
| tsup (dev)                     | 8.3.5   | 8.3.6     | 8.3.6      |
| typescript (dev)               | 5.7.2   | 5.7.3     | 5.7.3      |
```

## [​](https://bun.com/docs/pm/cli/outdated#version-information) Version Information

The output table shows three version columns:

* **Current**: The version currently installed
* **Update**: The latest version that satisfies your package.json version range
* **Latest**: The latest version published to the registry

### [​](https://bun.com/docs/pm/cli/outdated#dependency-filters) Dependency Filters

`bun outdated` supports searching for outdated dependencies by package names and glob patterns.
To check if specific dependencies are outdated, pass the package names as positional arguments:

terminal

Copy

```
bun outdated eslint-plugin-security eslint-plugin-sonarjs
```

Copy

```
| Package                        | Current | Update | Latest    |
| ------------------------------ | ------- | ------ | --------- |
| eslint-plugin-security (dev)   | 2.1.1   | 2.1.1  | 3.0.1     |
| eslint-plugin-sonarjs (dev)    | 0.23.0  | 0.23.0 | 3.0.1     |
```

You can also pass glob patterns to check for outdated packages:

terminal

Copy

```
bun outdated 'eslint*'
```

Copy

```
| Package                        | Current | Update | Latest     |
| ------------------------------ | ------- | ------ | ---------- |
| eslint (dev)                   | 8.57.1  | 8.57.1 | 9.20.0     |
| eslint-plugin-security (dev)   | 2.1.1   | 2.1.1  | 3.0.1      |
| eslint-plugin-sonarjs (dev)    | 0.23.0  | 0.23.0 | 3.0.1      |
```

For example, to check for outdated `@types/*` packages:

terminal

Copy

```
bun outdated '@types/*'
```

Copy

```
| Package            | Current | Update | Latest |
| ------------------ | ------- | ------ | ------ |
| @types/bun (dev)   | 1.3.0   | 1.3.3  | 1.3.3 |
```

Or to exclude all `@types/*` packages:

terminal

Copy

```
bun outdated '!@types/*'
```

Copy

```
| Package                        | Current | Update    | Latest     |
| ------------------------------ | ------- | --------- | ---------- |
| @sinclair/typebox              | 0.34.15 | 0.34.16   | 0.34.16    |
| eslint (dev)                   | 8.57.1  | 8.57.1    | 9.20.0     |
| eslint-plugin-security (dev)   | 2.1.1   | 2.1.1     | 3.0.1      |
| eslint-plugin-sonarjs (dev)    | 0.23.0  | 0.23.0    | 3.0.1      |
| expect-type (dev)              | 0.16.0  | 0.16.0    | 1.1.0      |
| prettier (dev)                 | 3.4.2   | 3.5.0     | 3.5.0      |
| tsup (dev)                     | 8.3.5   | 8.3.6     | 8.3.6      |
| typescript (dev)               | 5.7.2   | 5.7.3     | 5.7.3      |
```

### [​](https://bun.com/docs/pm/cli/outdated#workspace-filters) Workspace Filters

Use the `--filter` flag to check for outdated dependencies in a different workspace package:

terminal

Copy

```
bun outdated --filter='@monorepo/types'
```

Copy

```
| Package            | Current | Update | Latest |
| ------------------ | ------- | ------ | ------ |
| tsup (dev)         | 8.3.5   | 8.3.6  | 8.3.6  |
| typescript (dev)   | 5.7.2   | 5.7.3  | 5.7.3  |
```

You can pass multiple `--filter` flags to check multiple workspaces:

terminal

Copy

```
bun outdated --filter @monorepo/types --filter @monorepo/cli
```

Copy

```
| Package                        | Current | Update | Latest     |
| ------------------------------ | ------- | ------ | ---------- |
| eslint (dev)                 	 | 8.57.1  | 8.57.1 | 9.20.0     |
| eslint-plugin-security (dev)   | 2.1.1   | 2.1.1  | 3.0.1      |
| eslint-plugin-sonarjs (dev)    | 0.23.0  | 0.23.0 | 3.0.1      |
| expect-type (dev)              | 0.16.0  | 0.16.0 | 1.1.0      |
| tsup (dev)                     | 8.3.5   | 8.3.6  | 8.3.6      |
| typescript (dev)               | 5.7.2   | 5.7.3  | 5.7.3      |
```

You can also pass glob patterns to filter by workspace names:

terminal

Copy

```
bun outdated --filter='@monorepo/{types,cli}'
```

Copy

```
| Package                        | Current | Update | Latest     |
| ------------------------------ | ------- | ------ | ---------- |
| eslint (dev)                   | 8.57.1  | 8.57.1 | 9.20.0     |
| eslint-plugin-security (dev)   | 2.1.1   | 2.1.1  | 3.0.1      |
| eslint-plugin-sonarjs (dev)    | 0.23.0  | 0.23.0 | 3.0.1      |
| expect-type (dev)              | 0.16.0  | 0.16.0 | 1.1.0      |
| tsup (dev)                     | 8.3.5   | 8.3.6  | 8.3.6      |
| typescript (dev)               | 5.7.2   | 5.7.3  | 5.7.3      |
```

### [​](https://bun.com/docs/pm/cli/outdated#catalog-dependencies) Catalog Dependencies

`bun outdated` supports checking catalog dependencies defined in`package.json`:

terminal

Copy

```
bun outdated -r
```

Copy

```
┌────────────────────┬─────────┬─────────┬─────────┬────────────────────────────────┐
│ Package            │ Current │ Update  │ Latest  │ Workspace                      │
├────────────────────┼─────────┼─────────┼─────────┼────────────────────────────────┤
│ body-parser        │ 1.19.0  │ 1.19.0  │ 2.2.0   │ @test/shared                   │
├────────────────────┼─────────┼─────────┼─────────┼────────────────────────────────┤
│ cors               │ 2.8.0   │ 2.8.0   │ 2.8.5   │ @test/shared                   │
├────────────────────┼─────────┼─────────┼─────────┼────────────────────────────────┤
│ chalk              │ 4.0.0   │ 4.0.0   │ 5.6.2   │ @test/utils                    │
├────────────────────┼─────────┼─────────┼─────────┼────────────────────────────────┤
│ uuid               │ 8.0.0   │ 8.0.0   │ 13.0.0  │ @test/utils                    │
├────────────────────┼─────────┼─────────┼─────────┼────────────────────────────────┤
│ axios              │ 0.21.0  │ 0.21.0  │ 1.12.2  │ catalog (@test/app)            │
├────────────────────┼─────────┼─────────┼─────────┼────────────────────────────────┤
│ lodash             │ 4.17.15 │ 4.17.15 │ 4.17.21 │ catalog (@test/app, @test/app) │
├────────────────────┼─────────┼─────────┼─────────┼────────────────────────────────┤
│ react              │ 17.0.0  │ 17.0.0  │ 19.1.1  │ catalog (@test/app)            │
├────────────────────┼─────────┼─────────┼─────────┼────────────────────────────────┤
│ react-dom          │ 17.0.0  │ 17.0.0  │ 19.1.1  │ catalog (@test/app)            │
├────────────────────┼─────────┼─────────┼─────────┼────────────────────────────────┤
│ express            │ 4.17.0  │ 4.17.0  │ 5.1.0   │ catalog (@test/shared)         │
├────────────────────┼─────────┼─────────┼─────────┼────────────────────────────────┤
│ moment             │ 2.24.0  │ 2.24.0  │ 2.30.1  │ catalog (@test/utils)          │
├────────────────────┼─────────┼─────────┼─────────┼────────────────────────────────┤
│ @types/node (dev)  │ 14.0.0  │ 14.0.0  │ 24.5.2  │ @test/shared                   │
├────────────────────┼─────────┼─────────┼─────────┼────────────────────────────────┤
│ @types/react (dev) │ 17.0.0  │ 17.0.0  │ 19.1.15 │ catalog:testing (@test/app)    │
├────────────────────┼─────────┼─────────┼─────────┼────────────────────────────────┤
│ eslint (dev)       │ 7.0.0   │ 7.0.0   │ 9.36.0  │ catalog:testing (@test/app)    │
├────────────────────┼─────────┼─────────┼─────────┼────────────────────────────────┤
│ typescript (dev)   │ 4.9.5   │ 4.9.5   │ 5.9.2   │ catalog:build (@test/app)      │
├────────────────────┼─────────┼─────────┼─────────┼────────────────────────────────┤
│ jest (dev)         │ 26.0.0  │ 26.0.0  │ 30.2.0  │ catalog:testing (@test/shared) │
├────────────────────┼─────────┼─────────┼─────────┼────────────────────────────────┤
│ prettier (dev)     │ 2.0.0   │ 2.0.0   │ 3.6.2   │ catalog:build (@test/utils)    │
└────────────────────┴─────────┴─────────┴─────────┴────────────────────────────────┘
```

---

## [​](https://bun.com/docs/pm/cli/outdated#cli-usage) CLI Usage

terminal

Copy

```
bun outdated <filter>
```

### [​](https://bun.com/docs/pm/cli/outdated#general-options) General Options

[​](https://bun.com/docs/pm/cli/outdated#param-c-config)

-c, --config

string

Specify path to config file (`bunfig.toml`)

[​](https://bun.com/docs/pm/cli/outdated#param-cwd)

--cwd

string

Set a specific cwd

[​](https://bun.com/docs/pm/cli/outdated#param-h-help)

-h, --help

boolean

Print this help menu

[​](https://bun.com/docs/pm/cli/outdated#param-f-filter)

-F, --filter

string

Display outdated dependencies for each matching workspace

### [​](https://bun.com/docs/pm/cli/outdated#output-&-logging) Output & Logging

[​](https://bun.com/docs/pm/cli/outdated#param-silent)

--silent

boolean

Don’t log anything

[​](https://bun.com/docs/pm/cli/outdated#param-verbose)

--verbose

boolean

Excessively verbose logging

[​](https://bun.com/docs/pm/cli/outdated#param-no-progress)

--no-progress

boolean

Disable the progress bar

[​](https://bun.com/docs/pm/cli/outdated#param-no-summary)

--no-summary

boolean

Don’t print a summary

### [​](https://bun.com/docs/pm/cli/outdated#dependency-scope-&-target) Dependency Scope & Target

[​](https://bun.com/docs/pm/cli/outdated#param-p-production)

-p, --production

boolean

Don’t install devDependencies

[​](https://bun.com/docs/pm/cli/outdated#param-omit)

--omit

string

Exclude `dev`, `optional`, or `peer` dependencies from install

[​](https://bun.com/docs/pm/cli/outdated#param-g-global)

-g, --global

boolean

Install globally

### [​](https://bun.com/docs/pm/cli/outdated#lockfile-&-package-json) Lockfile & Package.json

[​](https://bun.com/docs/pm/cli/outdated#param-y-yarn)

-y, --yarn

boolean

Write a `yarn.lock` file (yarn v1)

[​](https://bun.com/docs/pm/cli/outdated#param-no-save)

--no-save

boolean

Don’t update `package.json` or save a lockfile

[​](https://bun.com/docs/pm/cli/outdated#param-save)

--save

boolean

default:"true"

Save to `package.json` (true by default)

[​](https://bun.com/docs/pm/cli/outdated#param-frozen-lockfile)

--frozen-lockfile

boolean

Disallow changes to lockfile

[​](https://bun.com/docs/pm/cli/outdated#param-save-text-lockfile)

--save-text-lockfile

boolean

Save a text-based lockfile

[​](https://bun.com/docs/pm/cli/outdated#param-lockfile-only)

--lockfile-only

boolean

Generate a lockfile without installing dependencies

[​](https://bun.com/docs/pm/cli/outdated#param-trust)

--trust

boolean

Add to `trustedDependencies` in the project’s `package.json` and install the package(s)

### [​](https://bun.com/docs/pm/cli/outdated#network-&-registry) Network & Registry

[​](https://bun.com/docs/pm/cli/outdated#param-ca)

--ca

string

Provide a Certificate Authority signing certificate

[​](https://bun.com/docs/pm/cli/outdated#param-cafile)

--cafile

string

Same as `—ca`, but as a file path to the certificate

[​](https://bun.com/docs/pm/cli/outdated#param-registry)

--registry

string

Use a specific registry by default, overriding `.npmrc`, `bunfig.toml` and environment variables

[​](https://bun.com/docs/pm/cli/outdated#param-network-concurrency)

--network-concurrency

number

default:"48"

Maximum number of concurrent network requests (default 48)

### [​](https://bun.com/docs/pm/cli/outdated#caching) Caching

[​](https://bun.com/docs/pm/cli/outdated#param-cache-dir)

--cache-dir

string

Store & load cached data from a specific directory path

[​](https://bun.com/docs/pm/cli/outdated#param-no-cache)

--no-cache

boolean

Ignore manifest cache entirely

### [​](https://bun.com/docs/pm/cli/outdated#execution-behavior) Execution Behavior

[​](https://bun.com/docs/pm/cli/outdated#param-dry-run)

--dry-run

boolean

Don’t install anything

[​](https://bun.com/docs/pm/cli/outdated#param-f-force)

-f, --force

boolean

Always request the latest versions from the registry & reinstall all dependencies

[​](https://bun.com/docs/pm/cli/outdated#param-no-verify)

--no-verify

boolean

Skip verifying integrity of newly downloaded packages

[​](https://bun.com/docs/pm/cli/outdated#param-ignore-scripts)

--ignore-scripts

boolean

Skip lifecycle scripts in the project’s `package.json` (dependency scripts are never run)

[​](https://bun.com/docs/pm/cli/outdated#param-backend)

--backend

string

default:"clonefile"

Platform-specific optimizations for installing dependencies. Possible values: `clonefile` (default),
`hardlink`, `symlink`, `copyfile`

[​](https://bun.com/docs/pm/cli/outdated#param-concurrent-scripts)

--concurrent-scripts

number

default:"5"

Maximum number of concurrent jobs for lifecycle scripts (default 5)

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/pm/cli/outdated.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /pm/cli/outdated)

⌘I