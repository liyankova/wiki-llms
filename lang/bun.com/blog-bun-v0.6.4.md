---
url: https://bun.com/blog/bun-v0.6.4
title: Bun v0.6.4 | Bun Blog
source_domain: bun.com
---

# Bun v0.6.4 | Bun Blog

# Bun v0.6.4

---

[Ashcon Partovi](https://twitter.com/ashconpartovi) · May 26, 2023

We're hiring C/C++ and Zig engineers to build the future of JavaScript! [Join our team →](https://bun.com/careers)

Last week, we launched our new JavaScript [bundler](https://bun.com/blog/bun-bundler) in Bun [v0.6.0](https://bun.com/blog/bun-v0.6.0).

Today, we're releasing improvements to `bun test`, Node.js compatibility bugfixes, console.log() improvements, modifiable timezone, require.cache support, bundler bugfixes and more.

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

## [Up to 80% faster `bun test`](https://bun.com/blog/bun-v0.6.4#up-to-80-faster-bun-test)

We've made `bun test` up to 80% faster, particularly when there are lots of small test files.

> bun:test just got 80% faster (in a benchmark rendering React components) [pic.twitter.com/BJTW0VqakQ](https://t.co/BJTW0VqakQ)
>
> — Jarred Sumner (@jarredsumner) [May 23, 2023](https://twitter.com/jarredsumner/status/1660915929893711872?ref_src=twsrc%5Etfw)

Bun was over-scheduling the garbage collector to run on every file synchronously. It already schedules GC whenever the heap size changes, so this is unnecessary. This resulted in a 9% growth in memory usage, or so, which is fine given that comparing other test runners with the same code, Bun uses 2-4x less memory.

## [bun test reads `.env.test` and `.env.test.local`](https://bun.com/blog/bun-v0.6.4#bun-test-reads-env-test-and-env-test-local)

* `NODE_ENV=test` is now properly set.
* Environment variables can be read from `.env.test` and `.env.test.local` files.

> In the next version of Bun  
>   
> "bun test" sets NODE\_ENV=test by default and loads .env.test & .env.test.local [pic.twitter.com/VuxMUmppxR](https://t.co/VuxMUmppxR)
>
> — Jarred Sumner (@jarredsumner) [May 23, 2023](https://twitter.com/jarredsumner/status/1661141664482873344?ref_src=twsrc%5Etfw)

## [bun test timeouts](https://bun.com/blog/bun-v0.6.4#bun-test-timeouts)

You can now set a timeout for your tests by passing `--timeout` or by passing a third optional `number` argument to `test()`.

```
import { test } from "bun:test";

test("i took too long", async () => {
  await Bun.sleep(100);

  // the last argument is a timeout in milliseconds
}, 50);
```

## [expect().toHaveLength() and expect().toBeEmpty()](https://bun.com/blog/bun-v0.6.4#expect-tohavelength-and-expect-tobeempty)

expect().toHaveLength() and expect().toBeEmpty() are now supported. These test matchers are available on Blob, Buffer, File, Headers, Map, Set, String, TypedArray, and Array-like objects.

```
import { expect, test } from "bun:test";

test("expect().toHaveLength()", () => {
  expect([1, 2, 3]).toHaveLength(3);
  expect([1, 2, 3]).not.toHaveLength(2);

  // Works on Blob, Buffer, File, Headers, Map, Set, String, TypedArray, and Array-like objects, or anything with a .length property
  expect(new Headers({ Origin: "https://bun.sh" })).toHaveLength(1);
});

test("expect().toBeEmpty()", () => {
  expect([]).toBeEmpty();
  expect([1]).not.toBeEmpty();

  // Works on Bun.file() too
  expect(Bun.file(import.meta.path)).not.toBeEmpty();
});
```

[View on Twitter](https://twitter.com/jarredsumner/status/1662004228267868161)

## [Change the timezone](https://bun.com/blog/bun-v0.6.4#change-the-timezone)

You can now change the [timezone](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones#List) that Bun uses for `Date` and `Intl` by setting `TZ` environment variable or assigning `process.env.TZ` in your code. This is also used by Node.js.

```
process.env.TZ = "America/New_York";
```

When using `bun test`, instead of using your machine's timezone, the default timezone is set to `Etc/UTC` to help prevent flaky tests when running in your CI environment.

[View on Twitter](https://twitter.com/jarredsumner/status/1660887638948335617)

## [Implemented `require.cache`](https://bun.com/blog/bun-v0.6.4#implemented-require-cache)

`require.cache` is a Node.js API that allows you to delete a module from the cache. This is useful for controlling hot reloading behavior, and is now supported in Bun. Unlike Node.js, `delete require.cache[id]` works with ESM too.

> In the next version of Bun  
>   
> delete require.cache[id] works on ESM [pic.twitter.com/xVKYwkVhLy](https://t.co/xVKYwkVhLy)
>
> — Jarred Sumner (@jarredsumner) [May 24, 2023](https://twitter.com/jarredsumner/status/1661256052254597120?ref_src=twsrc%5Etfw)

## [console.log(headers) shows headers](https://bun.com/blog/bun-v0.6.4#console-log-headers-shows-headers)

> in the next version of Bun   
>   
> console.log(headers) shows the headers [pic.twitter.com/RKiBNlffFs](https://t.co/RKiBNlffFs)
>
> — Jarred Sumner (@jarredsumner) [May 26, 2023](https://twitter.com/jarredsumner/status/1662048123584405506?ref_src=twsrc%5Etfw)

## [console.log(searchParams) shows params](https://bun.com/blog/bun-v0.6.4#console-log-searchparams-shows-params)

> in the next version of Bun   
>   
> console.log(headers) shows the headers [pic.twitter.com/RKiBNlffFs](https://t.co/RKiBNlffFs)
>
> — Jarred Sumner (@jarredsumner) [May 26, 2023](https://twitter.com/jarredsumner/status/1662048123584405506?ref_src=twsrc%5Etfw)

## [Bundler bugfixes](https://bun.com/blog/bun-v0.6.4#bundler-bugfixes)

Thanks to [@dylan-conway](https://github.com/dylan-conway) for fixing:

* Bun was auto-importing JSX when using the "classic" JSX runtime, which is incorrect.
* Bun was not importing `Fragment` from `jsxImportSource` when using the "automatic" JSX runtime.
* Bun was incorrectly choosing the "production" JSX runtime when using `jsxImportSource` and `NODE_ENV=development` (or unset) in certain case.

## [Transpiler bugfixes](https://bun.com/blog/bun-v0.6.4#transpiler-bugfixes)

* A regression related to printing tagged template literals containing non-ascii characters when running in Bun's runtime has been fixed.

## [Node.js compatiblity bugfixes](https://bun.com/blog/bun-v0.6.4#node-js-compatiblity-bugfixes)

* `node:https` now uses the correct port when using `node:https` and `port` is not set. Thanks to [@cirospaciari](https://github.com/cirospaciari) for the fix.
* `node:http` now has the correct return type for `getHeader()`. Thanks to [@Jarred-Sumner](https://github.com/Jarred-Sumner) for the fix.
* `node:https` now correctly uses `{ tls: true }` when using `createServer()`. Thanks to [@cirospaciari](https://github.com/cirospaciari) for the fix.

## [bun install bugfixes](https://bun.com/blog/bun-v0.6.4#bun-install-bugfixes)

* A bug that could cause bun to fail to symlink binaries into `node_modules/.bin` has been fixed, thanks to [@alexlamsl](https://github.com/alexlamsl).

## [Rewrote JavaScript builtins in TypeScript](https://bun.com/blog/bun-v0.6.4#rewrote-javascript-builtins-in-typescript)

Bun's internal JavaScript builtins are now implemented in TypeScript and bundled + minified with `bun build`, which reduces Bun's binary size by about 900 KB and makes it easier for us to catch bugs. This is thanks to [@paperclover](https://github.com/paperclover).

It also improves Bun's development velocity on these JavaScript builtins because the previous builtins generator script used by WebKit takes around 9s to run and this new builtins generator script takes around 0.9s.

## [Changelog](https://bun.com/blog/bun-v0.6.4#changelog)

| [`#3008`](https://github.com/oven-sh/bun/pull/3008) | Fixed port for HTTPS when using `node:https` by [@cirospaciari](https://github.com/cirospaciari) |
| [`#3007`](https://github.com/oven-sh/bun/pull/3007) | Fixed return type of `getHeader()` in `node:http` by [@Jarred-Sumner](https://github.com/Jarred-Sumner) |
| [`#3012`](https://github.com/oven-sh/bun/pull/3012) | Fixed `{ tls: true }` when using `createServer()` by [@cirospaciari](https://github.com/cirospaciari) |
| [`#3018`](https://github.com/oven-sh/bun/pull/3018) | Implemented `process.env.TZ` and changed the default timezone of `bun test` to Etc/UTC by [@Jarred-Sumner](https://github.com/Jarred-Sumner) |
| [`#3015`](https://github.com/oven-sh/bun/pull/3015) | Fixed a bug with `test.todo()` and async functions by [@Jarred-Sumner](https://github.com/Jarred-Sumner) |
| [`f71eb39`](https://github.com/oven-sh/bun/commit/f71eb39b14b0177c178d68d86e1ba11f227044af) | Reduced aggresiveness of garbage collection during `bun test` by [@Jarred-Sumner](https://github.com/Jarred-Sumner) |
| [`#3032`](https://github.com/oven-sh/bun/pull/3032) | Fixed a bug where `module.exports` had a key with a space by [@dylan-conway](https://github.com/dylan-conway) |
| [`#3040`](https://github.com/oven-sh/bun/pull/3040) | Implemented `bun test --timeout N` that can change the default per-test timeout by [@Electroid](https://github.com/Electroid) |
| [`#3045`](https://github.com/oven-sh/bun/pull/3045) | Implemented `require.cache` by [@Jarred-Sumner](https://github.com/Jarred-Sumner) |
| [`#3041`](https://github.com/oven-sh/bun/pull/3041) | Fixed a bug with emojis in tagged template literals by [@Jarred-Sumner](https://github.com/Jarred-Sumner) |
| [`#3057`](https://github.com/oven-sh/bun/pull/3057) | Fixed various bugs with `jsxImportSource`, `jsxFactory`, and `jsxFragmentFactory` by [@dylan-conway](https://github.com/dylan-conway) |
| [`#3051`](https://github.com/oven-sh/bun/pull/3051) | Fixed crash when using `server.fetch(Request)` by [@cirospaciari](https://github.com/cirospaciari) |
| [`#3037`](https://github.com/oven-sh/bun/pull/3037) | Implemented support to load `.env.test` and `.env.{test,production,development}.local` by [@Jarred-Sumner](https://github.com/Jarred-Sumner) |

---

[#### Bun v0.6.3](https://bun.com/blog/bun-v0.6.3)[#### Bun v0.6.5](https://bun.com/blog/bun-v0.6.5)