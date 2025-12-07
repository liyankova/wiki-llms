---
url: https://bun.com/docs/pm/cli/add
title: bun add - Bun
source_domain: bun.com
---

# bun add - Bun

To add a particular package:

terminal

Copy

```
bun add preact
```

To specify a version, version range, or tag:

terminal

Copy

```
bun add [email protected]
bun add zod@^3.0.0
bun add zod@latest
```

## [​](https://bun.com/docs/pm/cli/add#dev) `--dev`

**Alias** — `--development`, `-d`, `-D`

To add a package as a dev dependency (`"devDependencies"`):

terminal

Copy

```
bun add --dev @types/react
bun add -d @types/react
```

## [​](https://bun.com/docs/pm/cli/add#optional) `--optional`

To add a package as an optional dependency (`"optionalDependencies"`):

terminal

Copy

```
bun add --optional lodash
```

## [​](https://bun.com/docs/pm/cli/add#peer) `--peer`

To add a package as a peer dependency (`"peerDependencies"`):

terminal

Copy

```
bun add --peer @types/bun
```

## [​](https://bun.com/docs/pm/cli/add#exact) `--exact`

**Alias** — `-E`

To add a package and pin to the resolved version, use `--exact`. This will resolve the version of the package and add it to your `package.json` with an exact version number instead of a version range.

terminal

Copy

```
bun add react --exact
bun add react -E
```

This will add the following to your `package.json`:

package.json

Copy

```
{
  "dependencies": {
    // without --exact
    "react": "^18.2.0", // this matches >= 18.2.0 < 19.0.0

    // with --exact
    "react": "18.2.0" // this matches only 18.2.0 exactly
  }
}
```

To view a complete list of options for this command:

terminal

Copy

```
bun add --help
```

## [​](https://bun.com/docs/pm/cli/add#global) `--global`

**Note** — This would not modify package.json of your current project folder. **Alias** - `bun add --global`, `bun add -g`, `bun install --global` and `bun install -g`

To install a package globally, use the `-g`/`--global` flag. This will not modify the `package.json` of your current project. Typically this is used for installing command-line tools.

terminal

Copy

```
bun add --global cowsay # or `bun add -g cowsay`
cowsay "Bun!"
```

Copy

```
 ______
< Bun! >
 ------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

Configuring global installation behavior

bunfig.toml

Copy

```
[install]
# where `bun add --global` installs packages
globalDir = "~/.bun/install/global"

