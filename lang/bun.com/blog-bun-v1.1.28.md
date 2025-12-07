---
url: https://bun.com/blog/bun-v1.1.28
title: Bun v1.1.28 | Bun Blog
source_domain: bun.com
---

# Bun v1.1.28 | Bun Blog

# Bun v1.1.28

---

[Dylan Conway](https://github.com/dylan-conway) · September 18, 2024

Bun v1.1.28 is here! This release fixes 40 bugs (addressing 51 👍). Compile & run C from JavaScript. 30x faster `path.resolve`. Named pipes on Windows. Several Node.js compatibility improvements and bugfixes.

We're hiring [systems engineers](https://bun.com/careers) in San Francisco to build the future of JavaScript!

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

## [Compile & run C from JavaScript](https://bun.com/blog/bun-v1.1.28#compile-run-c-from-javascript)

Bun now supports compiling and running C from JavaScript. This is a simple way to use native system libraries from JavaScript without adding an extra build step.

Learn more about this feature [here](https://bun.com/blog/compile-and-run-c-in-js).

## [30x faster `path.resolve`](https://bun.com/blog/bun-v1.1.28#30x-faster-path-resolve)

This release makes `path.resolve` 30x faster.

> In the next version of Bun  
>   
> path.resolve() gets 30x faster [pic.twitter.com/ukdAHtK6lT](https://t.co/ukdAHtK6lT)
>
> — Jarred Sumner (@jarredsumner) [September 12, 2024](https://twitter.com/jarredsumner/status/1834353346318401915?ref_src=twsrc%5Etfw)

## [Named pipes on Windows](https://bun.com/blog/bun-v1.1.28#named-pipes-on-windows)

Bun now supports named pipes on Windows in many Node.js & Bun APIs, thanks to [@cirospaciari](https://github.com/cirospaciari)! Named pipes are interesting because they're not exactly files on disk. They're this other thing, sort of like Unix domain sockets but also not.

## [Node.js compatibility improvements](https://bun.com/blog/bun-v1.1.28#node-js-compatibility-improvements)

### [`process._exiting` is set to `false`](https://bun.com/blog/bun-v1.1.28#process-exiting-is-set-to-false)

Previously, `process._exiting` would be set to `undefined` before the `exit` event was emitted. Now, it will be `false`

```
console.log(process._exiting); // Previously: `undefined`, now: `false`

process.on("exit", () => {
  console.log(process._exiting); // true
});
```

### [`workerData` from `worker_threads` defaults to `null`](https://bun.com/blog/bun-v1.1.28#workerdata-from-worker-threads-defaults-to-null)

The default value of `workerData` has been changed from `undefined` to `null`.

```
import { workerData } from "worker_threads";

console.log(workerData); // Previously: `undefined`, now: `null`
```

### [Missing constants from `perf_hooks` have been added](https://bun.com/blog/bun-v1.1.28#missing-constants-from-perf-hooks-have-been-added)

The following constants were previously missing from the `perf_hooks` module:

```
import { constants } from "perf_hooks";
console.log(constants.NODE_PERFORMANCE_MILESTONE_BOOTSTRAP_COMPLETE); // 7
console.log(constants.NODE_PERFORMANCE_MILESTONE_ENVIRONMENT); // 2
console.log(constants.NODE_PERFORMANCE_MILESTONE_LOOP_EXIT); // 6
console.log(constants.NODE_PERFORMANCE_MILESTONE_LOOP_START); // 5
console.log(constants.NODE_PERFORMANCE_MILESTONE_NODE_START); // 3
console.log(constants.NODE_PERFORMANCE_MILESTONE_TIME_ORIGIN_TIMESTAMP); // 0
console.log(constants.NODE_PERFORMANCE_MILESTONE_TIME_ORIGIN); // 1
console.log(constants.NODE_PERFORMANCE_MILESTONE_V8_START); // 4
console.log(constants.NODE_PERFORMANCE_ENTRY_TYPE_DNS); // 4
console.log(constants.NODE_PERFORMANCE_ENTRY_TYPE_GC); // 0
console.log(constants.NODE_PERFORMANCE_ENTRY_TYPE_HTTP); // 1
console.log(constants.NODE_PERFORMANCE_ENTRY_TYPE_HTTP2); // 2
console.log(constants.NODE_PERFORMANCE_ENTRY_TYPE_NET); // 3
```

### [Fixed logic for undefined options provided `node:zlib`](https://bun.com/blog/bun-v1.1.28#fixed-logic-for-undefined-options-provided-node-zlib)

Option handling in `node:zlib` has been fixed, allowing options to be `undefined` without causing an error.

```
import { createGzip } from "zlib";

createGzip({ level: undefined });
```

### [`OutgoingMessage.headersSent` from `node:http` is now set to `true`](https://bun.com/blog/bun-v1.1.28#outgoingmessage-headerssent-from-node-http-is-now-set-to-true)

After headers have been sent, `req.headersSent` will be set to `true`

### [Added `timers.promises`](https://bun.com/blog/bun-v1.1.28#added-timers-promises)

Exports from `node:timers/promises` are now also available in `timers.promises` to better match Node.js.

```
import { promises } from "timers";

console.time("timeout");
await promises.setTimeout(1000);
console.timeEnd("timeout"); // [1002.48ms] test
```

### [Fixed: `cwd` is updated before searching for executables in `node:child_process` before spawning processes](https://bun.com/blog/bun-v1.1.28#fixed-cwd-is-updated-before-searching-for-executables-in-node-child-process-before-spawning-processes)

Previously, Bun would search for executables to spawn in the calling process's `cwd`. If a different `cwd` was provided and a relative path was given for the executable path, the expected executable would fail to be found. Now, Bun will search from the target `cwd`.

```
import { spawnSync } from "child_process";
import { join } from "path";

// This will search for `foo` in `./node_modules/package/bin/`
spawnSync("./bin/foo", { cwd: join(import.meta.dir, "node_modules/package") });
```

### [Fixed: crash in napi escapable handle scopes](https://bun.com/blog/bun-v1.1.28#fixed-crash-in-napi-escapable-handle-scopes)

A bug where `napi` escapable handle scopes could crash Bun has been fixed, thanks to [@190n](https://github.com/190n)!

### [Fixed: crash in napi handle scope finalization](https://bun.com/blog/bun-v1.1.28#fixed-crash-in-napi-handle-scope-finalization)

A bug where a napi finalizer is called and then we attempt to allocate a handle scope has been fixed. This would cause a crash in certain cases in the `sqlite3` package. This was a regression from v1.1.27. Thanks to [@190n](https://github.com/190n) for the fix!

## [More fixes and improvements](https://bun.com/blog/bun-v1.1.28#more-fixes-and-improvements)

### [Fixed an edgecase with `os` and `cpu` fields in `bun install`](https://bun.com/blog/bun-v1.1.28#fixed-an-edgecase-with-os-and-cpu-fields-in-bun-install)

In certain cases, the `os` and `cpu` fields in `bun install` would not handle exclusions properly, leading to always-skipped installs. This has been fixed.

We've also added an extra log message in `bun install --verbose` to make it easier to debug why a package is being skipped.

### [Fixed: IPC through `bun run`](https://bun.com/blog/bun-v1.1.28#fixed-ipc-through-bun-run)

Previously, if you spawned a process that opened `bun run` with IPC enabled, the IPC socket would be closed before the child process could use it. This has been fixed, thanks to [@snoglobe](https://github.com/snoglobe)!

### [Fixed: case-insensitive watch mode on Windows](https://bun.com/blog/bun-v1.1.28#fixed-case-insensitive-watch-mode-on-windows)

On Windows, watch mode would not pick up on changes to case-sensitive files in certain cases. This has been fixed, thanks to [@dylan-conway](https://github.com/dylan-conway)!

### [Fixed: `bun ./bun.lockb` would print env loaded message](https://bun.com/blog/bun-v1.1.28#fixed-bun-bun-lockb-would-print-env-loaded-message)

If you ran `bun ./bun.lockb`, with a `.env` file in the same directory Bun would print a mesasge telling you it loaded the .env file. It shouldn't be loading the .env file, but regardless it also shouldn't be printing a message when it did load the .env file since that's noise when you're just trying to see a yarn.lock printed from the bun.lockb. This has been fixed, thanks to [@snoglobe](https://github.com/snoglobe)!

### [Fixed: Bun.file(path).text() on Windows not reading to end of file sometimes](https://bun.com/blog/bun-v1.1.28#fixed-bun-file-path-text-on-windows-not-reading-to-end-of-file-sometimes)

On Windows, in certain cases, `Bun.file(path).text()` would not read to the end of the file. This has been fixed, thanks to [@190n](https://github.com/190n)!

### [Fixed: React 19 production mode SSR](https://bun.com/blog/bun-v1.1.28#fixed-react-19-production-mode-ssr)

React 19 changed the symbol used for identifying JSX elements. This broke Bun's JSX inlining optimization. To continue to support React 19, we've disabled the optimization for now.

Thanks to [@paperclover](https://github.com/paperclover) for the fix!

### [Fixed: DOMJIT crash with TextDecoder](https://bun.com/blog/bun-v1.1.28#fixed-domjit-crash-with-textdecoder)

A crash that could occur when throwing an exception from a `TextDecoder` has been fixed. DOMJIT is a neat feature in JavaScriptCore that allows us to leverage type information at build-time to call natively-implemented JS functions around 30% faster. We added typed array support to this some time ago, but it has proven to cause crashes in certain cases - so we're disabling it for now and will re-enable it once we make this API more robust.

## [Thanks to 12 contributors!](https://bun.com/blog/bun-v1.1.28#thanks-to-12-contributors)

* [@190n](https://github.com/190n)
* [@cirospaciari](https://github.com/cirospaciari)
* [@DannyJJK](https://github.com/DannyJJK)
* [@dylan-conway](https://github.com/dylan-conway)
* [@Electroid](https://github.com/Electroid)
* [@Jarred-Sumner](https://github.com/Jarred-Sumner)
* [@levabala](https://github.com/levabala)
* [@nektro](https://github.com/nektro)
* [@paperclover](https://github.com/paperclover)
* [@snoglobe](https://github.com/snoglobe)
* [@stilt0n](https://github.com/stilt0n)
* [@wpaulino](https://github.com/wpaulino)

---

[#### Bun v1.1.27](https://bun.com/blog/bun-v1.1.27)[#### Bun v1.1.29](https://bun.com/blog/bun-v1.1.29)