---
url: https://bun.com/blog/bun-v1.1.33
title: Bun v1.1.33 | Bun Blog
source_domain: bun.com
---

# Bun v1.1.33 | Bun Blog

# Bun v1.1.33

---

[Dylan Conway](https://github.com/dylan-conway) · October 24, 2024

We're hiring [systems engineers](https://bun.com/careers) in San Francisco to build the future of JavaScript!

This release fixes 8 bugs including: JSX symbol collisions with imports, `bun install` slowdowns, skipping optional dependencies, optional dependency postinstall failures, and an assertion failure in the CSS parser.

#### To install Bun

curl

npm

powershell

scoop

brew

docker

curl

```
curl -fsSL https://bun.sh/install | bash
```

npm

```
npm install -g bun
```

powershell

```
powershell -c "irm bun.sh/install.ps1|iex"
```

scoop

```
scoop install bun
```

brew

```
brew tap oven-sh/bun
```

```
brew install bun
```

docker

```
docker pull oven/bun
```

```
docker run --rm --init --ulimit memlock=-1:-1 oven/bun
```

#### To upgrade Bun

```
bun upgrade
```

## [Fixed: `NPM_CONFIG_TOKEN` environment variable](https://bun.com/blog/bun-v1.1.33#fixed-npm-config-token-environment-variable)

A bug reading the `NPM_CONFIG_TOKEN` environment variable due to lowercase letters was fixed. The diff was:

```
-  "NPM_CONFIG_token",
+  "NPM_CONFIG_TOKEN",
```

## [Reduced `bun install` max simultaneous connections](https://bun.com/blog/bun-v1.1.33#reduced-bun-install-max-simultaneous-connections)

`bun install` was using 256 as the default maximum number of simultaneous network connections. Allowing this many connections at once could cause install slowdowns while fetching dependency tarballs and manifests. We've reduced the default to 64 with and without a proxy.

## [Fixed: `optional = false` in `bunfig.toml`](https://bun.com/blog/bun-v1.1.33#fixed-optional-false-in-bunfig-toml)

Our docs mention setting `optional = false` in `bunfig.toml` will skip optional dependencies during installs, but the implementation was missing. This is now working as expected thanks to [@Eckhardt-D](https://github.com/Eckhardt-D)!

bunfig.toml

```
[install]
optional = false
```

## [Deleting optional dependencies on postinstall failure](https://bun.com/blog/bun-v1.1.33#deleting-optional-dependencies-on-postinstall-failure)

When an optional dependency lifecycle script fails, bun will now ignore the error and continue with the installation. Additionally, the directory will be deleted from `node_modules` to prevent unexpected errors from using a half-installed package.

Fixed thanks to [@dylan-conway](https://github.com/dylan-conway)!

## [Fixed: JSX symbol collisions](https://bun.com/blog/bun-v1.1.33#fixed-jsx-symbol-collisions)

A bug was fixed where imports sharing the same name as a JSX symbol would cause bun to fail to include the JSX import source in the transpiled output, resulting in a reference error. For example, running tests in the [`hono`](https://github.com/honojs/hono) repository:

```
bun test runtime-tests/bun/index.test.tsx
```

```
✗ JSX Middleware > Should return rendered HTML with Layout [0.12ms]
254 |     app.post('/about/some/thing', (c) => c.text('About Page 3tier'))
255 |     app.get('/bravo', (c) => c.html('Bravo Page'))
256 |     app.get('/Charlie', async (c, next) => {
257 |       c.setRenderer((content, head) => {
258 |         return c.html(
259 |           <html>
                ^
ReferenceError: Can't find variable: jsx
      at /Users/dylan/code/hono/runtime-tests/bun/index.test.tsx:259:11
      at /Users/dylan/code/hono/src/compose.ts:74:23
```

Fixed thanks to [@snoglobe](https://github.com/snoglobe)!

## [Fixed: assertion failure in the CSS parser](https://bun.com/blog/bun-v1.1.33#fixed-assertion-failure-in-the-css-parser)

A hashing function in the CSS parser was casting a `u64` to a `u32` without telling zig safety checks to ignore truncating non-zero bits. This was fixed by using the `@truncate` zig builtin function.

## [Single quotes in module resolution error messages](https://bun.com/blog/bun-v1.1.33#single-quotes-in-module-resolution-error-messages)

When bun fails to resolve a module or package, the error message has been changed to use single quotes instead of double quotes. This fixes the [`optional-require`](https://www.npmjs.com/package/optional-require) package, which checks for the package name surrounded by single quotes.

index.js

```
require('does-not-exist');
// before: Cannot find package "does-not-exist" from "/path/to/index.js"
// after:  Cannot find package 'does-not-exist' from '/path/to/index.js'
```

Fixed thanks to [@nektro](https://github.com/nektro)!

## [Thanks to 10 contributors!](https://bun.com/blog/bun-v1.1.33#thanks-to-10-contributors)

* [@CanadaHonk](https://github.com/CanadaHonk)
* [@cirospaciari](https://github.com/cirospaciari)
* [@dylan-conway](https://github.com/dylan-conway)
* [@Eckhardt-D](https://github.com/Eckhardt-D)
* [@Electroid](https://github.com/Electroid)
* [@Jarred-Sumner](https://github.com/Jarred-Sumner)
* [@lirantal](https://github.com/lirantal)
* [@Nanome203](https://github.com/Nanome203)
* [@nektro](https://github.com/nektro)
* [@snoglobe](https://github.com/snoglobe)

---

[#### Bun v1.1.32](https://bun.com/blog/bun-v1.1.32)[#### Bun v1.1.34](https://bun.com/blog/bun-v1.1.34)