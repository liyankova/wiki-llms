---
url: https://bun.com/blog/bun-v0.7.2
title: Bun v0.7.2 | Bun Blog
source_domain: bun.com
---

# Bun v0.7.2 | Bun Blog

# Bun v0.7.2

---

[Jarred Sumner](https://twitter.com/jarredsumner) · August 3, 2023

Bun v0.7.2 adds support for `node:worker_threads`, `node:diagnostics_channel`, [`BroadcastChannel`](https://developer.mozilla.org/en-US/docs/Web/API/BroadcastChannel), improves compatibility with Node.js, and fixes a couple nasty memory leaks.

We're hiring C/C++ and Zig engineers to build the future of JavaScript! [Join our team →](https://bun.com/careers)

Bun is an incredibly fast JavaScript runtime, bundler, transpiler, and package manager — all in one. Over the past couple months, we've been releasing a lot of changes to Bun recently, here's a recap in case you missed it:

* [`v0.6.12`](https://bun.com/blog/bun-v0.6.12) - Sourcemap support in `Error.stack`, `Bun.file().exists()`, and Node.js bug fixes.
* [`v0.6.13`](https://bun.com/blog/bun-v0.6.13) - Implemented mock `Date`, faster base64 encoding, and fixes for `WebSocket` and `node:tls`.
* [`v0.6.14`](https://bun.com/blog/bun-v0.6.14) - `process.memoryUsage()`, `process.cpuUsage()`, `process.on('beforeExit', cb)`, `process.on('exit', cb)` and crash fixes
* [`v0.7.0`](https://bun.com/blog/bun-v0.7.0) - Web Workers, --smol, structuredClone(), WebSocket reliability improvements, node:tls fixes, and more.
* [`v0.7.1`](https://bun.com/blog/bun-v0.7.1) - ES Modules load 30% - 250% faster, fs.watch fixes, and lots of node:fs compatibility improvements.

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

## [Node.js worker\_threads](https://bun.com/blog/bun-v0.7.2#node-js-worker-threads)

You can now use the `node:worker_threads` module in Bun. `Worker` remains a global variable, but you can now use packages & frameworks that depend on `node:worker_threads` in Bun.

```
import { Worker } from "node:worker_threads";

const worker = new Worker("./worker.js");
```

## [`bun .` - run the main file](https://bun.com/blog/bun-v0.7.2#bun-run-the-main-file)

You can now run a project in Bun with `bun .` when you don't want to type out a path to a file. It is equivalent to doing `import '.'`

```
bun .
```

## [BroadcastChannel](https://bun.com/blog/bun-v0.7.2#broadcastchannel)

The [`BroadcastChannel`](https://developer.mozilla.org/en-US/docs/Web/API/BroadcastChannel) API is now available in Bun. It allows you to publish-subscribe to messages across multiple `Worker` threads and the main thread. This is a new global variable, so you can use it without importing anything just like in web browsers.

```
const channel = new BroadcastChannel("my-channel");
const message = { hello: "world" };

channel.onmessage = (event) => {
  console.log(event.data); // { hello: "world" }
};
channel.postMessage(message);
```

Thanks to [@dylan-conway](https://github.com/dylan-conway) for getting this working in Bun and the WebKit/Safari team for the original implementation.

## [postMessage() now supports `Error`](https://bun.com/blog/bun-v0.7.2#postmessage-now-supports-error)

You can now use `postMessage` and `structuredClone()` to clone `Error` objects.

```
const error = new Error("hello world");
const clone = structuredClone(error);
console.log(clone.message); // "hello world"
```

## [Node.js `node:diagnostics_channel` support](https://bun.com/blog/bun-v0.7.2#node-js-node-diagnostics-channel-support)

You can now use the `node:diagnostics_channel` module in Bun. The node:diagnostics\_channel module provides an API to create named channels to report arbitrary message data for diagnostics purposes.

## [Creating new TypedArray gets up to 40x faster](https://bun.com/blog/bun-v0.7.2#creating-new-typedarray-gets-up-to-40x-faster)

> In the next version of Bun  
>   
> Creating large new typed arrays gets up to 40x faster, thanks to [@Constellation](https://twitter.com/Constellation?ref_src=twsrc%5Etfw) [pic.twitter.com/PRvKsVh7GE](https://t.co/PRvKsVh7GE)
>
> — Jarred Sumner (@jarredsumner) [August 3, 2023](https://twitter.com/jarredsumner/status/1687023208548241408?ref_src=twsrc%5Etfw)

## [Module resolution change: `browser` and `module` exports conditions](https://bun.com/blog/bun-v0.7.2#module-resolution-change-browser-and-module-exports-conditions)

Bun no longer respects the `"browser"` or `"module"` package.json `"exports"` conditions. This addresses bugs impacting Astro CLI, axios, and more.

* Bun is not a web browser, so Bun should not use the `"browser"` package.json exports condition.
* The `"module"` exports condition is used by older versions of tslib and that breaks packages which rely on tslib. We still support this in `bun build`, but not at runtime.

The list of package.json `"exports"` conditions Bun respects at runtime is now as follows:

* `"bun"`
* `"worker"`
* `"node"`
* `"default"`

When coming from an ES module, `"import"` is used and when coming from a CommonJS module, `"require"` is used as well.

This is technically a breaking change, but it will usually be more of a "fixing" change.

## [2 memory leaks fixed](https://bun.com/blog/bun-v0.7.2#2-memory-leaks-fixed)

A memory leak in strong references held by native code in Bun has been fixed. This is a leak of about 16 bytes, however it quickly adds up in long-running processes.

> fixes a memory leak in fetch, Bun.spawn, napi, Bun.write, Bun.connect, Bun.listen, streams... [pic.twitter.com/FqhSg4HTZy](https://t.co/FqhSg4HTZy)
>
> — Jarred Sumner (@jarredsumner) [July 30, 2023](https://twitter.com/jarredsumner/status/1685481593862004737?ref_src=twsrc%5Etfw)

A memory leak in `response.clone()` has been fixed. The headers object was cloned twice.

> fixed a memory leak in response.clone() [pic.twitter.com/6c37kllgWC](https://t.co/6c37kllgWC)
>
> — Jarred Sumner (@jarredsumner) [July 31, 2023](https://twitter.com/jarredsumner/status/1685890215775436800?ref_src=twsrc%5Etfw)

## [Bugfixes](https://bun.com/blog/bun-v0.7.2#bugfixes)

We also fixed some bugs

### [`PrintingErrorWriteFailed` bug fixed](https://bun.com/blog/bun-v0.7.2#printingerrorwritefailed-bug-fixed)

A regression from the async transpiler changes caused some imports to fail with `PrintingErrorWriteFailed`. This has been fixed.

### [`file` loader bug fix](https://bun.com/blog/bun-v0.7.2#file-loader-bug-fix)

A regression from the async transpiler changes caused `file` loader imports to fail to load unless explicitly passed via `--loader`. This has been fixed.

### [`require('node:module')` is now a `Module` constructor](https://bun.com/blog/bun-v0.7.2#require-node-module-is-now-a-module-constructor)

`require('node:module')` is now a `Module` constructor, as it is in Node.js.

### [`bun install --production` with workspaces](https://bun.com/blog/bun-v0.7.2#bun-install-production-with-workspaces)

A bug causing packages to not be updated in the lockfile when `--production` was used in a workspace has been fixed.

### [node:http file upload bug has been fixed](https://bun.com/blog/bun-v0.7.2#node-http-file-upload-bug-has-been-fixed)

[A bug](https://github.com/oven-sh/bun/issues/3116) where binary file uploads via `node:http` would produce incorrectly-encoded data has been fixed by [@Hanaasagi](https://github.com/Hanaasagi). Thanks @Hanaasagi!

## [Internals changes](https://bun.com/blog/bun-v0.7.2#internals-changes)

We migrated our JavaScript builtins from ES modules to CommonJS, which improves start time for `"crypto"` by about 30% and fixed a crash when importing `"astro"`.

## [Changelog](https://bun.com/blog/bun-v0.7.2#changelog)

[View the complete changelog](https://github.com/oven-sh/bun/compare/bun-v0.7.1...bun-v0.7.2)

---

[#### Bun v0.7.1](https://bun.com/blog/bun-v0.7.1)[#### Bun v0.7.3](https://bun.com/blog/bun-v0.7.3)