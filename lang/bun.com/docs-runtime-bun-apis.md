---
url: https://bun.com/docs/runtime/bun-apis
title: Bun APIs - Bun
source_domain: bun.com
---

# Bun APIs - Bun

Bun implements a set of native APIs on the `Bun` global object and through a number of built-in modules. These APIs are heavily optimized and represent the canonical “Bun-native” way to implement some common functionality.
Bun strives to implement standard Web APIs wherever possible. Bun introduces new APIs primarily for server-side tasks where no standard exists, such as file I/O and starting an HTTP server. In these cases, Bun’s approach still builds atop standard APIs like `Blob`, `URL`, and `Request`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)server.ts

Copy

```
Bun.serve({
  fetch(req: Request) {
    return new Response("Success!");
  },
});
```

Click the link in the right column to jump to the associated documentation.

| Topic | APIs |
| --- | --- |
| HTTP Server | [`Bun.serve`](https://bun.com/docs/runtime/http/server) |
| Shell | [`$`](https://bun.com/docs/runtime/shell) |
| Bundler | [`Bun.build`](https://bun.com/docs/bundler) |
| File I/O | [`Bun.file`](https://bun.com/docs/runtime/file-io#reading-files-bun-file), [`Bun.write`](https://bun.com/docs/runtime/file-io#writing-files-bun-write), `Bun.stdin`, `Bun.stdout`, `Bun.stderr` |
| Child Processes | [`Bun.spawn`](https://bun.com/docs/runtime/child-process#spawn-a-process-bun-spawn), [`Bun.spawnSync`](https://bun.com/docs/runtime/child-process#blocking-api-bun-spawnsync) |
| TCP Sockets | [`Bun.listen`](https://bun.com/docs/runtime/networking/tcp#start-a-server-bun-listen), [`Bun.connect`](https://bun.com/docs/runtime/networking/tcp#start-a-server-bun-listen) |
| UDP Sockets | [`Bun.udpSocket`](https://bun.com/docs/runtime/networking/udp) |
| WebSockets | `new WebSocket()` (client), [`Bun.serve`](https://bun.com/docs/runtime/http/websockets) (server) |
| Transpiler | [`Bun.Transpiler`](https://bun.com/docs/runtime/transpiler) |
| Routing | [`Bun.FileSystemRouter`](https://bun.com/docs/runtime/file-system-router) |
| Streaming HTML | [`HTMLRewriter`](https://bun.com/docs/runtime/html-rewriter) |
| Hashing | [`Bun.password`](https://bun.com/docs/runtime/hashing#bun-password), [`Bun.hash`](https://bun.com/docs/runtime/hashing#bun-hash), [`Bun.CryptoHasher`](https://bun.com/docs/runtime/hashing#bun-cryptohasher), `Bun.sha` |
| SQLite | [`bun:sqlite`](https://bun.com/docs/runtime/sqlite) |
| PostgreSQL Client | [`Bun.SQL`](https://bun.com/docs/runtime/sql), `Bun.sql` |
| Redis (Valkey) Client | [`Bun.RedisClient`](https://bun.com/docs/runtime/redis), `Bun.redis` |
| FFI (Foreign Function Interface) | [`bun:ffi`](https://bun.com/docs/runtime/ffi) |
| DNS | [`Bun.dns.lookup`](https://bun.com/docs/runtime/networking/dns), `Bun.dns.prefetch`, `Bun.dns.getCacheStats` |
| Testing | [`bun:test`](https://bun.com/docs/test) |
| Workers | [`new Worker()`](https://bun.com/docs/runtime/workers) |
| Module Loaders | [`Bun.plugin`](https://bun.com/docs/bundler/plugins) |
| Glob | [`Bun.Glob`](https://bun.com/docs/runtime/glob) |
| Cookies | [`Bun.Cookie`](https://bun.com/docs/runtime/cookies), [`Bun.CookieMap`](https://bun.com/docs/runtime/cookies) |
| Node-API | [`Node-API`](https://bun.com/docs/runtime/node-api) |
| `import.meta` | [`import.meta`](https://bun.com/docs/runtime/module-resolution#import-meta) |
| Utilities | [`Bun.version`](https://bun.com/docs/runtime/utils#bun-version), [`Bun.revision`](https://bun.com/docs/runtime/utils#bun-revision), [`Bun.env`](https://bun.com/docs/runtime/utils#bun-env), [`Bun.main`](https://bun.com/docs/runtime/utils#bun-main) |
| Sleep & Timing | [`Bun.sleep()`](https://bun.com/docs/runtime/utils#bun-sleep), [`Bun.sleepSync()`](https://bun.com/docs/runtime/utils#bun-sleepsync), [`Bun.nanoseconds()`](https://bun.com/docs/runtime/utils#bun-nanoseconds) |
| Random & UUID | [`Bun.randomUUIDv7()`](https://bun.com/docs/runtime/utils#bun-randomuuidv7) |
| System & Environment | [`Bun.which()`](https://bun.com/docs/runtime/utils#bun-which) |
| Comparison & Inspection | [`Bun.peek()`](https://bun.com/docs/runtime/utils#bun-peek), [`Bun.deepEquals()`](https://bun.com/docs/runtime/utils#bun-deepequals), `Bun.deepMatch`, [`Bun.inspect()`](https://bun.com/docs/runtime/utils#bun-inspect) |
| String & Text Processing | [`Bun.escapeHTML()`](https://bun.com/docs/runtime/utils#bun-escapehtml), [`Bun.stringWidth()`](https://bun.com/docs/runtime/utils#bun-stringwidth), `Bun.indexOfLine` |
| URL & Path Utilities | [`Bun.fileURLToPath()`](https://bun.com/docs/runtime/utils#bun-fileurltopath), [`Bun.pathToFileURL()`](https://bun.com/docs/runtime/utils#bun-pathtofileurl) |
| Compression | [`Bun.gzipSync()`](https://bun.com/docs/runtime/utils#bun-gzipsync), [`Bun.gunzipSync()`](https://bun.com/docs/runtime/utils#bun-gunzipsync), [`Bun.deflateSync()`](https://bun.com/docs/runtime/utils#bun-deflatesync), [`Bun.inflateSync()`](https://bun.com/docs/runtime/utils#bun-inflatesync), `Bun.zstdCompressSync()`, `Bun.zstdDecompressSync()`, `Bun.zstdCompress()`, `Bun.zstdDecompress()` |
| Stream Processing | [`Bun.readableStreamTo*()`](https://bun.com/docs/runtime/utils#bun-readablestreamto), `Bun.readableStreamToBytes()`, `Bun.readableStreamToBlob()`, `Bun.readableStreamToFormData()`, `Bun.readableStreamToJSON()`, `Bun.readableStreamToArray()` |
| Memory & Buffer Management | `Bun.ArrayBufferSink`, `Bun.allocUnsafe`, `Bun.concatArrayBuffers` |
| Module Resolution | [`Bun.resolveSync()`](https://bun.com/docs/runtime/utils#bun-resolvesync) |
| Parsing & Formatting | [`Bun.semver`](https://bun.com/docs/runtime/semver), `Bun.TOML.parse`, [`Bun.color`](https://bun.com/docs/runtime/color) |
| Low-level / Internals | `Bun.mmap`, `Bun.gc`, `Bun.generateHeapSnapshot`, [`bun:jsc`](https://bun.com/reference/bun/jsc) |

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/runtime/bun-apis.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /runtime/bun-apis)

⌘I