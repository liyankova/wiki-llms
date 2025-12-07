---
url: https://bun.com/docs/guides/install/from-npm-install-to-bun-install
title: Migrate from npm install to bun install - Bun
source_domain: bun.com
---

# Migrate from npm install to bun install - Bun

`bun install` is a Node.js compatible npm client designed to be an incredibly fast successor to npm.
We’ve put a lot of work into making sure that the migration path from `npm install` to `bun install` is as easy as running `bun install` instead of `npm install`.

* **Designed for Node.js & Bun**: `bun install` installs a Node.js compatible `node_modules` folder. You can use it in place of `npm install` for Node.js projects without any code changes and without using Bun’s runtime.
* **Automatically converts `package-lock.json`** to bun’s `bun.lock` lockfile format, preserving your existing resolved dependency versions without any manual work on your part. You can secretly use `bun install` in place of `npm install` at work without anyone noticing.
* **`.npmrc` compatible**: bun install reads npm registry configuration from npm’s `.npmrc`, so you can use the same configuration for both npm and Bun.
* **Hardlinks**: On Windows and Linux, `bun install` uses hardlinks to conserve disk space and install times.

terminal

Copy

```
# It only takes one command to migrate
bun i

# To add dependencies:
bun i @types/bun

# To add devDependencies:
bun i -d @types/bun

# To remove a dependency:
bun rm @types/bun
```

---

## [​](https://bun.com/docs/guides/install/from-npm-install-to-bun-install#run-package-json-scripts-faster) Run package.json scripts faster

Run scripts from package.json, executables from `node_modules/.bin` (sort of like `npx`), and JavaScript/TypeScript files (just like `node`) - all from a single simple command.

| NPM | Bun |
| --- | --- |
| `npm run <script>` | `bun <script>` |
| `npm exec <bin>` | `bun <bin>` |
| `node <file>` | `bun <file>` |
| `npx <package>` | `bunx <package>` |

When you use `bun run <executable>`, it will choose the locally-installed executable

terminal

Copy

```
# Run a package.json script:
bun my-script
bun run my-script

# Run an executable in node_modules/.bin:
bun my-executable # such as tsc, esbuild, etc.
bun run my-executable

# Run a JavaScript/TypeScript file:
bun ./index.ts
```

---

## [​](https://bun.com/docs/guides/install/from-npm-install-to-bun-install#workspaces-yes) Workspaces? Yes.

`bun install` supports workspaces similarly to npm, with more features.
In package.json, you can set `"workspaces"` to an array of relative paths.

package.json

Copy

```
{
  "name": "my-app",
  "workspaces": ["packages/*", "apps/*"]
}
```

---

### [​](https://bun.com/docs/guides/install/from-npm-install-to-bun-install#filter-scripts-by-workspace-name) Filter scripts by workspace name

In Bun, the `--filter` flag accepts a glob pattern, and will run the command concurrently for all workspace packages with a `name` that matches the pattern, respecting dependency order.

terminal

Copy

```
bun --filter 'lib-*' my-script
# instead of:
# npm run --workspace lib-foo --workspace lib-bar my-script
```

---

## [​](https://bun.com/docs/guides/install/from-npm-install-to-bun-install#update-dependencies) Update dependencies

To update a dependency, you can use `bun update <package>`. This will update the dependency to the latest version that satisfies the semver range specified in package.json.

terminal

Copy

```
# Update a single dependency
bun update @types/bun

# Update all dependencies
bun update

# Ignore semver, update to the latest version
bun update @types/bun --latest

# Update a dependency to a specific version
bun update @types/[email protected]

# Update all dependencies to the latest versions
bun update --latest
```

---

### [​](https://bun.com/docs/guides/install/from-npm-install-to-bun-install#view-outdated-dependencies) View outdated dependencies

To view outdated dependencies, run `bun outdated`. This is like `npm outdated` but with more compact output.

terminal

Copy

```
bun outdated
```

Copy

