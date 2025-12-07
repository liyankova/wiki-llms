---
url: https://bun.com/blog/bun-v1.1.6
title: Bun v1.1.6 | Bun Blog
source_domain: bun.com
---

# Bun v1.1.6 | Bun Blog

# Bun v1.1.6

---

[Jarred Sumner](https://twitter.com/jarredsumner) · April 28, 2024

Bun is an incredibly fast JavaScript runtime, bundler, transpiler, and package manager — all in one.

Bun v1.1.6 is here! This release fixes 10 bugs (addressing 512 👍 reactions). We've implemented UDP socket support & `node:dgram`. DataDog and ClickHouseDB now work. We've fixed a regression in `node:http` from v1.1.5. There are also Node.js compatibility improvements and bugfixes.

We're hiring [systems engineers](https://bun.com/careers) in San Francisco to build the future of JavaScript!

#### Previous releases

* [`v1.1.5`](https://bun.com/blog/bun-v1.1.5) fixes 64 bugs (addressing 101 👍). bun build --compile cross-compile standalone JavaScript & TypeScript executables to other platforms. import any file as text via the `type: "text"` import attribute. Introduces a new crash reporter. `package.json` doesn't error with comments or trailing commas. Fixes a bug where `bun run --filter` exited with 0. Fixes a bug in bun install with file: dependencies. Fixes bugs in `node:fs`, `node:tls`, `node:crypto`, `node:readline`, `node:http`, `node:worker_threads`
* [`v1.1.4`](https://bun.com/blog/bun-v1.1.4) fixes 40 bugs (addressing 84 👍 reactions). `bun run --filter <workspace> <script>` lets you run multiple workspace scripts in parallel. Reinstalls get up to 50% faster in bun install. Important reliability fixes to bun install. bun:sqlite supports `using` for resource cleanup and has a few bugfixes. Memory leak impacting Next.js Standalone & Web Streams is fixed. Node.js compatibility improvements `fs` and `child_process`. Fix for "Connection closed" in fetch(). A few bugfixes for Bundows.
* [`v1.1.0`](https://bun.com/blog/bun-v1.1) Bundows. Windows support is here!

#### To install Bun:

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

#### To upgrade Bun:

```
bun upgrade
```

## [UDP Sockets](https://bun.com/blog/bun-v1.1.6#udp-sockets)

Bun now supports UDP sockets. UDP sockets are a low-level unreliable messaging protocol, often used by production monitoring tools, video/audio streaming tools, and games.

```
import { udpSocket } from "bun";
const server = await udpSocket({
  socket: {
    data(socket, buf, port, addr) {
      console.log(`message from ${addr}:${port}:`);
      console.log(buf.toString());
    },
  },
});

const client = await udpSocket({});
client.send("Hello!", server.port, "127.0.0.1");
```

Thanks to [@gvilums](https://github.com/gvilums) for implementing UDP socket soupport in Bun!

## [node:dgram is implemented](https://bun.com/blog/bun-v1.1.6#node-dgram-is-implemented)

`node:dgram` is the Node.js module for using UDP sockets. Building on top of Bun's new UDP socket support, `node:dgram` is now implemented. This was one of the most upvoted issues on Bun's GitHub repository.

send-10-messages.js

```
const dgram = require("dgram");
let count = 0;
const { promise, resolve } = Promise.withResolvers();

const server = dgram.createSocket("udp4");
server.on("message", (msg, {port, address}) => {
  console.log(`server got: ${msg} from ${address}:${port}`);
  if (count++ === 9) process.exit(0);
});
server.bind(41234);

const client = dgram.createSocket("udp4");
for (let i = 0; i < 10; i++) {
  client.send("hello", 41234, "127.0.0.1");
}
await promise;
```

Thanks to [@gvilums](https://github.com/gvilums) for implementing `node:dgram` in Bun!

## [DataDog in Bun](https://bun.com/blog/bun-v1.1.6#datadog-in-bun)

DataDog's `dd-trace` module now works in Bun. DataDog is a popular infrastructure monitoring tool.

> In the next version of Bun[@datadoghq](https://twitter.com/datadoghq?ref_src=twsrc%5Etfw) + express seems to work [pic.twitter.com/szOIDs4fsc](https://t.co/szOIDs4fsc)
>
> — Bun (@bunjavascript) [April 27, 2024](https://twitter.com/bunjavascript/status/1784104050935644483?ref_src=twsrc%5Etfw)

Thanks to [@gvilums](https://github.com/gvilums) and @paperclover for getting DataDog to work in Bun!

## [ClickHouse in Bun](https://bun.com/blog/bun-v1.1.6#clickhouse-in-bun)

The official Node.js client for ClickHouse now works in Bun.

> In the next version of Bun  
>   
> ClickHouse works [pic.twitter.com/tT58vaDkUb](https://t.co/tT58vaDkUb)
>
> — meghan 🌻 (@nektro) [April 27, 2024](https://twitter.com/nektro/status/1784092005850906927?ref_src=twsrc%5Etfw)

Thanks to [@nektro](https://github.com/nektro) for getting ClickHouse to work in Bun!

## [SvelteKit in Bun](https://bun.com/blog/bun-v1.1.6#sveltekit-in-bun)

A bug impacting `fetch` when used with SvelteKit has been fixed.

When `fetch` was called with a `Request` subclass, Bun would skip calling the `method` or `url` getters and instead use the internal `method` and `url` properties. Since `SvelteKit`'s `Request` subclass overrides these properties, this meant we ignored the `method` property from the `Request` subclass.

```
class FooRequest extends Request {
  get method() {
    return "POST";
  }
}

await fetch(new FooRequest("https://example.com"));
// This would be a GET request instead of a POST request!
```

This bug has now been fixed, and our test suite has been updated to prevent regressions.

## [Array#sort gets 15% - 135% faster](https://bun.com/blog/bun-v1.1.6#array-sort-gets-15-135-faster)

This release upgrades to the latest version of JavaScriptCore, and `Array.prototype.sort` is now 15% - 135% faster in Bun & Safari. Thanks to [@Constellation](https://github.com/Constellation).

```
❯ bun array-sort.mjs # New
cpu: Apple M3 Max
runtime: bun 1.1.6 (arm64-darwin)

benchmark                            time (avg)             (min … max)       p75       p99      p995
----------------------------------------------------------------------- -----------------------------
Array.sort (64 num, unsorted)    736.22 ns/iter  (673.6 ns … 975.75 ns) 747.02 ns 975.75 ns 975.75 ns
Array.sort (64 num, pre-sorted)  377.94 ns/iter  (370.2 ns … 395.56 ns) 380.33 ns  390.1 ns 395.56 ns

❯ bun-1.1.4 array-sort.mjs # Before
cpu: Apple M3 Max
runtime: bun 1.1.4 (arm64-darwin)

benchmark                            time (avg)             (min … max)       p75       p99      p995
----------------------------------------------------------------------- -----------------------------
Array.sort (64 num, unsorted)      1.14 µs/iter     (1.03 µs … 1.65 µs)   1.19 µs   1.65 µs   1.65 µs
Array.sort (64 num, pre-sorted)    1.07 µs/iter     (1.01 µs … 1.18 µs)   1.08 µs   1.18 µs   1.18 µs

❯ node array-sort.mjs # Node.js, for comparison
cpu: Apple M3 Max
runtime: node v22.0.0 (arm64-darwin)

benchmark                            time (avg)             (min … max)       p75       p99      p995
----------------------------------------------------------------------- -----------------------------
Array.sort (64 num, unsorted)      1.95 µs/iter      (1.8 µs … 2.12 µs)   2.04 µs   2.12 µs   2.12 µs
Array.sort (64 num, pre-sorted)  689.28 ns/iter  (677.4 ns … 719.66 ns) 694.22 ns 719.66 ns 719.66 ns
```

[View microbenchmark](https://github.com/oven-sh/bun/blob/84d81c3002bf68f913712b492a7aff988ad4c151/bench/snippets/array-sort.mjs)

## [`Module._resolveLookupPaths` in `node:module` is implemented](https://bun.com/blog/bun-v1.1.6#module-resolvelookuppaths-in-node-module-is-implemented)

The private Node.js API `Module._resolveLookupPaths` is now implemented in Bun. This API is used by `require-in-the-middle` to intercept `require` calls to instrument module loading.

Warning: when used by `dd-trace` [this may slow down your application's start time](https://github.com/DataDog/dd-trace-js/issues/3834).

## [node:http regression is fixed](https://bun.com/blog/bun-v1.1.6#node-http-regression-is-fixed)

A regression in node:http from v1.1.5 is fixed. The regression caused requests with errors to not propagate to the error event correctly. This regression impacted the `stripe` npm package, amongst others. Thanks to [@nektro](https://github.com/nektro) for fixing this regression!

## [Fixed: node:http listen callback had wrong `this` value](https://bun.com/blog/bun-v1.1.6#fixed-node-http-listen-callback-had-wrong-this-value)

A bug where the `this` value in the `listen` callback was incorrect has been fixed. The `this` value is now the server instance, as expected.

Thanks to [@nektro](https://github.com/nektro) for fixing this.

## [Fixed: cross-compilation extracting bug on Windows](https://bun.com/blog/bun-v1.1.6#fixed-cross-compilation-extracting-bug-on-windows)

A bug where `bun build --compile` would incorrectly extract the tarball on Windows has been fixed, thanks to [@dylan-conway](https://github.com/dylan-conway).

## [Fixed: `error.Unexpected` when upgrading bun across devices on Windows](https://bun.com/blog/bun-v1.1.6#fixed-error-unexpected-when-upgrading-bun-across-devices-on-windows)

The Windows NT error `NOT_SAME_DEVICE` was not correctly mapped to the posix error `EXDEV`, causing an `error.Unexpected` when upgrading Bun across different drive letters on Windows. This has been fixed.

## [Fixed: node:dns lookup didn't keep event loop alive on macOS](https://bun.com/blog/bun-v1.1.6#fixed-node-dns-lookup-didn-t-keep-event-loop-alive-on-macos)

Previously, the following code would not log `hiii` on macOS:

```
const dns = require("dns");

dns.lookup("google.com", (err, address, family) => {
  console.log("hiii");
});
```

This has been fixed.

The bug was we were not draining microtasks after DNS lookups on macOS were completed. This caused the event loop to be empty, and the process to exit before the callback was called.

## [Fixed: Bug with TOML & JSON imports](https://bun.com/blog/bun-v1.1.6#fixed-bug-with-toml-json-imports)

A bug where `json` and `toml` imports would go through the CommonJS -> ESM conversion path when they were originally required has been fixed.

The following input:

```
console.log(require("./hello.toml"));
```

🔴 Bun v1.1.5 would output (bad):

```
Module {
  __esModule: true,
  default: {
    hello: "world"
  },
  hello: {
    world: "world"
  }
}
```

🟢 Bun v1.1.6 now outputs (good):

```
{
  hello: "world",
}
```

This should also slightly reduce the memory usage of TOML imports. Previously, we would generate a sourcemap for TOML along with source code, which was unnecessary. Now we just create the objects/values directly without emitting JavaScript source code.

## [Fixed: memory leak in Bun.write()](https://bun.com/blog/bun-v1.1.6#fixed-memory-leak-in-bun-write)

When using `Bun.write()` with large output, the memory for the input string or bytes was not correctly freed. This led to large memory growth over time. This has been fixed, and a memory leak test has been added to prevent this from regressing in the future.

## [Fixed: Crash in `napi_get_date_value`](https://bun.com/blog/bun-v1.1.6#fixed-crash-in-napi-get-date-value)

A crash in `napi_get_date_value` when an unexpected type was passed has been fixed. This crash impacted certain Node Native Addons.

## [Fixed: Possible crash in HTMLRewriter with Bun.file()](https://bun.com/blog/bun-v1.1.6#fixed-possible-crash-in-htmlrewriter-with-bun-file)

When using `HTMLRewriter` to transform HTML files on disk with `Bun.file()`, in certain cases Bun could crash or never fulfill a Promise. This has been fixed.

## [Fixed: edgecase with --define](https://bun.com/blog/bun-v1.1.6#fixed-edgecase-with-define)

A bug where `--define` when used on a global property would have incorrect output has been fixed, thanks to [@dylan-conway](https://github.com/dylan-conway).

## [Thank you to 9 contributors!](https://bun.com/blog/bun-v1.1.6#thank-you-to-9-contributors)

* [@Electroid](https://github.com/Electroid)
* [@Jarred-Sumner](https://github.com/Jarred-Sumner)
* [@KilianB](https://github.com/KilianB)
* [@dylan-conway](https://github.com/dylan-conway)
* [@gvilums](https://github.com/gvilums)
* [@jlucaso1](https://github.com/jlucaso1)
* [@nektro](https://github.com/nektro)
* [@paperclover](https://github.com/paperclover)
* [@yus-ham](https://github.com/yus-ham)

---

[#### Bun v1.1.5](https://bun.com/blog/bun-v1.1.5)[#### Bun v1.1.7](https://bun.com/blog/bun-v1.1.7)