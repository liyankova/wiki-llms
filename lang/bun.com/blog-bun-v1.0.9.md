---
url: https://bun.com/blog/bun-v1.0.9
title: Bun v1.0.9 | Bun Blog
source_domain: bun.com
---

# Bun v1.0.9 | Bun Blog

# Bun v1.0.9

---

[Jarred Sumner](https://twitter.com/jarredsumner) · November 5, 2023

Bun v1.0.9 fixes regressions impacting usage in Vercel & older CPUs, a `Bun.spawn` bug, an edgecase with peer dependency installs, and a JSX transpiler bugfix.

Bun is an incredibly fast JavaScript runtime, bundler, transpiler, and package manager — all in one. In case you missed it, here are some of the recent changes to Bun:

* [`v1.0.0`](https://bun.com/blog/bun-v1.0) - First stable release!
* [`v1.0.1`](https://bun.com/blog/bun-v1.0.1) - Named imports for .json and .toml files, fixes to `bun install`, `node:path`, and `Buffer`
* [`v1.0.2`](https://bun.com/blog/bun-v1.0.2) - Make `--watch` faster and lots of bug fixes
* [`v1.0.3`](https://bun.com/blog/bun-v1.0.3) - `emitDecoratorMetadata` and Nest.js support, fixes for private registries and more
* [`v1.0.4`](https://bun.com/blog/bun-v1.0.4) - `server.requestIP`, virtual modules in runtime plugins, and more
* [`v1.0.5`](https://bun.com/blog/bun-v1.0.5) - Fixed memory leak with `fetch()`, `KeyObject` support in `node:crypto` module, `expect().toEqualIgnoringWhitespace` in `bun:test`, and more
* [`v1.0.6`](https://bun.com/blog/bun-v1.0.6) - Fixes 3 bugs (addressing 85 👍 reactions), implements `overrides` & `resolutions` in `package.json`, and fixes regression impacting Docker usage with Bun
* [`v1.0.7`](https://bun.com/blog/bun-v1.0.7) - Fixes 59 bugs (addressing 78 👍 reactions), implements optional peer dependencies in `bun install`, and makes improvements to Node.js compatibility.
* [`v1.0.8`](https://bun.com/blog/bun-v1.0.8) - Fixes 138 bugs (addressing 257 👍 reactions), makes `require()` use 30% less memory, adds module mocking to `bun test`, fixes more `bun install` bugs

To install Bun:

curl

npm

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

To upgrade Bun:

```
bun upgrade
```

## ["Illegal instruction" and glibc symbol version regression from v1.0.8 is fixed](https://bun.com/blog/bun-v1.0.9#illegal-instruction-and-glibc-symbol-version-regression-from-v1-0-8-is-fixed)

In Bun v1.0.8, we moved our internal build-system from a bespoke 2,000 line `Makefile` to CMake & Ninja. This was to simplify our build system for contributors and to make it easier to build Bun on Windows.

Along the way, there were three regressions:

1. Bun v1.0.8 would crash with an "Illegal instruction" error on older CPUs (e.g. Intel Xeon E5-2670 v1) and some Linux arm64 CPUs. This impacted Docker users and users of older CPUs.
2. Bun v1.0.8 would crash with a "symbol not found" error for those using < glibc 2.28. This impacted Vercel users and users of older Linux distributions.
3. `bun init` would incorrectly print the version number in the `README.md`

These regressions are fixed, but they are embarassing for a post 1.0 product and I am sorry.

Here's what we're doing to prevent this from happening again:

1. We are adding a CI job that runs on a machine with an older CPU to test Bun on older CPUs
2. We are adding a CI job to check the minimum required version of glibc used by Bun's final executable and throw an error if it requests a version that is too new
3. We added a test to ensure `bun init` prints the correct version number in the `README.md`

## [Bun.spawn bugfixes](https://bun.com/blog/bun-v1.0.9#bun-spawn-bugfixes)

This release fixes two bugs in `Bun.spawn`. We've also added more tests to `Bun.spawn`.

### [Fixed: `await spawn(...).exited` sometimes returned a string](https://bun.com/blog/bun-v1.0.9#fixed-await-spawn-exited-sometimes-returned-a-string)

`await child.exited` sometimes returned a string instead of a number. The string was the signal that caused the process to exit.

```
import { spawn } from "bun";

const child = spawn(["sleep", "1"]);
child.kill();
const code = await child.exited;

// Before:
console.log(code); // "SIGHUP"

// After:
console.log(code); // 129
```

Instead of returning a string, `await child.exited` now returns a number. This is consistent with what our TypeScript types declared, what our documentation said, and what bash's exit codes do.

If the process exited normally, it returns `0`. If the process exited due to a signal, it returns `128` + signal number. For example, if the process exited due to `SIGTERM`, it would return `128 + 15 = 143`.

### [Fixed: edgecase causing `await spawn(...).exited` to not resolve](https://bun.com/blog/bun-v1.0.9#fixed-edgecase-causing-await-spawn-exited-to-not-resolve)

An edgecase that could cause `await spawn(...).exited` to not resolve has been fixed.

## [`bun install` peer dependency too many versions bugfix](https://bun.com/blog/bun-v1.0.9#bun-install-peer-dependency-too-many-versions-bugfix)

In this release, we began porting some tests from other package managers to Bun.

One of the tests uncovered an issue where Bun would not re-use a peer dependency's version from the existing project. This is fixed to align with the behavior of npm.

We've also added a warning when a peer dependency's chosen version is incompatible with the version range specified in the `package.json`.

## [JSX transpiler bugfix](https://bun.com/blog/bun-v1.0.9#jsx-transpiler-bugfix)

Either of the following lines of code would previously cause a runtime panic due to an assertion failure:

```
<A key={() => {}} b={class {}} />
<A key={() => {}} b={() => {}} />
```

This is fixed.

The bug was due to special handling of the `key` prop causing the AST nodes to not be visited in the order they were parsed. This bug could occur if the `key` prop created a scope, such as defining a function or class.

Thanks to [@dylan-conway](https://github.com/dylan-conway) for fixing this bug!

---

[#### Bun v1.0.8](https://bun.com/blog/bun-v1.0.8)[#### Bun v1.0.10](https://bun.com/blog/bun-v1.0.10)