```
┌────────────────────────────────────────┬─────────┬────────┬────────┐
│ Package                                │ Current │ Update │ Latest │
├────────────────────────────────────────┼─────────┼────────┼────────┤
│ @types/bun (dev)                       │ 1.1.6   │ 1.1.10 │ 1.1.10 │
├────────────────────────────────────────┼─────────┼────────┼────────┤
│ @types/react (dev)                     │ 18.3.3  │ 18.3.8 │ 18.3.8 │
├────────────────────────────────────────┼─────────┼────────┼────────┤
│ @typescript-eslint/eslint-plugin (dev) │ 7.16.1  │ 7.18.0 │ 8.6.0  │
├────────────────────────────────────────┼─────────┼────────┼────────┤
│ @typescript-eslint/parser (dev)        │ 7.16.1  │ 7.18.0 │ 8.6.0  │
├────────────────────────────────────────┼─────────┼────────┼────────┤
│ @vscode/debugadapter (dev)             │ 1.66.0  │ 1.67.0 │ 1.67.0 │
├────────────────────────────────────────┼─────────┼────────┼────────┤
│ esbuild (dev)                          │ 0.21.5  │ 0.21.5 │ 0.24.0 │
├────────────────────────────────────────┼─────────┼────────┼────────┤
│ eslint (dev)                           │ 9.7.0   │ 9.11.0 │ 9.11.0 │
├────────────────────────────────────────┼─────────┼────────┼────────┤
│ mitata (dev)                           │ 0.1.11  │ 0.1.14 │ 1.0.2  │
├────────────────────────────────────────┼─────────┼────────┼────────┤
│ prettier-plugin-organize-imports (dev) │ 4.0.0   │ 4.1.0  │ 4.1.0  │
├────────────────────────────────────────┼─────────┼────────┼────────┤
│ source-map-js (dev)                    │ 1.2.0   │ 1.2.1  │ 1.2.1  │
├────────────────────────────────────────┼─────────┼────────┼────────┤
│ typescript (dev)                       │ 5.5.3   │ 5.6.2  │ 5.6.2  │
└────────────────────────────────────────┴─────────┴────────┴────────┘
```

---

## [​](https://bun.com/docs/guides/install/from-npm-install-to-bun-install#list-installed-packages) List installed packages

To list installed packages, you can use `bun pm ls`. This will list all the packages that are installed in the `node_modules` folder using Bun’s lockfile as the source of truth. You can pass the `-a` flag to list all installed packages, including transitive dependencies.

terminal

Copy

```
# List top-level installed packages:
bun pm ls
```

Copy

```
my-pkg node_modules (781)
├── @types/[email protected]
├── @types/[email protected]
├── @types/[email protected]
├── [email protected]
├── [email protected]
...
```

terminal

Copy

```
# List all installed packages:
bun pm ls -a
```

Copy

```
my-pkg node_modules
├── @alloc/[email protected]
├── @isaacs/[email protected]
│   └── [email protected]
│       └── [email protected]
├── @jridgewell/[email protected]
├── @jridgewell/[email protected]
...
```

---

## [​](https://bun.com/docs/guides/install/from-npm-install-to-bun-install#create-a-package-tarball) Create a package tarball

To create a package tarball, you can use `bun pm pack`. This will create a tarball of the package in the current directory.

terminal

Copy

```
# Create a tarball
bun pm pack
```

Copy

```
Total files: 46
Shasum: 2ee19b6f0c6b001358449ca0eadead703f326216
Integrity: sha512-ZV0lzWTEkGAMz[...]Gl4f8lA9sl97g==
Unpacked size: 0.41MB
Packed size: 117.50KB
```

---

## [​](https://bun.com/docs/guides/install/from-npm-install-to-bun-install#shebang) Shebang

If the package references `node` in the `#!/usr/bin/env node` shebang, `bun run` will by default respect it and use the system’s `node` executable. You can force it to use Bun’s `node` by passing `--bun` to `bun run`.
When you pass `--bun` to `bun run`, we create a symlink to the locally-installed Bun executable named `"node"` in a temporary directory and add that to your `PATH` for the duration of the script’s execution.

terminal

Copy

```
# Force using Bun's runtime instead of node
bun --bun my-script

# This also works:
bun run --bun my-script
```

---

## [​](https://bun.com/docs/guides/install/from-npm-install-to-bun-install#global-installs) Global installs

You can install packages globally using `bun i -g <package>`. This will install into a `.bun/install/global/node_modules` folder inside your home directory by default.

terminal

Copy

```
# Install a package globally
bun i -g eslint

# Run a globally-installed package without the `bun run` prefix
eslint --init
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/install/from-npm-install-to-bun-install.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/install/from-npm-install-to-bun-install)

⌘I