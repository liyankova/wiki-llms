---
url: https://bun.com/blog/bun-v0.5.1
title: Bun v0.5.1 | Bun Blog
source_domain: bun.com
---

# Bun v0.5.1 | Bun Blog

# Bun v0.5.1

---

[Jarred Sumner](https://twitter.com/jarredsumner) · January 19, 2023

We're hiring [C/C++ and Zig engineers](https://bun.com/careers) to build the future of JavaScript!

Bun v0.5.1 adds support for aliasing package.json dependencies, a better error message when a workspace is not found, and a few important bug fixes. This release is a follow up to [Bun v0.5](https://bun.com/blog/bun-v0.5.0).

```
# Install Bun
curl https://bun.sh/install | bash

# Upgrade to latest release of Bun
bun upgrade
```

### [Alias dependencies in package.json](https://bun.com/blog/bun-v0.5.1#alias-dependencies-in-package-json)

`bun install` now supports aliasing dependencies via the `npm:` prefix (thanks to [@alexlamsl](https://github.com/alexlamsl))

This lets you install multiple versions of the same dependency and have it placed under a different folder in `node_modules`.

`package.json`:

```
{
  "name": "all-the-lodashes",
  "dependencies": {
    "lodash": "^4.17.21",
    "lodash3": "npm:lodash@3"
  }
}
```

`index.ts`:

```
const lodash3 = require("lodash3");
const lodash4 = require("lodash");

console.log(lodash3.VERSION);
console.log(lodash4.VERSION);
```

Output:

```
❯ bun index.ts

3.10.1
4.17.21
```

This feature is also supported by `npm`, `yarn` and others. Previously, when a package.json used this feature `bun install` showed an error message because it wasn't implemented yet.

### [Better error message when workspace is not found](https://bun.com/blog/bun-v0.5.1#better-error-message-when-workspace-is-not-found)

Before:

```
bun install v0.5.0 (2db04ef9)

error: FileNotFound
bun could not find a file, and the code that produces this error is missing a better error.

----- bun meta -----
Bun v0.5.0 (2db04ef9) macOS Silicon 22.2.0
InstallCommand: bunfig
Elapsed: 4ms | User: 5ms | Sys: 9ms
RSS: 14.07MB | Peak: 14.07MB | Commit: 69.22MB | Faults: 12
----- bun meta -----
```

After:

```
bun install v0.5.1 (f993975a)

error: Workspace not found "i-dont-exist" in "/private/tmp/bun-bad-workspace"

    "workspaces": ["i-dont-exist"]
                   ^
/private/tmp/bun-bad-workspace/package.json:3:18
```

For a package.json like this:

```
{
  "name": "my-workspace",
  "workspaces": ["i-dont-exist"]
}
```

## [Bug fixes](https://bun.com/blog/bun-v0.5.1#bug-fixes)

This release fixes a few important bugs

* A regression introduced in v0.5.0 where reading the `"encoding"` string caused crashes
* `fetch` was not wired up correctly to read the `HTTPS_PROXY` / `HTTP_PROXY` environment variables (fixed by [@cirospaciari](https://github.com/cirospaciari))
* Assigning `require` to a variable caused `undefined is not an object` errors if used more than once #1831
* A crash that sometimes occurred while processing long lists of workspace names
* `rmdir` was missing from `node:fs` (fixed by [@alexlamsl](https://github.com/alexlamsl))
* Error messages from BoringSSL were not being read correctly
* Fixes a transpiler issue with TypeScript parameter fields in the constructor function. This regression was introduced when TypeScript decorators were implemented [#1855](https://github.com/oven-sh/bun/issues/1855) (fixed by [@dylan-conway](https://github.com/dylan-conway))

## [PRs](https://bun.com/blog/bun-v0.5.1#prs)

| [`#1836`](https://github.com/oven-sh/bun/pull/1836) | Fix/simplify `bun-types` release by [@colinhacks](https://github.com/colinhacks) |
| --- | --- |
| [`#1838`](https://github.com/oven-sh/bun/pull/1838) | add `fs.rmdir` & friends by [@alexlamsl](https://github.com/alexlamsl) |
| [`#1837`](https://github.com/oven-sh/bun/pull/1837) | support npm dependency aliasing by [@alexlamsl](https://github.com/alexlamsl) |
| [`#1844`](https://github.com/oven-sh/bun/pull/1844) | fix(fetch:HTTP\_PROXY) fix support for HTTP\_PROXY/HTTPS\_PROXY and NO\_PROXY in fetch instances by [@cirospaciari](https://github.com/cirospaciari) |
| [`#1827`](https://github.com/oven-sh/bun/pull/1827) | Create new example http-file-extended.ts by [@gornostay25](https://github.com/gornostay25) |
| [`#1848`](https://github.com/oven-sh/bun/pull/1848) | Bugfixes to install by [@Jarred-Sumner](https://github.com/Jarred-Sumner) |
| [`#1850`](https://github.com/oven-sh/bun/pull/1850) | use `String.from()` by [@alexlamsl](https://github.com/alexlamsl) |

---

[#### Bun v0.5.0](https://bun.com/blog/bun-v0.5.0)[#### Bun v0.5.2](https://bun.com/blog/bun-v0.5.2)