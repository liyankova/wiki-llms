---
url: https://bun.com/docs/pm/cli/update
title: bun update - Bun
source_domain: bun.com
---

# bun update - Bun

To upgrade your Bun CLI version, see [`bun upgrade`](https://bun.com/docs/installation#upgrading).

To update all dependencies to the latest version:

terminal

Copy

```
bun update
```

To update a specific dependency to the latest version:

terminal

Copy

```
bun update [package]
```

## [​](https://bun.com/docs/pm/cli/update#interactive) `--interactive`

For a more controlled update experience, use the `--interactive` flag to select which packages to update:

terminal

Copy

```
bun update --interactive
bun update -i
```

This launches an interactive terminal interface that shows all outdated packages with their current and target versions. You can then select which packages to update.

### [​](https://bun.com/docs/pm/cli/update#interactive-interface) Interactive Interface

The interface displays packages grouped by dependency type:

Copy

```
? Select packages to update - Space to toggle, Enter to confirm, a to select all, n to select none, i to invert, l to toggle latest

  dependencies                Current  Target   Latest
    □ react                   17.0.2   18.2.0   18.3.1
    □ lodash                  4.17.20  4.17.21  4.17.21

  devDependencies             Current  Target   Latest
    □ typescript              4.8.0    5.0.0    5.3.3
    □ @types/node             16.11.7  18.0.0   20.11.5

  optionalDependencies        Current  Target   Latest
    □ some-optional-package   1.0.0    1.1.0    1.2.0
```

**Sections:**

* Packages are grouped under section headers: `dependencies`, `devDependencies`, `peerDependencies`, `optionalDependencies`
* Each section shows column headers aligned with the package data

**Columns:**

* **Package**: Package name (may have suffix like  `dev`,  `peer`,  `optional` for clarity)
* **Current**: Currently installed version
* **Target**: Version that would be installed (respects semver constraints)
* **Latest**: Latest available version

### [​](https://bun.com/docs/pm/cli/update#keyboard-controls) Keyboard Controls

**Selection:**

* **Space**: Toggle package selection
* **Enter**: Confirm selections and update
* **a/A**: Select all packages
* **n/N**: Select none
* **i/I**: Invert selection

**Navigation:**

* **↑/↓ Arrow keys** or **j/k**: Move cursor
* **l/L**: Toggle between target and latest version for current package

**Exit:**

* **Ctrl+C** or **Ctrl+D**: Cancel without updating

### [​](https://bun.com/docs/pm/cli/update#visual-indicators) Visual Indicators

* **☑** Selected packages (will be updated)
* **□** Unselected packages
* **>** Current cursor position
* **Colors**: Red (major), yellow (minor), green (patch) version changes
* **Underlined**: Currently selected update target

### [​](https://bun.com/docs/pm/cli/update#package-grouping) Package Grouping

Packages are organized in sections by dependency type:

* **dependencies** - Regular runtime dependencies
* **devDependencies** - Development dependencies
* **peerDependencies** - Peer dependencies
* **optionalDependencies** - Optional dependencies

Within each section, individual packages may have additional suffixes ( `dev`,  `peer`,  `optional`) for extra clarity.

## [​](https://bun.com/docs/pm/cli/update#recursive) `--recursive`

Use the `--recursive` flag with `--interactive` to update dependencies across all workspaces in a monorepo:

terminal

Copy

```
bun update --interactive --recursive
bun update -i -r
```

This displays an additional “Workspace” column showing which workspace each dependency belongs to.

## [​](https://bun.com/docs/pm/cli/update#latest) `--latest`

By default, `bun update` will update to the latest version of a dependency that satisfies the version range specified in your `package.json`.
To update to the latest version, regardless of if it’s compatible with the current version range, use the `--latest` flag:

terminal

Copy

```
bun update --latest
```

In interactive mode, you can toggle individual packages between their target version (respecting semver) and latest version using the **l** key.
For example, with the following `package.json`:

package.json

Copy

```
{
  "dependencies": {
    "react": "^17.0.2"
  }
}
```

* `bun update` would update to a version that matches `17.x`.
* `bun update --latest` would update to a version that matches `18.x` or later.

---

## [​](https://bun.com/docs/pm/cli/update#cli-usage) CLI Usage

terminal

Copy

```
bun update <package> <version>
```

### [​](https://bun.com/docs/pm/cli/update#update-strategy) Update Strategy

[​](https://bun.com/docs/pm/cli/update#param-force)

--force

boolean

Always request the latest versions from the registry & reinstall all dependencies. Alias: `-f`

[​](https://bun.com/docs/pm/cli/update#param-latest)

--latest

boolean

Update packages to their latest versions

### [​](https://bun.com/docs/pm/cli/update#dependency-scope) Dependency Scope

[​](https://bun.com/docs/pm/cli/update#param-production)

--production

boolean

Don’t install devDependencies. Alias: `-p`

[​](https://bun.com/docs/pm/cli/update#param-global)

--global

boolean

Install globally. Alias: `-g`

[​](https://bun.com/docs/pm/cli/update#param-omit)

--omit

string

Exclude `dev`, `optional`, or `peer` dependencies from install

### [​](https://bun.com/docs/pm/cli/update#project-file-management) Project File Management

[​](https://bun.com/docs/pm/cli/update#param-yarn)

--yarn

boolean

Write a `yarn.lock` file (yarn v1). Alias: `-y`

[​](https://bun.com/docs/pm/cli/update#param-no-save)

--no-save

boolean

Don’t update `package.json` or save a lockfile

[​](https://bun.com/docs/pm/cli/update#param-save)

--save

boolean

default:"true"

Save to `package.json` (true by default)

[​](https://bun.com/docs/pm/cli/update#param-frozen-lockfile)

--frozen-lockfile

boolean

Disallow changes to lockfile

[​](https://bun.com/docs/pm/cli/update#param-save-text-lockfile)

--save-text-lockfile

boolean

Save a text-based lockfile

[​](https://bun.com/docs/pm/cli/update#param-lockfile-only)

--lockfile-only

boolean

Generate a lockfile without installing dependencies

### [​](https://bun.com/docs/pm/cli/update#network-&-registry) Network & Registry

[​](https://bun.com/docs/pm/cli/update#param-ca)

--ca

string

Provide a Certificate Authority signing certificate

[​](https://bun.com/docs/pm/cli/update#param-cafile)

--cafile

string

Same as `—ca`, but as a file path to the certificate

[​](https://bun.com/docs/pm/cli/update#param-registry)

--registry

string

Use a specific registry by default, overriding `.npmrc`, `bunfig.toml` and environment variables

[​](https://bun.com/docs/pm/cli/update#param-network-concurrency)

--network-concurrency

number

default:"48"

Maximum number of concurrent network requests (default 48)

### [​](https://bun.com/docs/pm/cli/update#caching) Caching

[​](https://bun.com/docs/pm/cli/update#param-cache-dir)

--cache-dir

string

Store & load cached data from a specific directory path

[​](https://bun.com/docs/pm/cli/update#param-no-cache)

--no-cache

boolean

Ignore manifest cache entirely

### [​](https://bun.com/docs/pm/cli/update#output-&-logging) Output & Logging

[​](https://bun.com/docs/pm/cli/update#param-silent)

--silent

boolean

Don’t log anything

[​](https://bun.com/docs/pm/cli/update#param-verbose)

--verbose

boolean

Excessively verbose logging

[​](https://bun.com/docs/pm/cli/update#param-no-progress)

--no-progress

boolean

Disable the progress bar

[​](https://bun.com/docs/pm/cli/update#param-no-summary)

--no-summary

boolean

Don’t print a summary

### [​](https://bun.com/docs/pm/cli/update#script-execution) Script Execution

[​](https://bun.com/docs/pm/cli/update#param-ignore-scripts)

--ignore-scripts

boolean

Skip lifecycle scripts in the project’s `package.json` (dependency scripts are never run)

[​](https://bun.com/docs/pm/cli/update#param-concurrent-scripts)

--concurrent-scripts

number

default:"5"

Maximum number of concurrent jobs for lifecycle scripts (default 5)

### [​](https://bun.com/docs/pm/cli/update#installation-controls) Installation Controls

[​](https://bun.com/docs/pm/cli/update#param-no-verify)

--no-verify

boolean

Skip verifying integrity of newly downloaded packages

[​](https://bun.com/docs/pm/cli/update#param-trust)

--trust

boolean

Add to `trustedDependencies` in the project’s `package.json` and install the package(s)

[​](https://bun.com/docs/pm/cli/update#param-backend)

--backend

string

default:"clonefile"

Platform-specific optimizations for installing dependencies. Possible values: `clonefile` (default),
`hardlink`, `symlink`, `copyfile`

### [​](https://bun.com/docs/pm/cli/update#general-&-environment) General & Environment

[​](https://bun.com/docs/pm/cli/update#param-config)

--config

string

Specify path to config file (`bunfig.toml`). Alias: `-c`

[​](https://bun.com/docs/pm/cli/update#param-dry-run)

--dry-run

boolean

Don’t install anything

[​](https://bun.com/docs/pm/cli/update#param-cwd)

--cwd

string

Set a specific cwd

[​](https://bun.com/docs/pm/cli/update#param-help)

--help

boolean

Print this help menu. Alias: `-h`

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/pm/cli/update.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /pm/cli/update)

⌘I