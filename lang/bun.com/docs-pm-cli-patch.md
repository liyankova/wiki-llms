---
url: https://bun.com/docs/pm/cli/patch
title: bun patch - Bun
source_domain: bun.com
---

# bun patch - Bun

`bun patch` lets you persistently patch node\_modules in a maintainable, git-friendly way.
Sometimes, you need to make a small change to a package in `node_modules/` to fix a bug or add a feature. `bun patch` makes it easy to do this without vendoring the entire package and reuse the patch across multiple installs, multiple projects, and multiple machines.
Features:

* Generates `.patch` files applied to dependencies in `node_modules` on install
* `.patch` files can be committed to your repository, reused across multiple installs, projects, and machines
* `"patchedDependencies"` in `package.json` keeps track of patched packages
* `bun patch` lets you patch packages in `node_modules/` while preserving the integrity of Bun’s [Global Cache](https://bun.com/docs/pm/global-cache)
* Test your changes locally before committing them with `bun patch --commit <pkg>`
* To preserve disk space and keep `bun install` fast, patched packages are committed to the Global Cache and shared across projects where possible

#### [​](https://bun.com/docs/pm/cli/patch#step-1-prepare-the-package-for-patching) Step 1. Prepare the package for patching

To get started, use `bun patch <pkg>` to prepare the package for patching:

terminal

Copy

```
# you can supply the package name
bun patch react

# ...and a precise version in case multiple versions are installed
bun patch [email protected]

# or the path to the package
bun patch node_modules/react
```

Don’t forget to call `bun patch <pkg>`! This ensures the package folder in `node_modules/` contains a fresh copy of the package with no symlinks/hardlinks to Bun’s cache.If you forget to do this, you might end up editing the package globally in the cache!

#### [​](https://bun.com/docs/pm/cli/patch#step-2-test-your-changes-locally) Step 2. Test your changes locally

`bun patch <pkg>` makes it safe to edit the `<pkg>` in `node_modules/` directly, while preserving the integrity of Bun’s [Global Cache](https://bun.com/docs/pm/global-cache). This works by re-creating an unlinked clone of the package in `node_modules/` and diffing it against the original package in the Global Cache.

#### [​](https://bun.com/docs/pm/cli/patch#step-3-commit-your-changes) Step 3. Commit your changes

Once you’re happy with your changes, run `bun patch --commit <path or pkg>`.
Bun will generate a patch file in `patches/`, update your `package.json` and lockfile, and Bun will start using the patched package:

terminal

Copy

```
# you can supply the path to the patched package
bun patch --commit node_modules/react

# ... or the package name and optionally the version
bun patch --commit [email protected]

# choose the directory to store the patch files
bun patch --commit react --patches-dir=mypatches

# `patch-commit` is available for compatibility with pnpm
bun patch-commit react
```

---

# [​](https://bun.com/docs/pm/cli/patch#cli-usage) CLI Usage

Copy

```
bun patch <package>@<version>
```

### [​](https://bun.com/docs/pm/cli/patch#patch-generation) Patch Generation

[​](https://bun.com/docs/pm/cli/patch#param-commit)

--commit

boolean

Install a package containing modifications in `dir`

[​](https://bun.com/docs/pm/cli/patch#param-patches-dir)

--patches-dir

string

The directory to put the patch file in (only if —commit is used)

### [​](https://bun.com/docs/pm/cli/patch#dependency-management) Dependency Management

[​](https://bun.com/docs/pm/cli/patch#param-production)

--production

boolean

Don’t install devDependencies. Alias: `-p`

[​](https://bun.com/docs/pm/cli/patch#param-ignore-scripts)

--ignore-scripts

boolean

Skip lifecycle scripts in the project’s `package.json` (dependency scripts are never run)

[​](https://bun.com/docs/pm/cli/patch#param-trust)

--trust

boolean

Add to `trustedDependencies` in the project’s `package.json` and install the package(s)

[​](https://bun.com/docs/pm/cli/patch#param-global)

--global

boolean

Install globally. Alias: `-g`

[​](https://bun.com/docs/pm/cli/patch#param-omit)

--omit

string

Exclude `dev`, `optional`, or `peer` dependencies from install

### [​](https://bun.com/docs/pm/cli/patch#project-files-&-lockfiles) Project Files & Lockfiles

[​](https://bun.com/docs/pm/cli/patch#param-yarn)

--yarn

boolean

Write a `yarn.lock` file (yarn v1). Alias: `-y`

[​](https://bun.com/docs/pm/cli/patch#param-no-save)

--no-save

boolean

Don’t update `package.json` or save a lockfile

[​](https://bun.com/docs/pm/cli/patch#param-save)

--save

boolean

default:"true"

Save to `package.json` (true by default)

[​](https://bun.com/docs/pm/cli/patch#param-frozen-lockfile)

--frozen-lockfile

boolean

Disallow changes to lockfile

[​](https://bun.com/docs/pm/cli/patch#param-save-text-lockfile)

--save-text-lockfile

boolean

Save a text-based lockfile

[​](https://bun.com/docs/pm/cli/patch#param-lockfile-only)

--lockfile-only

boolean

Generate a lockfile without installing dependencies

### [​](https://bun.com/docs/pm/cli/patch#installation-control) Installation Control

[​](https://bun.com/docs/pm/cli/patch#param-backend)

--backend

string

default:"clonefile"

Platform-specific optimizations for installing dependencies. Possible values: `clonefile` (default),
`hardlink`, `symlink`, `copyfile`

[​](https://bun.com/docs/pm/cli/patch#param-linker)

--linker

string

Linker strategy (one of `isolated` or `hoisted`)

[​](https://bun.com/docs/pm/cli/patch#param-dry-run)

--dry-run

boolean

Don’t install anything

[​](https://bun.com/docs/pm/cli/patch#param-force)

--force

boolean

Always request the latest versions from the registry & reinstall all dependencies. Alias: `-f`

[​](https://bun.com/docs/pm/cli/patch#param-no-verify)

--no-verify

boolean

Skip verifying integrity of newly downloaded packages

### [​](https://bun.com/docs/pm/cli/patch#network-&-registry) Network & Registry

[​](https://bun.com/docs/pm/cli/patch#param-ca)

--ca

string

Provide a Certificate Authority signing certificate

[​](https://bun.com/docs/pm/cli/patch#param-cafile)

--cafile

string

Same as `—ca`, but as a file path to the certificate

[​](https://bun.com/docs/pm/cli/patch#param-registry)

--registry

string

Use a specific registry by default, overriding `.npmrc`, `bunfig.toml`, and environment
variables

[​](https://bun.com/docs/pm/cli/patch#param-network-concurrency)

--network-concurrency

number

default:"48"

Maximum number of concurrent network requests (default 48)

### [​](https://bun.com/docs/pm/cli/patch#performance-&-resource) Performance & Resource

[​](https://bun.com/docs/pm/cli/patch#param-concurrent-scripts)

--concurrent-scripts

number

default:"5"

Maximum number of concurrent jobs for lifecycle scripts (default 5)

### [​](https://bun.com/docs/pm/cli/patch#caching) Caching

[​](https://bun.com/docs/pm/cli/patch#param-cache-dir)

--cache-dir

string

Store & load cached data from a specific directory path

[​](https://bun.com/docs/pm/cli/patch#param-no-cache)

--no-cache

boolean

Ignore manifest cache entirely

### [​](https://bun.com/docs/pm/cli/patch#output-&-logging) Output & Logging

[​](https://bun.com/docs/pm/cli/patch#param-silent)

--silent

boolean

Don’t log anything

[​](https://bun.com/docs/pm/cli/patch#param-quiet)

--quiet

boolean

Only show tarball name when packing

[​](https://bun.com/docs/pm/cli/patch#param-verbose)

--verbose

boolean

Excessively verbose logging

[​](https://bun.com/docs/pm/cli/patch#param-no-progress)

--no-progress

boolean

Disable the progress bar

[​](https://bun.com/docs/pm/cli/patch#param-no-summary)

--no-summary

boolean

Don’t print a summary

### [​](https://bun.com/docs/pm/cli/patch#platform-targeting) Platform Targeting

[​](https://bun.com/docs/pm/cli/patch#param-cpu)

--cpu

string

Override CPU architecture for optional dependencies (e.g., `x64`, `arm64`, `*` for
all)

[​](https://bun.com/docs/pm/cli/patch#param-os)

--os

string

Override operating system for optional dependencies (e.g., `linux`, `darwin`, `*` for
all)

### [​](https://bun.com/docs/pm/cli/patch#global-configuration-&-context) Global Configuration & Context

[​](https://bun.com/docs/pm/cli/patch#param-config)

--config

string

Specify path to config file (`bunfig.toml`). Alias: `-c`

[​](https://bun.com/docs/pm/cli/patch#param-cwd)

--cwd

string

Set a specific current working directory

### [​](https://bun.com/docs/pm/cli/patch#help) Help

[​](https://bun.com/docs/pm/cli/patch#param-help)

--help

boolean

Print this help menu. Alias: `-h`

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/pm/cli/patch.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /pm/cli/patch)

⌘I