---
url: https://bun.com/blog/bun-v0.1.7
title: Bun v0.1.7 | Bun Blog
source_domain: bun.com
---

# Bun v0.1.7 | Bun Blog

# Bun v0.1.7

---

[Jarred Sumner](https://twitter.com/jarredsumner) · August 6, 2022

To upgrade:

```
bun upgrade
```

To install:

```
curl https://bun.sh/install | bash
```

If you have any problems upgrading

Run the install script (you can run it multiple times):

```
curl https://bun.sh/install | bash
```

## [What's new](https://bun.com/blog/bun-v0.1.7#what-s-new)

**`bun init` quickly start a new, empty project that uses Bun** (similar to npm init). `bun init` is a new subcommand in `bun`.

[![](https://user-images.githubusercontent.com/709451/183006613-271960a3-ff22-4f7c-83f5-5e18f684c836.gif)](https://user-images.githubusercontent.com/709451/183006613-271960a3-ff22-4f7c-83f5-5e18f684c836.gif)

**`bun install` now supports private npm registries & scoped (authenticated) packages**

Thank you @soneymathew for your help with this.

[![image](https://user-images.githubusercontent.com/709451/183240854-325123ab-1c32-420b-b227-a68902d416ac.png)](https://user-images.githubusercontent.com/709451/183240854-325123ab-1c32-420b-b227-a68902d416ac.png)

**`bun install` now supports lifecycle hooks for project-level package.json** (not dependencies)

[![image](https://user-images.githubusercontent.com/709451/183240585-f5344dbf-1d9e-40ff-a9a3-f6e089c4dc77.png)](https://user-images.githubusercontent.com/709451/183240585-f5344dbf-1d9e-40ff-a9a3-f6e089c4dc77.png)

It runs postinstall scripts for your app's package.json, but ignores dependencies lifecycle hooks. This lets you use `husky`, `lint-staged`, and other postinstall-dependent packages tools

More new stuff:

* `express` is partially supported, thanks to [@zhuzilin](https://github.com/zhuzilin) and @evanwashere. There is a lot more work to be done - it's not fast yet and it logs a spurious error on request, but it is better than not working
* `bun create` now lets you specify a start command so that you can say how to run the program in the output
* `process.revision` has the git sha that bun was built with

## [Breaking changes](https://bun.com/blog/bun-v0.1.7#breaking-changes)

* bun install will invalidate the lockfiles on upgrade if it exists. Unfortunately, this is necessary to support private/scoped package installs

## [Bug fixes](https://bun.com/blog/bun-v0.1.7#bug-fixes)

* Fix a handful of crashes that occurred in rare cases in Bun.Transpiler, `bun:ffi` and a couple other places thanks to [@sno2](https://github.com/sno2)
* `Buffer.isBuffer` no longer checks that `this` is the `Buffer` constructor
* `Bun.Transpiler` no longer does bun-specific transforms when it shouldn't
* Make internal APIs that iterate through JS objects more reliable @sno2 in https://github.com/oven-sh/bun/pull/974
* Fix u32 jsNumber cast by [@zhuzilin](https://github.com/zhuzilin) in https://github.com/oven-sh/bun/pull/964
* fix import in http polyfill by [@zhuzilin](https://github.com/zhuzilin) in https://github.com/oven-sh/bun/pull/973
* fix path.normalize on ... by [@zhuzilin](https://github.com/zhuzilin) in https://github.com/oven-sh/bun/pull/966
* allow setting status code in Response.redirect by [@zhuzilin](https://github.com/zhuzilin) in https://github.com/oven-sh/bun/pull/985
* Fix for bearer tokens missing from request headers on bun install step by [@soneymathew](https://github.com/soneymathew) in https://github.com/oven-sh/bun/pull/991
* Fix of panic in threads while downloading scoped packages by [@soneymathew](https://github.com/soneymathew) in https://github.com/oven-sh/bun/pull/992
* feat(util): export util.TextDecoder by [@xHyroM](https://github.com/xHyroM) in https://github.com/oven-sh/bun/pull/990
* Fixed bugs in `latin1` and `binary` encodings in Bun's `Buffer` implementation

## [Misc:](https://bun.com/blog/bun-v0.1.7#misc)

* fix(makefile) fix devcontainer rule by [@zhuzilin](https://github.com/zhuzilin) in https://github.com/oven-sh/bun/pull/957
* refactor: create a high-level property iterator by [@sno2](https://github.com/sno2) in https://github.com/oven-sh/bun/pull/972
* fix(makefile): mkdir DEBUG\_OBJ\_DIR before compiling bindings by [@zhuzilin](https://github.com/zhuzilin) in https://github.com/oven-sh/bun/pull/975
* Convert landing page to zero-JS Next.js application. by [@leerob](https://github.com/leerob) in https://github.com/oven-sh/bun/pull/945
* benchmarks(sqlite): invalid northwind database url by [@xHyroM](https://github.com/xHyroM) in https://github.com/oven-sh/bun/pull/989
* Update README for development help by [@JL102](https://github.com/JL102) in https://github.com/oven-sh/bun/pull/982

## [New Contributors](https://bun.com/blog/bun-v0.1.7#new-contributors)

* @zhuzilin made their first contribution in https://github.com/oven-sh/bun/pull/964
* @leerob made their first contribution in https://github.com/oven-sh/bun/pull/945

[**Full Changelog**](https://github.com/oven-sh/bun/compare/bun-v0.1.6...bun-v0.1.7)

---

[#### Bun v0.1.6](https://bun.com/blog/bun-v0.1.6)[#### Bun v0.1.8](https://bun.com/blog/bun-v0.1.8)