# where globally-installed package bins are linked
globalBinDir = "~/.bun/bin"
```

## [​](https://bun.com/docs/pm/cli/add#trusted-dependencies) Trusted dependencies

Unlike other npm clients, Bun does not execute arbitrary lifecycle scripts for installed dependencies, such as `postinstall`. These scripts represent a potential security risk, as they can execute arbitrary code on your machine.
To tell Bun to allow lifecycle scripts for a particular package, add the package to `trustedDependencies` in your package.json.

package.json

Copy

```
{
  "name": "my-app",
  "version": "1.0.0",
  "trustedDependencies": ["my-trusted-package"] 
}
```

Bun reads this field and will run lifecycle scripts for `my-trusted-package`.

## [​](https://bun.com/docs/pm/cli/add#git-dependencies) Git dependencies

To add a dependency from a public or private git repository:

terminal

Copy

```
bun add [email protected]:moment/moment.git
```

To install private repositories, your system needs the appropriate SSH credentials to access the repository.

Bun supports a variety of protocols, including [`github`](https://docs.npmjs.com/cli/v9/configuring-npm/package-json#github-urls), [`git`](https://docs.npmjs.com/cli/v9/configuring-npm/package-json#git-urls-as-dependencies), `git+ssh`, `git+https`, and many more.

package.json

Copy

```
{
  "dependencies": {
    "dayjs": "git+https://github.com/iamkun/dayjs.git",
    "lodash": "git+ssh://github.com/lodash/lodash.git#4.17.21",
    "moment": "[email protected]:moment/moment.git",
    "zod": "github:colinhacks/zod"
  }
}
```

## [​](https://bun.com/docs/pm/cli/add#tarball-dependencies) Tarball dependencies

A package name can correspond to a publicly hosted `.tgz` file. During installation, Bun will download and install the package from the specified tarball URL, rather than from the package registry.

terminal

Copy

```
bun add zod@https://registry.npmjs.org/zod/-/zod-3.21.4.tgz
```

This will add the following line to your `package.json`:

package.json

Copy

```
{
  "dependencies": {
    "zod": "https://registry.npmjs.org/zod/-/zod-3.21.4.tgz"
  }
}
```

---

## [​](https://bun.com/docs/pm/cli/add#cli-usage) CLI Usage

Copy

```
bun add <package> <@version>
```

### [​](https://bun.com/docs/pm/cli/add#dependency-management) Dependency Management

[​](https://bun.com/docs/pm/cli/add#param-production)

--production

boolean

Don’t install devDependencies. Alias: `-p`

[​](https://bun.com/docs/pm/cli/add#param-omit)

--omit

string

Exclude `dev`, `optional`, or `peer` dependencies from install

[​](https://bun.com/docs/pm/cli/add#param-global)

--global

boolean

Install globally. Alias: `-g`

[​](https://bun.com/docs/pm/cli/add#param-dev)

--dev

boolean

Add dependency to `devDependencies`. Alias: `-d`

[​](https://bun.com/docs/pm/cli/add#param-optional)

--optional

boolean

Add dependency to `optionalDependencies`

[​](https://bun.com/docs/pm/cli/add#param-peer)

--peer

boolean

Add dependency to `peerDependencies`

[​](https://bun.com/docs/pm/cli/add#param-exact)

--exact

boolean

Add the exact version instead of the `^` range. Alias: `-E`

[​](https://bun.com/docs/pm/cli/add#param-only-missing)

--only-missing

boolean

Only add dependencies to `package.json` if they are not already present

### [​](https://bun.com/docs/pm/cli/add#project-files-&-lockfiles) Project Files & Lockfiles

[​](https://bun.com/docs/pm/cli/add#param-yarn)

--yarn

boolean

Write a `yarn.lock` file (yarn v1). Alias: `-y`

[​](https://bun.com/docs/pm/cli/add#param-no-save)

--no-save

boolean

Don’t update `package.json` or save a lockfile

[​](https://bun.com/docs/pm/cli/add#param-save)

--save

boolean

default:"true"

Save to `package.json` (true by default)

[​](https://bun.com/docs/pm/cli/add#param-frozen-lockfile)

--frozen-lockfile

boolean

Disallow changes to lockfile

[​](https://bun.com/docs/pm/cli/add#param-trust)

--trust

boolean

Add to `trustedDependencies` in the project’s `package.json` and install the package(s)

[​](https://bun.com/docs/pm/cli/add#param-save-text-lockfile)

--save-text-lockfile

boolean

Save a text-based lockfile

[​](https://bun.com/docs/pm/cli/add#param-lockfile-only)

--lockfile-only

boolean

Generate a lockfile without installing dependencies

### [​](https://bun.com/docs/pm/cli/add#installation-control) Installation Control

[​](https://bun.com/docs/pm/cli/add#param-dry-run)

--dry-run

boolean

Don’t install anything

[​](https://bun.com/docs/pm/cli/add#param-force)

--force

boolean

Always request the latest versions from the registry & reinstall all dependencies. Alias: `-f`

[​](https://bun.com/docs/pm/cli/add#param-no-verify)

--no-verify

boolean

Skip verifying integrity of newly downloaded packages

[​](https://bun.com/docs/pm/cli/add#param-ignore-scripts)

--ignore-scripts

boolean

Skip lifecycle scripts in the project’s `package.json` (dependency scripts are never run)

[​](https://bun.com/docs/pm/cli/add#param-analyze)

--analyze

boolean

Recursively analyze & install dependencies of files passed as arguments (using Bun’s bundler). Alias:
`-a`

### [​](https://bun.com/docs/pm/cli/add#network-&-registry) Network & Registry

[​](https://bun.com/docs/pm/cli/add#param-ca)

--ca

string

Provide a Certificate Authority signing certificate

[​](https://bun.com/docs/pm/cli/add#param-cafile)

--cafile

string

Same as `—ca`, but as a file path to the certificate

[​](https://bun.com/docs/pm/cli/add#param-registry)

--registry

string

Use a specific registry by default, overriding `.npmrc`, `bunfig.toml`, and environment
variables

[​](https://bun.com/docs/pm/cli/add#param-network-concurrency)

--network-concurrency

number

default:"48"

Maximum number of concurrent network requests (default 48)

### [​](https://bun.com/docs/pm/cli/add#performance-&-resource) Performance & Resource

[​](https://bun.com/docs/pm/cli/add#param-backend)

--backend

string

default:"clonefile"

Platform-specific optimizations for installing dependencies. Possible values: `clonefile` (default),
`hardlink`, `symlink`, `copyfile`

[​](https://bun.com/docs/pm/cli/add#param-concurrent-scripts)

--concurrent-scripts

number

default:"5"

Maximum number of concurrent jobs for lifecycle scripts (default 5)

### [​](https://bun.com/docs/pm/cli/add#caching) Caching

[​](https://bun.com/docs/pm/cli/add#param-cache-dir)

--cache-dir

string

Store & load cached data from a specific directory path

[​](https://bun.com/docs/pm/cli/add#param-no-cache)

--no-cache

boolean

Ignore manifest cache entirely

### [​](https://bun.com/docs/pm/cli/add#output-&-logging) Output & Logging

[​](https://bun.com/docs/pm/cli/add#param-silent)

--silent

boolean

Don’t log anything

[​](https://bun.com/docs/pm/cli/add#param-verbose)

--verbose

boolean

Excessively verbose logging

[​](https://bun.com/docs/pm/cli/add#param-no-progress)

--no-progress

boolean

Disable the progress bar

[​](https://bun.com/docs/pm/cli/add#param-no-summary)

--no-summary

boolean

Don’t print a summary

### [​](https://bun.com/docs/pm/cli/add#global-configuration-&-context) Global Configuration & Context

[​](https://bun.com/docs/pm/cli/add#param-config)

--config

string

Specify path to config file (`bunfig.toml`). Alias: `-c`

[​](https://bun.com/docs/pm/cli/add#param-cwd)

--cwd

string

Set a specific current working directory

### [​](https://bun.com/docs/pm/cli/add#help) Help

[​](https://bun.com/docs/pm/cli/add#param-help)

--help

boolean

Print this help menu. Alias: `-h`

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/pm/cli/add.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /pm/cli/add)

⌘I