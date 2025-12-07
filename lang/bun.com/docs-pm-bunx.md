---
url: https://bun.com/docs/pm/bunx
title: bunx - Bun
source_domain: bun.com
---

# bunx - Bun

`bunx` is an alias for `bun x`. The `bunx` CLI will be auto-installed when you install `bun`.

Use `bunx` to auto-install and run packages from `npm`. It’s Bun’s equivalent of `npx` or `yarn dlx`.

terminal

Copy

```
bunx cowsay "Hello world!"
```

⚡️ **Speed** — With Bun’s fast startup times, `bunx` is [roughly 100x
faster](https://twitter.com/jarredsumner/status/1606163655527059458) than `npx` for locally installed packages.

Packages can declare executables in the `"bin"` field of their `package.json`. These are known as *package executables* or *package binaries*.

package.json

Copy

```
{
  // ... other fields
  "name": "my-cli",
  "bin": {
    "my-cli": "dist/index.js"
  }
}
```

These executables are commonly plain JavaScript files marked with a [shebang line](https://en.wikipedia.org/wiki/Shebang_(Unix)) to indicate which program should be used to execute them. The following file indicates that it should be executed with `node`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/javascript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=81efd0ad0d779debfa163bfd906ef6a6](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/javascript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=81efd0ad0d779debfa163bfd906ef6a6)dist/index.js

Copy

```
#!/usr/bin/env node

console.log("Hello world!");
```

These executables can be run with `bunx`,

terminal

Copy

```
bunx my-cli
```

As with `npx`, `bunx` will check for a locally installed package first, then fall back to auto-installing the package from `npm`. Installed packages will be stored in Bun’s global cache for future use.

## [​](https://bun.com/docs/pm/bunx#arguments-and-flags) Arguments and flags

To pass additional command-line flags and arguments through to the executable, place them after the executable name.

terminal

Copy

```
bunx my-cli --foo bar
```

---

## [​](https://bun.com/docs/pm/bunx#shebangs) Shebangs

By default, Bun respects shebangs. If an executable is marked with `#!/usr/bin/env node`, Bun will spin up a `node` process to execute the file. However, in some cases it may be desirable to run executables using Bun’s runtime, even if the executable indicates otherwise. To do so, include the `--bun` flag.

terminal

Copy

```
bunx --bun my-cli
```

The `--bun` flag must occur *before* the executable name. Flags that appear *after* the name are passed through to the executable.

terminal

Copy

```
bunx --bun my-cli # good
bunx my-cli --bun # bad
```

## [​](https://bun.com/docs/pm/bunx#package-flag) Package flag

**`--package <pkg>` or `-p <pkg>`** - Run binary from specific package. Useful when binary name differs from package name:

terminal

Copy

```
bunx -p renovate renovate-config-validator
bunx --package @angular/cli ng
```

To force bun to always be used with a script, use a shebang.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/javascript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=81efd0ad0d779debfa163bfd906ef6a6](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/javascript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=81efd0ad0d779debfa163bfd906ef6a6)dist/index.js

Copy

```
#!/usr/bin/env bun
```

---

## [​](https://bun.com/docs/pm/bunx#usage) Usage

Copy

```
bunx [flags] <package>[@version] [flags and arguments for the package]
```

Execute an npm package executable (CLI), automatically installing into a global shared cache if not installed in `node_modules`.

### [​](https://bun.com/docs/pm/bunx#flags) Flags

[​](https://bun.com/docs/pm/bunx#param-bun)

--bun

boolean

Force the command to run with Bun instead of Node.js, even if the executable contains a Node shebang (`#!/usr/bin/env node`)

[​](https://bun.com/docs/pm/bunx#param-p-package)

-p, --package

string

Specify package to install when binary name differs from package name

[​](https://bun.com/docs/pm/bunx#param-no-install)

--no-install

boolean

Skip installation if package is not already installed

[​](https://bun.com/docs/pm/bunx#param-verbose)

--verbose

boolean

Enable verbose output during installation

[​](https://bun.com/docs/pm/bunx#param-silent)

--silent

boolean

Suppress output during installation

### [​](https://bun.com/docs/pm/bunx#examples) Examples

terminal

Copy

```
# Run Prisma migrations
bunx prisma migrate

# Format a file with Prettier
bunx prettier foo.js

# Run a specific version of a package
bunx [email protected] app.js

# Use --package when binary name differs from package name
bunx -p @angular/cli ng new my-app

# Force running with Bun instead of Node.js, even if the executable contains a Node shebang
bunx --bun vite dev foo.js
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/pm/bunx.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /pm/bunx)

⌘I