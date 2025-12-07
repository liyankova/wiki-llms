---
url: https://bun.com/blog/bun-v0.6.14
title: Bun v0.6.14 | Bun Blog
source_domain: bun.com
---

# Bun v0.6.14 | Bun Blog

# Bun v0.6.14

---

[Ashcon Partovi](https://twitter.com/ashconpartovi) · July 12, 2023

We're hiring C/C++ and Zig engineers to build the future of JavaScript! [Join our team →](https://bun.com/careers)

As a reminder: Bun is an incredibly fast JavaScript runtime, bundler, transpiler, and package manager — all in one.

We've been releasing a lot of changes to Bun recently, here's a recap in case you missed it:

* [`v0.6.0`](https://bun.com/blog/bun-bundler) - Introducing `bun build`, Bun's new JavaScript bundler.
* [`v0.6.2`](https://bun.com/blog/bun-v0.6.2) - Performance boosts: 20% faster `JSON.parse`, up to 2x faster `Proxy` and `arguments`.
* [`v0.6.3`](https://bun.com/blog/bun-v0.6.3) - Implemented `node:vm`, lots of fixes to `node:http` and `node:tls`.
* [`v0.6.4`](https://bun.com/blog/bun-v0.6.4) - Implemented `require.cache`, `process.env.TZ`, and 80% faster `bun test`.
* [`v0.6.5`](https://bun.com/blog/bun-v0.6.5) - Native support for CommonJS modules (*previously, Bun did CJS to ESM transpilation*),
* [`v0.6.6`](https://bun.com/blog/bun-v0.6.6) - `bun test` improvements, including Github Actions support, `test.only()`, `test.if()`, `describe.skip()`, and 15+ more `expect()` matchers; also streaming file uploads using `fetch()`.
* [`v0.6.7`](https://bun.com/blog/bun-v0.6.7) - Node.js compatibility improvements to unblock Discord.js, Prisma, and Puppeteer
* [`v0.6.8`](https://bun.com/blog/bun-v0.6.8) - Introduced `Bun.password`, mocking in `bun test`, and `toMatchObject()`
* [`v0.6.9`](https://bun.com/blog/bun-v0.6.9) - Less memory usage and support for non-ascii filenames
* [`v0.6.10`](https://bun.com/blog/bun-v0.6.10) - `fs.watch()`, `bun install` bug fixes, `bun test` features, and improved CommonJS support
* [`v0.6.11`](https://bun.com/blog/bun-v0.6.10) - Addressed a release build issue from `v0.6.10`.
* [`v0.6.12`](https://bun.com/blog/bun-v0.6.12) - Sourcemap support in `Error.stack`, `Bun.file().exists()`, and Node.js bug fixes.
* [`v0.6.13`](https://bun.com/blog/bun-v0.6.13) - Implemented mock `Date`, faster base64 encoding, and fixes for `WebSocket` and `node:tls`.

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

## [Better support for `process`](https://bun.com/blog/bun-v0.6.14#better-support-for-process)

Bun has improved support for the Node.js [`process`](https://nodejs.org/api/process.html) object.

### [Memory usage](https://bun.com/blog/bun-v0.6.14#memory-usage)

You can now use [`process.memoryUsage()`](https://nodejs.org/api/process.html#processmemoryusage) to get the memory usage of Bun's process.

```
console.log(process.memoryUsage());
// {
//  rss: 4935680,
//  heapTotal: 1826816,
//  heapUsed: 650472,
//  external: 49879,
//  arrayBuffers: 9386
// }
```

### [CPU usage](https://bun.com/blog/bun-v0.6.14#cpu-usage)

You can also get the current CPU usage from Bun using [`process.cpuUsage()`](https://nodejs.org/api/process.html#processcpuusagepreviousvalue).

```
console.log(process.cpuUsage());
// {
//  user: 38579,
//  system: 6986
// }
```

### [Signal events](https://bun.com/blog/bun-v0.6.14#signal-events)

You can now use [`process.on()`](https://nodejs.org/api/process.html#signal-events) to listen and run code when the process receives a signal event.

```
process.on("SIGINT", () => {
  console.log("Interrupt from keyboard");
});
```

### [Exit events](https://bun.com/blog/bun-v0.6.14#exit-events)

If you don't know which signal to listen for, you can also listen for a generic [`exit`](https://nodejs.org/api/process.html#event-exit) or [`beforeExit`](https://nodejs.org/api/process.html#event-beforeexit) event.

```
process.on("beforeExit", (code) => {
  console.log("Event loop is empty and no work is left to schedule.", code);
});

process.on("exit", (code) => {
  console.log("Exiting with code:", code);
});
```

### [process.kill](https://bun.com/blog/bun-v0.6.14#process-kill)

You can now use `process.kill(pid, signal)`, which kills a process by pid.

```
process.kill(123, "SIGTERM");
```

### [getuid, geteuid, getgid, getegid, getgroups](https://bun.com/blog/bun-v0.6.14#getuid-geteuid-getgid-getegid-getgroups)

The following methods have been added:

* `process.getegid()`
* `process.geteuid()`
* `process.getgid()`
* `process.getgroups()`
* `process.getuid()`

### [`process.assert`](https://bun.com/blog/bun-v0.6.14#process-assert)

`process.assert()` is a deprecated alternative to `require("assert")`. Bun adds this deprecated function for compatibility with existing npm packages.

```
process.assert(false, "PleAsE don't Use THIs It IS dEpReCATED");
```

### [`process.reallyExit`](https://bun.com/blog/bun-v0.6.14#process-reallyexit)

`process.reallyExit()` is used by some npm packages to exit without triggering the `"exit"` event handler. This is an undocumented function which Bun now implements for ecosystem compatibility reasons.

```
process.reallyExit(); // probably just use process.exit() though
```

## [Class constructors in `console.log`](https://bun.com/blog/bun-v0.6.14#class-constructors-in-console-log)

Previously, when a value was printed to `console.log`, a class would was mis-categorized as a function. This has now been fixed and shows that the value is a class.

```
console.log(class A {});
// Previous: [Function: A]
// Now: [class A]
```

## [Fixed TypeScript decorator bug](https://bun.com/blog/bun-v0.6.14#fixed-typescript-decorator-bug)

Previously, Bun had a bug where decorators were not evaluated when used on an anonymous default export. This has been [fixed](https://github.com/oven-sh/bun/pull/3578).

```
function decorator(target: unknown, propertyKey: unknown) {
  // ...
}

export default class {
  @decorator
  method() {
    // ...
  }
}
```

## [Fixed fetch in URLs without slash](https://bun.com/blog/bun-v0.6.14#fixed-fetch-in-urls-without-slash)

Previously, Bun would throw an error when a URL used in [`fetch()`](https://developer.mozilla.org/en-US/docs/Web/API/fetch) did not have a slash. This has been [fixed](https://github.com/oven-sh/bun/pull/3547).

```
await fetch("http://example.com?a=b");
// Previous: <throw>
// Now: Response { ... }
```

## [Fixed 2 crashes in Error.captureStackTrace](https://bun.com/blog/bun-v0.6.14#fixed-2-crashes-in-error-capturestacktrace)

We've added a small stress test for Error.captureStackTrace and that led to fixing two crashes:

* When the sourceURL of a stack frame was empty and Error.captureStackTrace() was called, incorrectly initialized memory could sometimes be passed to the stack trace sourcemapper. This has been fixed.
* Creating the array of `CallSite` objects could sometimes cause a crash due to creating an Array using the fast path which prohbits additional GC-owned memory allocations until the Array has been fully initialized. Since the `CallSite` objects are each a GC-owned allocation, this could cause a crash when GC happens while creating these (suhc as when called repeatedly in a loop). This has been fixed.

## [Implemented `throwIfNoEntry`](https://bun.com/blog/bun-v0.6.14#implemented-throwifnoentry)

[Implemented](https://github.com/oven-sh/bun/commit/854ddaa909a97c0317ec29682f6c6635818d7b9e) support for the `throwIfNoEntry` option for [`stat`](https://nodejs.org/api/fs.html#fsstatsyncpath-options) and [`lstat`](https://nodejs.org/api/fs.html#fslstatsyncpath-options) in `node:fs`. If set to false and the file does not exist, it will return undefined instead of throwing an error.

```
import { statSync } from "node:fs";

statSync("./does-not-exist.txt"); // <throws>
statSync("./does-not-exist.txt", { throwIfNoEntry: false }); // undefined
```

## [Other changes](https://bun.com/blog/bun-v0.6.14#other-changes)

* [Implemented](https://github.com/oven-sh/bun/pull/3598) [`getCurves()`](https://nodejs.org/api/crypto.html#cryptogetcurves) in `node:crypto`
* [Added](https://github.com/oven-sh/bun/pull/3553) support for obscure HTTP methods.
* [Fixed](https://github.com/oven-sh/bun/commit/9c374eac96779aa1c217f53c4d781fc5c8add938) a bug that caused `bun build` to non-deterministically rename symbols.
* [Fixed](https://github.com/oven-sh/bun/pull/3600) an off-by-one error that could cause stack traces show the wrong preview.
* [Fixed](https://github.com/oven-sh/bun/pull/3475) a bug where the `readable` event was being emitted after a stream was destroyed.
* [Fixed](https://github.com/oven-sh/bun/pull/3587) a bug where `digest("binary")` was not implemented properly.
* [Fixed](https://github.com/oven-sh/bun/pull/3556) bad coercion from large numbers and BigInt in `node:fs`.
* [Fixed](https://github.com/oven-sh/bun/pull/3543) the `connection` event from being emitted when it shouldn't.
* [Fixed](https://github.com/oven-sh/bun/pull/3522) a bug in `HTMLRewriter` where `element.attributes` used the wrong encoding.
* [Fixed](https://github.com/oven-sh/bun/pull/3523) a bug where the JIT from [`Buffer.isBuffer()`](https://nodejs.org/api/buffer.html) would become invalid.
* [Fixed](https://github.com/oven-sh/bun/pull/3539) a regression for React support where the bundle size was larger than in previous releases.
* [Fixed](https://github.com/oven-sh/bun/pull/3526) a bug where `ref()` and `unref()` did not return the [`Timer`](https://nodejs.org/dist/latest-v20.x/docs/api/timers.html#timeoutref) object.
* [Fixed](https://github.com/oven-sh/bun/pull/3583) a bug where the metadata bits from [`randomUUID()`](https://developer.mozilla.org/en-US/docs/Web/API/Crypto/randomUUID) were incorrect.
* [Fixed](https://github.com/oven-sh/bun/pull/3563) a crash from invalid utf-8 data in `node:string_decoder`.
* [Fixed](https://github.com/oven-sh/bun/commit/fd4c8fb871c12157f64b4d6297614dcc8f571ddd) a [bug](https://github.com/oven-sh/bun/issues/3585) where `Set-Cookie` was not present in `express-session` because of a monkey-patch. (Thanks to [@Hanaasagi](https://github.com/Hanaasagi) for fixing those last three bugs!)

## [Changelog](https://bun.com/blog/bun-v0.6.14#changelog)

[See the changelog on GitHub](https://github.com/oven-sh/bun/compare/bun-v0.6.13...bun-v0.6.14)

---

[#### Bun v0.6.13](https://bun.com/blog/bun-v0.6.13)