---
url: https://bun.com/docs/pm/lifecycle
title: Lifecycle scripts - Bun
source_domain: bun.com
---

# Lifecycle scripts - Bun

Packages on `npm` can define *lifecycle scripts* in their `package.json`. Some of the most common are below, but there are [many others](https://docs.npmjs.com/cli/v10/using-npm/scripts).

* `preinstall`: Runs before the package is installed
* `postinstall`: Runs after the package is installed
* `preuninstall`: Runs before the package is uninstalled
* `prepublishOnly`: Runs before the package is published

These scripts are arbitrary shell commands that the package manager is expected to read and execute at the appropriate time. But executing arbitrary scripts represents a potential security risk, so—unlike other `npm` clients—Bun does not execute arbitrary lifecycle scripts by default.

---

## [​](https://bun.com/docs/pm/lifecycle#postinstall) `postinstall`

The `postinstall` script is particularly important. It’s widely used to build or install platform-specific binaries for packages that are implemented as [native Node.js add-ons](https://nodejs.org/api/addons.html). For example, `node-sass` is a popular package that uses `postinstall` to build a native binary for Sass.

package.json

Copy

```
{
  "name": "my-app",
  "version": "1.0.0",
  "dependencies": {
    "node-sass": "^6.0.1"
  }
}
```

---

## [​](https://bun.com/docs/pm/lifecycle#trusteddependencies) `trustedDependencies`

Instead of executing arbitrary scripts, Bun uses a “default-secure” approach. You can add certain packages to an allow list, and Bun will execute lifecycle scripts for those packages. To tell Bun to allow lifecycle scripts for a particular package, add the package name to `trustedDependencies` array in your `package.json`.

package.json

Copy

```
{
  "name": "my-app",
  "version": "1.0.0",
  "trustedDependencies": ["node-sass"] 
}
```

Once added to `trustedDependencies`, install/re-install the package. Bun will read this field and run lifecycle scripts for `my-trusted-package`.
The top 500 npm packages with lifecycle scripts are allowed by default. You can see the full list [here](https://github.com/oven-sh/bun/blob/main/src/install/default-trusted-dependencies.txt).

---

## [​](https://bun.com/docs/pm/lifecycle#ignore-scripts) `--ignore-scripts`

To disable lifecycle scripts for all packages, use the `--ignore-scripts` flag.

terminal

Copy

```
bun install --ignore-scripts
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/pm/lifecycle.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /pm/lifecycle)

⌘I