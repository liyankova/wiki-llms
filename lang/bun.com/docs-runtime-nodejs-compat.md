---
url: https://bun.com/docs/runtime/nodejs-compat
title: Node.js Compatibility - Bun
source_domain: bun.com
---

# Node.js Compatibility - Bun

Every day, Bun gets closer to 100% Node.js API compatibility. Today, popular frameworks like Next.js, Express, and millions of `npm` packages intended for Node just work with Bun. To ensure compatibility, we run thousands of tests from Node.js’ test suite before every release of Bun.
**If a package works in Node.js but doesn’t work in Bun, we consider it a bug in Bun.** Please [open an issue](https://bun.com/issues) and we’ll fix it.
This page is updated regularly to reflect compatibility status of the latest version of Bun. The information below reflects Bun’s compatibility with *Node.js v23*.

## [​](https://bun.com/docs/runtime/nodejs-compat#built-in-node-js-modules) Built-in Node.js modules

### [​](https://bun.com/docs/runtime/nodejs-compat#node:assert) [`node:assert`](https://nodejs.org/api/assert.html)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:buffer) [`node:buffer`](https://nodejs.org/api/buffer.html)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:console) [`node:console`](https://nodejs.org/api/console.html)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:dgram) [`node:dgram`](https://nodejs.org/api/dgram.html)

🟢 Fully implemented. > 90% of Node.js’s test suite passes.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:diagnostics-channel) [`node:diagnostics_channel`](https://nodejs.org/api/diagnostics_channel.html)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:dns) [`node:dns`](https://nodejs.org/api/dns.html)

🟢 Fully implemented. > 90% of Node.js’s test suite passes.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:events) [`node:events`](https://nodejs.org/api/events.html)

🟢 Fully implemented. 100% of Node.js’s test suite passes. `EventEmitterAsyncResource` uses `AsyncResource` underneath.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:fs) [`node:fs`](https://nodejs.org/api/fs.html)

🟢 Fully implemented. 92% of Node.js’s test suite passes.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:http) [`node:http`](https://nodejs.org/api/http.html)

🟢 Fully implemented. Outgoing client request body is currently buffered instead of streamed.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:https) [`node:https`](https://nodejs.org/api/https.html)

🟢 APIs are implemented, but `Agent` is not always used yet.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:os) [`node:os`](https://nodejs.org/api/os.html)

🟢 Fully implemented. 100% of Node.js’s test suite passes.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:path) [`node:path`](https://nodejs.org/api/path.html)

🟢 Fully implemented. 100% of Node.js’s test suite passes.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:punycode) [`node:punycode`](https://nodejs.org/api/punycode.html)

🟢 Fully implemented. 100% of Node.js’s test suite passes, *deprecated by Node.js*.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:querystring) [`node:querystring`](https://nodejs.org/api/querystring.html)

🟢 Fully implemented. 100% of Node.js’s test suite passes.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:readline) [`node:readline`](https://nodejs.org/api/readline.html)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:stream) [`node:stream`](https://nodejs.org/api/stream.html)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:string-decoder) [`node:string_decoder`](https://nodejs.org/api/string_decoder.html)

🟢 Fully implemented. 100% of Node.js’s test suite passes.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:timers) [`node:timers`](https://nodejs.org/api/timers.html)

🟢 Recommended to use global `setTimeout`, et. al. instead.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:tty) [`node:tty`](https://nodejs.org/api/tty.html)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:url) [`node:url`](https://nodejs.org/api/url.html)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:zlib) [`node:zlib`](https://nodejs.org/api/zlib.html)

🟢 Fully implemented. 98% of Node.js’s test suite passes.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:async-hooks) [`node:async_hooks`](https://nodejs.org/api/async_hooks.html)

🟡 `AsyncLocalStorage`, and `AsyncResource` are implemented. v8 promise hooks are not called, and its usage is [strongly discouraged](https://nodejs.org/docs/latest/api/async_hooks.html#async-hooks).

### [​](https://bun.com/docs/runtime/nodejs-compat#node:child-process) [`node:child_process`](https://nodejs.org/api/child_process.html)

🟡 Missing `proc.gid` `proc.uid`. `Stream` class not exported. IPC cannot send socket handles. Node.js ↔ Bun IPC can be used with JSON serialization.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:cluster) [`node:cluster`](https://nodejs.org/api/cluster.html)

🟡 Handles and file descriptors cannot be passed between workers, which means load-balancing HTTP requests across processes is only supported on Linux at this time (via `SO_REUSEPORT`). Otherwise, implemented but not battle-tested.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:crypto) [`node:crypto`](https://nodejs.org/api/crypto.html)

🟡 Missing `secureHeapUsed` `setEngine` `setFips`

### [​](https://bun.com/docs/runtime/nodejs-compat#node:domain) [`node:domain`](https://nodejs.org/api/domain.html)

🟡 Missing `Domain` `active`

### [​](https://bun.com/docs/runtime/nodejs-compat#node:http2) [`node:http2`](https://nodejs.org/api/http2.html)

🟡 Client & server are implemented (95.25% of gRPC’s test suite passes). Missing `options.allowHTTP1`, `options.enableConnectProtocol`, ALTSVC extension, and `http2stream.pushStream`.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:module) [`node:module`](https://nodejs.org/api/module.html)

🟡 Missing `syncBuiltinESMExports`, `Module#load()`. Overriding `require.cache` is supported for ESM & CJS modules. `module._extensions`, `module._pathCache`, `module._cache` are no-ops. `module.register` is not implemented and we recommend using a [`Bun.plugin`](https://bun.com/docs/runtime/plugins) in the meantime.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:net) [`node:net`](https://nodejs.org/api/net.html)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:perf-hooks) [`node:perf_hooks`](https://nodejs.org/api/perf_hooks.html)

🟡 APIs are implemented, but Node.js test suite does not pass yet for this module.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:process) [`node:process`](https://nodejs.org/api/process.html)

🟡 See [`process`](https://bun.com/docs/runtime/nodejs-compat#process) Global.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:sys) [`node:sys`](https://nodejs.org/api/util.html)

🟡 See [`node:util`](https://bun.com/docs/runtime/nodejs-compat#node-util).

### [​](https://bun.com/docs/runtime/nodejs-compat#node:tls) [`node:tls`](https://nodejs.org/api/tls.html)

🟡 Missing `tls.createSecurePair`.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:util) [`node:util`](https://nodejs.org/api/util.html)

🟡 Missing `getCallSite` `getCallSites` `getSystemErrorMap` `getSystemErrorMessage` `transferableAbortSignal` `transferableAbortController`

### [​](https://bun.com/docs/runtime/nodejs-compat#node:v8) [`node:v8`](https://nodejs.org/api/v8.html)

🟡 `writeHeapSnapshot` and `getHeapSnapshot` are implemented. `serialize` and `deserialize` use JavaScriptCore’s wire format instead of V8’s. Other methods are not implemented. For profiling, use [`bun:jsc`](https://bun.com/docs/project/benchmarking#javascript-heap-stats) instead.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:vm) [`node:vm`](https://nodejs.org/api/vm.html)

🟡 Core functionality and ES modules are implemented, including `vm.Script`, `vm.createContext`, `vm.runInContext`, `vm.runInNewContext`, `vm.runInThisContext`, `vm.compileFunction`, `vm.isContext`, `vm.Module`, `vm.SourceTextModule`, `vm.SyntheticModule`, and `importModuleDynamically` support. Options like `timeout` and `breakOnSigint` are fully supported. Missing `vm.measureMemory` and some `cachedData` functionality.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:wasi) [`node:wasi`](https://nodejs.org/api/wasi.html)

🟡 Partially implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:worker-threads) [`node:worker_threads`](https://nodejs.org/api/worker_threads.html)

🟡 `Worker` doesn’t support the following options: `stdin` `stdout` `stderr` `trackedUnmanagedFds` `resourceLimits`. Missing `markAsUntransferable` `moveMessagePortToContext`.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:inspector) [`node:inspector`](https://nodejs.org/api/inspector.html)

🔴 Not implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:repl) [`node:repl`](https://nodejs.org/api/repl.html)

🔴 Not implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:sqlite) [`node:sqlite`](https://nodejs.org/api/sqlite.html)

🔴 Not implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:test) [`node:test`](https://nodejs.org/api/test.html)

🟡 Partly implemented. Missing mocks, snapshots, timers. Use [`bun:test`](https://bun.com/docs/test) instead.

### [​](https://bun.com/docs/runtime/nodejs-compat#node:trace-events) [`node:trace_events`](https://nodejs.org/api/tracing.html)

🔴 Not implemented.

## [​](https://bun.com/docs/runtime/nodejs-compat#node-js-globals) Node.js globals

The table below lists all globals implemented by Node.js and Bun’s current compatibility status.

### [​](https://bun.com/docs/runtime/nodejs-compat#abortcontroller) [`AbortController`](https://developer.mozilla.org/en-US/docs/Web/API/AbortController)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#abortsignal) [`AbortSignal`](https://developer.mozilla.org/en-US/docs/Web/API/AbortSignal)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#blob) [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#buffer) [`Buffer`](https://nodejs.org/api/buffer.html#class-buffer)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#bytelengthqueuingstrategy) [`ByteLengthQueuingStrategy`](https://developer.mozilla.org/en-US/docs/Web/API/ByteLengthQueuingStrategy)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#dirname) [`__dirname`](https://nodejs.org/api/globals.html#__dirname)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#filename) [`__filename`](https://nodejs.org/api/globals.html#__filename)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#atob) [`atob()`](https://developer.mozilla.org/en-US/docs/Web/API/atob)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#atomics) [`Atomics`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Atomics)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#broadcastchannel) [`BroadcastChannel`](https://developer.mozilla.org/en-US/docs/Web/API/BroadcastChannel)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#btoa) [`btoa()`](https://developer.mozilla.org/en-US/docs/Web/API/btoa)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#clearimmediate) [`clearImmediate()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/clearImmediate)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#clearinterval) [`clearInterval()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/clearInterval)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#cleartimeout) [`clearTimeout()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/clearTimeout)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#compressionstream) [`CompressionStream`](https://developer.mozilla.org/en-US/docs/Web/API/CompressionStream)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#console) [`console`](https://developer.mozilla.org/en-US/docs/Web/API/console)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#countqueuingstrategy) [`CountQueuingStrategy`](https://developer.mozilla.org/en-US/docs/Web/API/CountQueuingStrategy)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#crypto) [`Crypto`](https://developer.mozilla.org/en-US/docs/Web/API/Crypto)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#subtlecrypto-crypto) [`SubtleCrypto (crypto)`](https://developer.mozilla.org/en-US/docs/Web/API/crypto)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#cryptokey) [`CryptoKey`](https://developer.mozilla.org/en-US/docs/Web/API/CryptoKey)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#customevent) [`CustomEvent`](https://developer.mozilla.org/en-US/docs/Web/API/CustomEvent)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#decompressionstream) [`DecompressionStream`](https://developer.mozilla.org/en-US/docs/Web/API/DecompressionStream)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#event) [`Event`](https://developer.mozilla.org/en-US/docs/Web/API/Event)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#eventtarget) [`EventTarget`](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#exports) [`exports`](https://nodejs.org/api/globals.html#exports)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#fetch) [`fetch`](https://developer.mozilla.org/en-US/docs/Web/API/fetch)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#formdata) [`FormData`](https://developer.mozilla.org/en-US/docs/Web/API/FormData)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#global) [`global`](https://nodejs.org/api/globals.html#global)

🟢 Implemented. This is an object containing all objects in the global namespace. It’s rarely referenced directly, as its contents are available without an additional prefix, e.g. `__dirname` instead of `global.__dirname`.

### [​](https://bun.com/docs/runtime/nodejs-compat#globalthis) [`globalThis`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/globalThis)

🟢 Aliases to `global`.

### [​](https://bun.com/docs/runtime/nodejs-compat#headers) [`Headers`](https://developer.mozilla.org/en-US/docs/Web/API/Headers)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#messagechannel) [`MessageChannel`](https://developer.mozilla.org/en-US/docs/Web/API/MessageChannel)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#messageevent) [`MessageEvent`](https://developer.mozilla.org/en-US/docs/Web/API/MessageEvent)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#messageport) [`MessagePort`](https://developer.mozilla.org/en-US/docs/Web/API/MessagePort)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#module) [`module`](https://nodejs.org/api/globals.html#module)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#performanceentry) [`PerformanceEntry`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceEntry)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#performancemark) [`PerformanceMark`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceMark)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#performancemeasure) [`PerformanceMeasure`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceMeasure)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#performanceobserver) [`PerformanceObserver`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceObserver)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#performanceobserverentrylist) [`PerformanceObserverEntryList`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceObserverEntryList)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#performanceresourcetiming) [`PerformanceResourceTiming`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#performance) [`performance`](https://developer.mozilla.org/en-US/docs/Web/API/performance)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#process) [`process`](https://nodejs.org/api/process.html)

🟡 Mostly implemented. `process.binding` (internal Node.js bindings some packages rely on) is partially implemented. `process.title` is currently a no-op on macOS & Linux. `getActiveResourcesInfo` `setActiveResourcesInfo`, `getActiveResources` and `setSourceMapsEnabled` are stubs. Newer APIs like `process.loadEnvFile` and `process.getBuiltinModule` are not implemented yet.

### [​](https://bun.com/docs/runtime/nodejs-compat#queuemicrotask) [`queueMicrotask()`](https://developer.mozilla.org/en-US/docs/Web/API/queueMicrotask)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#readablebytestreamcontroller) [`ReadableByteStreamController`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableByteStreamController)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#readablestream) [`ReadableStream`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#readablestreambyobreader) [`ReadableStreamBYOBReader`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStreamBYOBReader)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#readablestreambyobrequest) [`ReadableStreamBYOBRequest`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStreamBYOBRequest)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#readablestreamdefaultcontroller) [`ReadableStreamDefaultController`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStreamDefaultController)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#readablestreamdefaultreader) [`ReadableStreamDefaultReader`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStreamDefaultReader)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#require) [`require()`](https://nodejs.org/api/globals.html#require)

🟢 Fully implemented, including [`require.main`](https://nodejs.org/api/modules.html#requiremain), [`require.cache`](https://nodejs.org/api/modules.html#requirecache), [`require.resolve`](https://nodejs.org/api/modules.html#requireresolverequest-options).

### [​](https://bun.com/docs/runtime/nodejs-compat#response) [`Response`](https://developer.mozilla.org/en-US/docs/Web/API/Response)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#request) [`Request`](https://developer.mozilla.org/en-US/docs/Web/API/Request)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#setimmediate) [`setImmediate()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/setImmediate)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#setinterval) [`setInterval()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/setInterval)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#settimeout) [`setTimeout()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/setTimeout)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#structuredclone) [`structuredClone()`](https://developer.mozilla.org/en-US/docs/Web/API/structuredClone)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#subtlecrypto) [`SubtleCrypto`](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#domexception) [`DOMException`](https://developer.mozilla.org/en-US/docs/Web/API/DOMException)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#textdecoder) [`TextDecoder`](https://developer.mozilla.org/en-US/docs/Web/API/TextDecoder)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#textdecoderstream) [`TextDecoderStream`](https://developer.mozilla.org/en-US/docs/Web/API/TextDecoderStream)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#textencoder) [`TextEncoder`](https://developer.mozilla.org/en-US/docs/Web/API/TextEncoder)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#textencoderstream) [`TextEncoderStream`](https://developer.mozilla.org/en-US/docs/Web/API/TextEncoderStream)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#transformstream) [`TransformStream`](https://developer.mozilla.org/en-US/docs/Web/API/TransformStream)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#transformstreamdefaultcontroller) [`TransformStreamDefaultController`](https://developer.mozilla.org/en-US/docs/Web/API/TransformStreamDefaultController)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#url) [`URL`](https://developer.mozilla.org/en-US/docs/Web/API/URL)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#urlsearchparams) [`URLSearchParams`](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#webassembly) [`WebAssembly`](https://nodejs.org/api/globals.html#webassembly)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#writablestream) [`WritableStream`](https://developer.mozilla.org/en-US/docs/Web/API/WritableStream)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#writablestreamdefaultcontroller) [`WritableStreamDefaultController`](https://developer.mozilla.org/en-US/docs/Web/API/WritableStreamDefaultController)

🟢 Fully implemented.

### [​](https://bun.com/docs/runtime/nodejs-compat#writablestreamdefaultwriter) [`WritableStreamDefaultWriter`](https://developer.mozilla.org/en-US/docs/Web/API/WritableStreamDefaultWriter)

🟢 Fully implemented.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/runtime/nodejs-compat.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /runtime/nodejs-compat)

⌘I