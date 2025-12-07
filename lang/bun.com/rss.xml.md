---
url: https://bun.com/rss.xml
title: bun.com
source_domain: bun.com
---

# bun.com

bun.com
https://bun.com
A fast all-in-one JavaScript runtime and toolkit
en-us

Tue, 02 Dec 2025 17:51:42 GMT
Tue, 02 Dec 2025 17:51:42 GMT
60

Bun is joining Anthropic
https://bun.com/blog/bun-joins-anthropic
https://bun.com/blog/bun-joins-anthropic
Bun has been acquired by Anthropic. Anthropic is betting on Bun as the infrastructure powering Claude Code, Claude Agent SDK, and future AI coding products & tools.
Tue, 02 Dec 2025 10:00:00 GMT

Bun v1.3.3
https://bun.com/blog/bun-v1.3.3
https://bun.com/blog/bun-v1.3.3
Fixes 95 issues (addressing 348 👍). CompressionStream and DecompressionStream, Control .env and bunfig.toml loading in standalone executables, `retry` and `repeats` in `bun:test`, --no-env-file, SQLite 3.51.0, Upgraded to Zig 0.15.2, Bugfixes for bundler, bun install, Windows, Node.js compatibility, Web APIs, Bun.serve, networking, Bun.YAML, Bun.Transpiler, Bun.spawn & TypeScript definitions
Fri, 21 Nov 2025 10:11:00 GMT

Bun v1.3.2
https://bun.com/blog/bun-v1.3.2
https://bun.com/blog/bun-v1.3.2
Fixes 287 issues (addressing 324 👍). Hoisted installs restored as default for backward compatibility. CPU profiling with --cpu-prof, faster installs for packages with post-install scripts, bun:test onTestFinished hook, ServerWebSocket subscriptions getter, Alpine 3.22 in Docker images, improved Git dependency resolution, bun list alias, and numerous bug fixes across install, HTTP/HTTPS, N-API, bun test, bun build, and runtime.
Sat, 08 Nov 2025 10:11:00 GMT

Vercel now supports the Bun Runtime
https://bun.com/blog/vercel-adds-native-bun-support
https://bun.com/blog/vercel-adds-native-bun-support
Deploy and run your applications with Bun's fast JavaScript runtime on Vercel Functions, with full access to Bun APIs and improved performance
Tue, 28 Oct 2025 15:00:00 GMT

Bun v1.3.1
https://bun.com/blog/bun-v1.3.1
https://bun.com/blog/bun-v1.3.1
Fixes 103 issues (addressing 172 👍). 2× faster bun build on macOS for symlink-heavy projects, source maps preserve legal comments, and --format=cjs now inlines import.meta; bun test adds global vi, --pass-with-no-tests, and --only-failures; .npmrc :email auth support, faster installs when no peer deps, selective hoisting for isolated installs (publicHoistPattern/hoistPattern), and fs/promises FileHandle.readLines(); numerous bundler/transpiler fixes (external sourcemaps in Bun.build({ compile:true }), --bytecode with import.meta, Windows react-jsxdev); reliability fixes across install/pm/pack, bunx, Node.js compatibility improvements, and numerous bug fixes.
Wed, 22 Oct 2025 10:11:00 GMT

Bun 1.3
https://bun.com/blog/bun-v1.3
https://bun.com/blog/bun-v1.3
Bun 1.3 introduces zero-config frontend development, unified SQL API, built-in Redis client, security enhancements, package catalogs, async stack traces, VS Code test integration, and Node.js compatibility improvements.
Fri, 10 Oct 2025 20:00:00 GMT

Bun v1.2.23
https://bun.com/blog/bun-v1.2.23
https://bun.com/blog/bun-v1.2.23
Fixes 119 issues (addressing 412 👍). pnpm-lock.yaml migration for seamless switching from pnpm to bun install, Redis Pub/Sub support, concurrent test execution with configurable parallelism, platform-specific dependency filtering with --cpu and --os flags, system CA certificates support with --use-system-ca, Windows code signing for compiled executables, JSX configuration improvements in Bun.build, sql.array helper for parameterized arrays, randomized test ordering, stricter CI test defaults, process.report.getReport() on Windows, and numerous Node.js compatibility improvements including http, dns, worker\_threads, crypto, http2, net, and tty modules.
Sun, 28 Sep 2025 10:11:00 GMT

Bun v1.2.22
https://bun.com/blog/bun-v1.2.22
https://bun.com/blog/bun-v1.2.22
Fixes 144 issues (addressing 257 👍). Async stack traces for better debugging, RFC 6455 compliant WebSocket client subprotocol negotiation, MySQL adapter improvements including affectedRows and lastInsertRowid support, JSX side effects preservation during bundling, event loop delay monitoring with perf\_hooks, HTTP server idle connection management, --workspaces in bun run, function name removal during minification, and numerous Node.js compatibility fixes including child\_process.spawnSync, socket.write with Uint8Array, crypto.verify RSA defaults, N-API improvements, HTMLRewriter error handling, fetch decompression fixes, Bun.SQL, and Bun.$ improvements.
Sun, 14 Sep 2025 22:54:53 GMT

Behind The Scenes of Bun Install
https://bun.com/blog/behind-the-scenes-of-bun-install
https://bun.com/blog/behind-the-scenes-of-bun-install
Learn how Bun is able to cut install times by up to 25×. Bun skips Node.js's overhead with direct system calls, cache-friendly data layouts, OS-level copy-on-write, and full-core parallelism.
Wed, 10 Sep 2025 15:00:00 GMT

Bun v1.2.21
https://bun.com/blog/bun-v1.2.21
https://bun.com/blog/bun-v1.2.21
Fixes 69 issues (addressing 204 👍). Bun.SQL now supports MySQL and SQLite, alongside PostgreSQL. Native YAML support. 500x faster postMessage(string). Bun.build() compile API, with cross-platform targets. Reduced idle CPU usage. Bun.stripANSI for SIMD-accelerated ANSI escape removal. bunx --package flag support. customizable User-Agent headers. Windows executable metadata embedding. and extensive Node.js compatibility improvements
Mon, 25 Aug 2025 22:54:53 GMT

500x faster postMessage(string)
https://bun.com/blog/how-we-made-postMessage-string-500x-faster
https://bun.com/blog/how-we-made-postMessage-string-500x-faster
Zero-copy postMessage(string)
Wed, 20 Aug 2025 22:54:53 GMT

Bun v1.2.20
https://bun.com/blog/bun-v1.2.20
https://bun.com/blog/bun-v1.2.20
Fixes 141 issues (addressing 429 👍). Reduced idle CPU usage. Improved `bun:test` diffing. Automatic `ETag` and `If-None-Match` in static routes for `Bun.serve`. 40x faster `AbortSignal.timeout`. Windows long path support. `WebAssembly.compileStreaming` and `WebAssembly.instantiateStreaming`. Many, many reliability improvements.
Sun, 10 Aug 2025 10:00:00 GMT

Bun v1.2.19
https://bun.com/blog/bun-v1.2.19
https://bun.com/blog/bun-v1.2.19
Fixes 163 issues (addressing 1,043 👍). Introduces `bun install --linker=isolated` for pnpm-style isolated node\_modules, `bun why` for dependency tree understanding, `bun pm pkg` commands for package.json management, enhanced `node:fs.glob()` with array patterns and exclude options, `node:module.SourceMap` class and `findSourceMap()`, smarter `@types/bun` with automatic Node.js compatibility detection, plus numerous Node.js compatibility improvements, runtime bugfixes, bundler enhancements, and bun install optimizations.
Sat, 19 Jul 2025 10:00:00 GMT

Bun v1.2.18
https://bun.com/blog/bun-v1.2.18
https://bun.com/blog/bun-v1.2.18
Fixes 52 issues (addressing 112 👍). ReadableStream text(), json(), bytes(), blob(), WebSocket client compression with `permessage-deflate`, `bun pm version`, reduced memory usage for large `fetch()` and `S3` uploads, faster `napi\_create\_buffer`, faster sliced string handling in native addons, `fs.glob` now matches directories by default, `net.createConnection()` now validates `options.host`, `http.ClientRequest#flushHeaders` now correctly sends the request body, `net.connect` `keepAlive` and `keepAliveInitialDelay` options are now correctly handled, `fs.watchFile` emits `stop` on next tick, `net.Server` handles promise rejections in connection listeners, `net.connect` throws `ERR\_INVALID\_IP\_ADDRESS` for non-string lookup results, `fs.watchFile` now ignores access time, `bun:sqlite` updated to SQLite 3.50.2, Bun now reports as Node.js v24.3.0, `bun test` now fails when no tests match a filter, `bun install` is faster for packages using `node-gyp`, `Math.sumPrecise` is now available, Node.js compatibility improvements.
Thu, 03 Jul 2025 10:00:00 GMT

Bun v1.2.17
https://bun.com/blog/bun-v1.2.17
https://bun.com/blog/bun-v1.2.17
Fixes 50 issues (addressing 80 👍), and adds +24 passing Node.js tests. Ahead-of-time bundling for HTML imports, more reliable Bun Shell, `setTimeout` and `setImmediate` use 8-15% less memory, `columnTypes` & `declaredTypes` in `bun:sqlite`, `bun info` is the new `bun pm view`, Node.js compatibility improvements to `child\_process.fork`, `fs.glob` options are now optional, `tls.getCACertificates()` is now implemented, `bun init` generates `CLAUDE.md` when claude code is installed, and more.
Sat, 21 Jun 2025 22:54:53 GMT

Bun v1.2.16
https://bun.com/blog/bun-v1.2.16
https://bun.com/blog/bun-v1.2.16
Fixes 73 issues (addressing 124 👍), and adds +119 passing Node.js tests. Serve files with `Bun.serve` through `routes`, `install.linkWorkspacePackages` option in `bunfig.toml`, `bun outdated` support for catalogs, `Bun.hash.rapidhash`, `node:net` compatibility, `vm.SyntheticModule` support, `HTTPParser` binding, and memory leak fixes.
Wed, 11 Jun 2025 22:54:53 GMT

Bun v1.2.15
https://bun.com/blog/bun-v1.2.15
https://bun.com/blog/bun-v1.2.15
Fixes 11 issues (addressing 261 👍). bun audit scans dependencies for security vulnerabilities, bun pm view shows package metadata from npm. bun init adds a Cursor rule to use Bun instead of Node.js/Vite/npm/pnpm, `node:vm SourceTextModule` and `node:perf\_hooks createHistogram` are now implemented.
Wed, 28 May 2025 17:07:10 GMT

Bun v1.2.14
https://bun.com/blog/bun-v1.2.14
https://bun.com/blog/bun-v1.2.14
Fixes 39 issues (addressing 179 👍). Adds support for catalogs in bun install, --react flag for bun init, improved HTTP routing with method-specific routes, better TypeScript default module settings, fixes a HTTPS proxy issue impacting Codex, and several Node.js compatibility improvements including worker\_threads reliability enhancements and http2 server improvements.
Wed, 21 May 2025 12:00:00 GMT

Bun v1.2.13
https://bun.com/blog/bun-v1.2.13
https://bun.com/blog/bun-v1.2.13
Fixes 17 bugs (addressing 28 👍, adding +28 passing Node.js tests). Improved --hot stability and Node.js compatibility. Better `node:worker\_threads` support, environment data, reduced memory usage for child\_process IPC and worker\_threads. Fixes BOM handling in `.npmrc` files. Fixes hot reloading on older versions of chrome
Fri, 09 May 2025 05:00:00 GMT

Bun v1.2.12
https://bun.com/blog/bun-v1.2.12
https://bun.com/blog/bun-v1.2.12
Stream browser console logs to your terminal, dev server uses less memory. Node.js compatibility improvements for timers, vm, net, http, and bugfixes for TextDecoder, hot reloading reliability bugfixes
Sun, 04 May 2025 05:02:21 GMT

Bun v1.2.11
https://bun.com/blog/bun-v1.2.11
https://bun.com/blog/bun-v1.2.11
Fixes 62 bugs (addressing 77 👍). `process.ref` and `process.unref`, `util.parseArgs` negative options, `BUN\_INSPECT\_PRELOAD`, Highway SIMD, Node.js compatibility improvements for `node:http`, `node:https`, `node:tls`, and `node:readline`
Tue, 29 Apr 2025 02:39:42 GMT

Bun v1.2.10
https://bun.com/blog/bun-v1.2.10
https://bun.com/blog/bun-v1.2.10
Fixes 33 bugs (addressing 33 👍). setImmediate gets faster. Reliability improvements for filesystem operations. Fixes test.failing with done callbacks. Fixes default idle timeout in Redis client. Fixes importing from 'bun' module with bytecode compilation. Default Docker image updated to Debian Bookworm.
Thu, 17 Apr 2025 05:02:21 GMT

Bun v1.2.9
https://bun.com/blog/bun-v1.2.9
https://bun.com/blog/bun-v1.2.9
Fixes 48 bugs (addressing 116 👍). Bun.redis is a builtin Redis client for Bun. `ListObjectsV2` support in `Bun.S3Client`, more `libuv` symbols, `require.extensions` & require.resolve paths, bugfixes in `node:http`, `AsyncLocalStorage`, and `node:crypto`. Shell reliability improvements.
Wed, 09 Apr 2025 03:04:26 GMT

Debugging JavaScript Memory Leaks
https://bun.com/blog/debugging-memory-leaks
https://bun.com/blog/debugging-memory-leaks
Use v8 heap snapshot API + Chrome DevTools to compare heap snapshots
Wed, 02 Apr 2025 15:00:00 GMT

Bun v1.2.8
https://bun.com/blog/bun-v1.2.8
https://bun.com/blog/bun-v1.2.8
Fixes 18 bugs (addressing 18 👍). napi improvements make node-sdl 100x faster. Headers.get() is 2x faster. Several node:http bugfixes. node:fs improvements. `bun install --frozen-lockfile` now works with `overrides`. `bun pack` now handles directory-specific pattern exclusion.
Mon, 31 Mar 2025 08:46:20 GMT

Bun v1.2.7
https://bun.com/blog/bun-v1.2.7
https://bun.com/blog/bun-v1.2.7
Fixes 35 bugs (addressing 219 👍). Bun.CookieMap is a Map-like API for getting & setting cookies. Bun's TypeScript type declarations have been rewritten to eliminate conflicts with Node.js and DOM type definitions. Several bugfixes for node:http, node:crypto, and node:vm.
Thu, 27 Mar 2025 08:51:16 GMT

Bun v1.2.6
https://bun.com/blog/bun-v1.2.6
https://bun.com/blog/bun-v1.2.6
Fixes 74 bugs (addressing 36 👍). Faster, more compatible node:crypto. `timeout` option in Bun.spawn. Support for `module.children` in `node:module`. Connect to PostgreSQL via unix sockets with `Bun.SQL`. Dev Server stability improvements. vm.compileFunction. Initial support for node:test. Faster Express & Fastify.
Tue, 25 Mar 2025 07:46:20 GMT

Bun v1.2.5
https://bun.com/blog/bun-v1.2.5
https://bun.com/blog/bun-v1.2.5
Fixes 75 bugs (addressing 162 👍), and adds +69 passing Node.js tests. Improvements to the frontend dev server, CSS modules support, a full rewrite of Node-API, faster `Sign`, `Verify`, `Hash`, `Hmac` from `node:crypto`, and bug fixes for `node:net` and Bun's bundler
Tue, 11 Mar 2025 08:51:16 GMT

Bun v1.2.4
https://bun.com/blog/bun-v1.2.4
https://bun.com/blog/bun-v1.2.4
Up to 60% faster Bun.build on macOS, codesigning support for single-file executables on macOS, dev server stability improvements, fixes a regression from v1.2.3 affecting Hono, fixes up/down buttons in `bun init` on Windows, and improves Node.js compatibility
Wed, 26 Feb 2025 08:51:16 GMT

Bun v1.2.3
https://bun.com/blog/bun-v1.2.3
https://bun.com/blog/bun-v1.2.3
Fixes 128 bugs (addressing 349 👍). Bun gets a full-featured frontend development toolchain with incredibly fast hot reloading and bundling. Built-in routing for Bun.serve() makes it simpler to build web applications. Bun.SQL gets sql.array, sql fragments, sql.file, and many bugfixes. Node.js compatibility improvements for Buffer & Node-API (napi).
Sat, 22 Feb 2025 02:51:16 GMT

Bun v1.2.2
https://bun.com/blog/bun-v1.2.2
https://bun.com/blog/bun-v1.2.2
Fixes 38 bugs (addressing 129 👍). JavaScript idle memory usage drops by 10–30%. Fixes regression impacting vite build. Reliability improvements to Bun.SQL, Bun.S3Client, Bun's CSS parser. Node.js compatibility improvements: fs.glob, fs.globSync, fs.promises.glob, bugfixes for fs.Dir, fs.accessSync, node:http WebSocket exports
Sat, 01 Feb 2025 05:07:32 GMT

Bun v1.2.1
https://bun.com/blog/bun-v1.2.1
https://bun.com/blog/bun-v1.2.1
Fixes 32 bugs. S3 storage class support, X25519 support in crypto.generateKeyPair. fs.stat uses less memory. node:fs, node:child\_process, and node:process compatibility improvements. CSS parser bugfixes. Zero-filled buffers with `--zero-fill-buffers` flag. Indented inline snapshots in bun test. Improved: String GC Reporting Accuracy. Fixed memory leaks in Bun.serve(), Bun.pathToFileURL, and with some strings. Disable minification in HTML imports.
Mon, 27 Jan 2025 15:35:49 GMT

Bun 1.2
https://bun.com/blog/bun-v1.2
https://bun.com/blog/bun-v1.2
Built-in Postgres client with Bun.sql, built-in S3 object support with Bun.s3, a new text-based lockfile: bun.lock, Express is 3x faster, and a major update on Node.js compatibility.
Wed, 22 Jan 2025 16:00:00 GMT

Bun v1.1.45
https://bun.com/blog/bun-v1.1.45
https://bun.com/blog/bun-v1.1.45
Fixes 13 bugs (addressing 50 👍) 82% of the 'streams' module tests from Node.js' test suite now pass in Bun. node:crypto now implements diffieHellman, getCipherInfo, and X509Certificate. The checkServerIdentity object now matches Node.js' format. Bugfixes in Bun's fs.mkdirSync method, importing with query string
Fri, 17 Jan 2025 15:35:49 GMT

Bun v1.1.44
https://bun.com/blog/bun-v1.1.44
https://bun.com/blog/bun-v1.1.44
Fixes 43 bugs. > 90% of the 'dns' module tests from Node.js' test suite now pass in Bun. You can now build frontend applications on-demand in Bun.serve(). Adds xxHash support to Bun.hash(). Adds support for reading bun.lock using import. Adds --no-install flag to bunx. Improves console.warn output. Fixes bugs in Bun's S3 client, HTMLRewriter, and node:fs compatibility improvements, and more.
Thu, 16 Jan 2025 14:01:24 GMT

Bun v1.1.43
https://bun.com/blog/bun-v1.1.43
https://bun.com/blog/bun-v1.1.43
Bun v1.1.43 introduces 1st-class S3 support, HTML bundling, bun install --filter, V8 heap snapshots, bun install --lockfile-only, bun add --peer, 100% of `node:path` module Node.js test pass, 98% of `node:zlib` tests pass, Bun.file(path).stat(), Bun.file(path).delete(), along with many reliability improvements and bugfixes.
Wed, 08 Jan 2025 16:29:43 GMT

Bun v1.1.42
https://bun.com/blog/bun-v1.1.42
https://bun.com/blog/bun-v1.1.42
Fixes 1 regression from Bun v1.1.41 involving 'use strict' in empty files that impacted Prisma
Sat, 21 Dec 2024 13:57:57 GMT

Bun v1.1.41
https://bun.com/blog/bun-v1.1.41
https://bun.com/blog/bun-v1.1.41
Fixes 12 bugs (addressing 196 👍). JSDOM & happy-dom work more reliably due to node:vm compatibility improvements. Single-file executables on Windows now support custom icons and hiding the console. throw: true in Bun.build throws an error instead of returning errors. bun install gets the --omit=dev|optional|peer options and in .npmrc. A hoisting edgecase in bun install is fixed
Fri, 20 Dec 2024 13:57:57 GMT

Bun v1.1.40
https://bun.com/blog/bun-v1.1.40
https://bun.com/blog/bun-v1.1.40
Fixes 14 bugs. Adds `install.saveTextLockfile` option in bunfig.toml to make the text lockfile format the default. Fixes a bug in package-lock.json migration when manually changing npm URLs to git URLs. Fixes a regression in process.on from Bun v1.1.39. Fixes an issue with BigInt in napi APIs impacting DuckDB. Improves reliability of installing git/github dependencies in bun install. Upgrades WebKit with security & reliability improvements.
Wed, 18 Dec 2024 05:51:42 GMT

Bun's new text-based lockfile
https://bun.com/blog/bun-lock-text-lockfile
https://bun.com/blog/bun-lock-text-lockfile
We're introducing a new text-based lockfile format for bun install. It's GitHub & git-friendly, and makes it easier for teams to migrate from npm, yarn, and pnpm to bun install
Tue, 17 Dec 2024 11:28:30 GMT

Bun v1.1.39
https://bun.com/blog/bun-v1.1.39
https://bun.com/blog/bun-v1.1.39
Fixes 61 bugs (addressing 99 👍). bun.lock is bun's new text-based lockfile. Cached bun install gets 30% faster. fetch() request body streams. 100% of string\_decoder, punycode and querystring Node.js tests pass. Native plugin API for Bun.build() and Rust crate. Implemented expect().toMatchInlineSnapshot(). More accurate heap snapshots. WebSocket server memory reduction. WebKit Upgrade with Error.isError, faster String.prototype.at.
Tue, 17 Dec 2024 11:19:14 GMT

Bun v1.1.38
https://bun.com/blog/bun-v1.1.38
https://bun.com/blog/bun-v1.1.38
Fixes 7 bugs (addressing 14 👍). Fixes debugger bug causing Bun to hang in VSCode terminal. Fixes crash in `postgres` npm package. Fixes TypeScript minification bug, console.log improvements, updated SQLite and c-ares. Adds `reusePort` option to `Bun.listen` and `node:net`, and fixes a bug in `Bun.FileSystemRouter.reload()`. Fixes rare crash in `fetch()`. Fixes assertion failure when re-assigning global modules in `--print` or `--eval`
Fri, 29 Nov 2024 08:00:00 GMT

Bun v1.1.37
https://bun.com/blog/bun-v1.1.37
https://bun.com/blog/bun-v1.1.37
Fixes 62 bugs (addressing 109 👍). Realtime error reporting & test runner in VSCode, self-referencing `import` & `require`, package.json `config` environment variables, improved CSS parser errors, fixes for a Prisma memory leak, a `bun install` regression, `expect.toMatchSnapshot` quote escaping, `node:net` regression impacting `http2-wrapper`, and several other bugfixes and improvements.
Tue, 26 Nov 2024 00:58:38 GMT

Bun v1.1.35
https://bun.com/blog/bun-v1.1.35
https://bun.com/blog/bun-v1.1.35
Fixes 46 bugs (addressing 570 👍). Musl LibC support, JUnit XML test output, 6 MB binary size reduction, `Worker` `preload` option, faster `fs.readFile` for small files, deep equality support for `Headers` and `URLSearchParams`, `node:net` compatibility improvements, unicode import bugfixes, several `bun install` fixes
Tue, 19 Nov 2024 10:54:31 GMT

How Bun supports V8 APIs without using V8 (part 2)
https://bun.com/blog/how-bun-supports-v8-apis-without-using-v8-part-2
https://bun.com/blog/how-bun-supports-v8-apis-without-using-v8-part-2
Rearranging JavaScriptCore types to match V8 code's assumptions
Tue, 05 Nov 2024 07:00:00 GMT

Bun v1.1.34
https://bun.com/blog/bun-v1.1.34
https://bun.com/blog/bun-v1.1.34
Fixes 64 bugs (addressing 62 👍). `Bun.randomUUIDv7`, reduced memory usage for long-running processes, `napi\_type\_tag\_object` and `napi\_check\_object\_type\_tag`, redacted secrets from config logs, `ReadableStream` and HTTP/1.1 spec fixes, several `bun install` and Node.js compatibility improvements
Sat, 02 Nov 2024 05:09:22 GMT

Bun v1.1.33
https://bun.com/blog/bun-v1.1.33
https://bun.com/blog/bun-v1.1.33
Fixes 8 bugs. Fixes JSX symbol collisions with imports, fixes a `bun install` slowdown, skips optional dependency, fixes optional dependency postinstall failures, and fixes an assertion failure in the CSS parser.
Thu, 24 Oct 2024 00:40:17 GMT

Bun v1.1.32
https://bun.com/blog/bun-v1.1.32
https://bun.com/blog/bun-v1.1.32
Fixes 7 bugs and adds crypto.hash() in node:crypto. Warnings in Next.js 15 are fixed. A regression in ESM <> CJS interop impacting Vite config objects is fixed. A crash in Bun.serve() when passing invalid TLS certificates at start is fixed.
Mon, 21 Oct 2024 20:25:58 GMT

Bun v1.1.31
https://bun.com/blog/bun-v1.1.31
https://bun.com/blog/bun-v1.1.31
Fixes 41 bugs (addressing 595 👍). node:http2 server and gRPC server support, ca and cafile support in bun install, Bun.inspect.table, bun build --drop, iterable SQLite queries, iterator helpers, Promise.try, Buffer.copyBytesFrom, and several Node.js compatibility improvements and bugfixes.
Fri, 18 Oct 2024 03:55:06 GMT

Bun v1.1.30
https://bun.com/blog/bun-v1.1.30
https://bun.com/blog/bun-v1.1.30
Fixes 57 bugs (addressing 150 👍) Bun's CSS bundler is here (and very experimental). `bun publish` is a drop-in replacement for `npm publish`. `bun build --bytecode` compiles to bytecode leading to 2x faster start time. Bun.color() formats and normalizes colors. `bun pm whoami` prints your npm username. bun install reads $HOME/.npmrc. bun build --format=cjs outputs CommonJS modules. bun build --target=node now supports Node.js native addons. 30x faster crypto.privateEncrypt() & crypto.publicDecrypt(). Zombie process killer in bun test. --banner and --footer options in bun build. Bun.serve().stop() returns a promise. CryptoHasher now supports HMAC. Bugfixes for node:zlib, node:module, and node:buffer. Lots more bugfixes and Node.js compatibility improvements.
Tue, 08 Oct 2024 10:33:19 GMT

How Bun supports V8 APIs without using V8 (part 1)
https://bun.com/blog/how-bun-supports-v8-apis-without-using-v8-part-1
https://bun.com/blog/how-bun-supports-v8-apis-without-using-v8-part-1
Bun is built on JavaScriptCore, not V8. Here's how we're implementing V8's C++ API on top of it.
Mon, 30 Sep 2024 07:00:00 GMT

Bun v1.1.29
https://bun.com/blog/bun-v1.1.29
https://bun.com/blog/bun-v1.1.29
Fixes 21 bugs (addressing 22 👍). Fixes issue with proxying requests with axios. N-API (napi) support in compiled C. Faster typed arrays in `bun:ffi` with 'buffer' type. Fixes issue with bundling imported .wasm files in `bun build`. Fixes regression with `bun build` from v1.1.28. Fixes snapshot regression in `bun test`. Fixes bug with argument validation in `Bun.build` plugins.
Fri, 20 Sep 2024 08:54:53 GMT

Bun v1.1.28
https://bun.com/blog/bun-v1.1.28
https://bun.com/blog/bun-v1.1.28
This release fixes 40 bugs (addressing 51 👍). Compile & run C from JavaScript. 30x faster path.resolve. Named pipes on Windows. Several Node.js compatibility improvements and bugfixes.
Wed, 18 Sep 2024 14:36:14 GMT

Compile and run C in JavaScript
https://bun.com/blog/compile-and-run-c-in-js
https://bun.com/blog/compile-and-run-c-in-js
Bun now supports compiling and running C from JavaScript to make using systems libraries easier.
Wed, 18 Sep 2024 14:36:14 GMT

Bun v1.1.27
https://bun.com/blog/bun-v1.1.27
https://bun.com/blog/bun-v1.1.27
Fixes 130 bugs (addressing 250 👍). `bun pm pack`, faster `node:zlib`. Static routes in Bun.serve(). ReadableStream support in response.clone() & request.clone(). Per-request timeouts. Cancel method in ReadableStream is called. `bun run` handles CTRL + C better. Faster buffered streams. `bun outdated` package filtering. Watch arbtirary file types in --hot and --watch. Fixes to proxies on Windows. Several Node.js compatibility improvements.
Sat, 07 Sep 2024 10:33:38 GMT

Bun v1.1.26
https://bun.com/blog/bun-v1.1.26
https://bun.com/blog/bun-v1.1.26
Fixes 9 bugs (addressing 652 👍). `bun outdated` shows outdated dependencies. Bun.serve() gets a new `idleTimeout` option and `subscriberCount(topic: string)` for a count of websocket clients subscribed to a topic. `test.only` in bun:test now skips tests before and after instead of only after. expect.assertions(n) in async functionn is fixed. "use strict" in CommonJS modules is now preserved. Plus, more node.js compatibility improvements and bug fixes.
Sat, 24 Aug 2024 07:24:26 GMT

Bun v1.1.25
https://bun.com/blog/bun-v1.1.25
https://bun.com/blog/bun-v1.1.25
Fixes 42 bugs (addressing 470 👍). Support for `node:cluster` and V8's C++ API. Faster WebAssembly on Windows with OMGJIT. 5x faster S3 uploads with @aws-sdk/client-s3, Worker in standalone executables, and more Node.js compatibility improvements and bug fixes.
Wed, 21 Aug 2024 05:25:44 GMT

Bun v1.1.23
https://bun.com/blog/bun-v1.1.23
https://bun.com/blog/bun-v1.1.23
Support for `TextEncoderStream` and `TextDecoderStream`, 50% faster `console.log(string)`, support for `Float16Array`, Node.js<>Bun IPC on Windows, truncate large arrays in `console.log()`, and many more bug fixes and Node.js compatibility improvements.
Wed, 14 Aug 2024 00:02:32 GMT

Bun v1.1.22
https://bun.com/blog/bun-v1.1.22
https://bun.com/blog/bun-v1.1.22
Fixes 79 bugs (addressing 93 👍). Express is now 3x faster in Bun, ES modules load faster on Windows, 10% faster Bun.serve() at POST requests, source maps in `bun build --compile`. Memory usage reductions to `--hot`, Bun.serve(), and imports. `Uint8Array.toBase64()`, `Uint8Array.toHex()`, and lots of Node.js compatibiltiy improvements and bugfixes.
Wed, 07 Aug 2024 22:01:19 GMT

Bun v1.1.21
https://bun.com/blog/bun-v1.1.21
https://bun.com/blog/bun-v1.1.21
Fixes 72 bugs (addressing 63 👍). 30% faster fetch() decompression, New --fetch-preconnect flag, improved Remix support, Bun gets 4 MB smaller on Linux, bundle packages excluding dependencies, many bundler fixes and node compatibility improvements.
Sat, 27 Jul 2024 06:43:53 GMT

Bun v1.1.19
https://bun.com/blog/bun-v1.1.19
https://bun.com/blog/bun-v1.1.19
Fixes 54 bugs (addressing 248 👍). JavaScript gets faster on Windows. Raspberry Pi 4 support returns. `\_auth` support in `.npmrc`. `bun install` preserves package.json indentation. `aws-cdk-lib` support. Memory leak fixes in `new Response(request)` and `fs.readdir`. Several reliability improvements. Statically linked UCRT on Windows.
Fri, 12 Jul 2024 21:47:25 GMT

Bun v1.1.18
https://bun.com/blog/bun-v1.1.18
https://bun.com/blog/bun-v1.1.18
Fixes 55 bugs (addressing 493 👍). Support for npmrc. Improved constant folding & enum inlining. Improved console.log output for functions. Fixes patching dependencies in workspaces. Fixes several bugs in `bun install` when linking binaries. Fixes a crash in `dns.lookup`, and normalizes DNS errors to better match Node. Fixes an assertion failure in `Bun.escapeHTML`. Upgrades JavaScriptCore.
Wed, 03 Jul 2024 23:28:26 GMT

Bun v1.1.17
https://bun.com/blog/bun-v1.1.17
https://bun.com/blog/bun-v1.1.17
Fixes 4 bugs. Fixes a crash in bun repl. Makes fs.readdirSync 5% faster on macOS in small directories. Fixes "ws" module not calling the callback in "send" method. Fixes a crash when reading a corrupted lockfile in bun install. Makes macOS event loop a smidge faster.
Tue, 25 Jun 2024 03:37:20 GMT

Bun v1.1.16
https://bun.com/blog/bun-v1.1.16
https://bun.com/blog/bun-v1.1.16
Fixes 41 bugs (addressing 221 👍). lcov code coverage reports in bun test, Install dependencies from private git repositories including Gitlab and Bitbucket. `Buffer.from(string, "base64")` gets 6x - 30x faster on large input. Bug fixes to `bun patch`, `bun install`, N-AIi addons, transpiler bugfixes and Node.js compatibility improvements.
Sun, 23 Jun 2024 02:34:19 GMT

Bun v1.1.14
https://bun.com/blog/bun-v1.1.14
https://bun.com/blog/bun-v1.1.14
Fixes 63 bugs (addressing 519 👍). Patch node\_modules with bun patch. ORM-less object mapping in bun:sqlite. Log fetch() calls as curl commands. Node.js compatibility improvements. bun install bugfixes, bun:sqlite bugfixes, WebSocket fixes, Windows bugfixes
Wed, 19 Jun 2024 08:02:22 GMT

Bun v1.1.13
https://bun.com/blog/bun-v1.1.13
https://bun.com/blog/bun-v1.1.13
Fixes 97 bugs (addressing 211 👍). Reliability improvements to bun install, WebSocket server, fetch, worker\_threads. worker\_threads now supports eval. `URL.createObjectURL`, stack trace error location improvements, several `bun install` fixes, and many crashes and bugs fixed.
Wed, 05 Jun 2024 08:00:22 GMT

Bun v1.1.11
https://bun.com/blog/bun-v1.1.11
https://bun.com/blog/bun-v1.1.11
Fixes 36 bugs (addressing 362 👍). bun update saves dependency updates to package.json. A peer dependencies resolution bug in bun install is fixed. setTimeout gets 5x faster throughput on Linux. Node.js compatibility improvements to fs, zlib, timers, http, dgram and module. Event loop improvements on macOS. Windows reliability improvements.
Sat, 01 Jun 2024 08:00:22 GMT

Bun v1.1.10
https://bun.com/blog/bun-v1.1.10
https://bun.com/blog/bun-v1.1.10
Fixes 20 bugs. 2x faster uncached bun install on Windows. fetch() uses up to 2.8x less memory. Several bugfixes to bun install, sourcemaps, Windows reliability improvements and Node.js compatibility improvements
Fri, 24 May 2024 22:17:59 GMT

Bun v1.1.9
https://bun.com/blog/bun-v1.1.9
https://bun.com/blog/bun-v1.1.9
Fixes 67 bugs (addressing 150 👍). Fixes to: workspaces in `bun install`, sourcemaps in bun build, IPv6 & VPN connectivity, Loading UNC paths, junctions, symlinks, and pnpm on Windows, `fetch()` gets faster, added `dns.prefetch()` API, `atob()` gets 8x faster, `toString('base64url')` gets 5x faster, expect().toBeReturned() matcher, Node.js compatibility improvements, Bun Shell fixes, and lots more bugfixes.
Wed, 22 May 2024 00:40:48 GMT

Bun v1.1.8
https://bun.com/blog/bun-v1.1.8
https://bun.com/blog/bun-v1.1.8
Fixes 54 bugs (addressing 184 👍). Support for `process.on("uncaughtException")` and `process.on("unhandledRejection")`, Brotli support in `node:zlib`, Faster JSON.parse, `[Symbol.dispose]` in Bun APIs, fixes lots of crashes on Windows, and many other bugfixes.
Fri, 10 May 2024 11:16:44 GMT

Bun v1.1.7
https://bun.com/blog/bun-v1.1.7
https://bun.com/blog/bun-v1.1.7
Fixes 28 bugs (addressing 11 👍). Glob workspace names in bun install. Asymmetric matcher support in expect.extends() equals. bunx --version. Bugfixes to JSX transpilation, sourcemaps, cross-compilation of standalone executables, bun shell, RegExp, Worker on Windows, and Node.js compatibility improvements.
Fri, 03 May 2024 14:02:22 GMT

Bun v1.1.6
https://bun.com/blog/bun-v1.1.6
https://bun.com/blog/bun-v1.1.6
Fixes 10 bugs (addressing 512 👍). UDP sockets! node:dgram! DataDog and ClickHouseDB! Fixes a bug impacting SvelteKit. Array#sort gets 15% - 135% faster. Fixes a regression in node:http from v1.1.5. Node.js compatibiltiy improvements and bugfixes.
Sun, 28 Apr 2024 08:48:12 GMT

Bun v1.1.5
https://bun.com/blog/bun-v1.1.5
https://bun.com/blog/bun-v1.1.5
Fixes 64 bugs (addressing 101 👍). Cross-compile standalone JavaScript & TypeScript executables to other platforms with bun build --compile. import any file as text via the `type: 'text'` import attribute. Introduces a new crash reporter. package.json with comments and trailing commas. Fixes a bug where `bun run --filter` exited with 0. Fixes a bug in bun install with file: dependencies. Fixes bugs in `node:tls`, `node:crypto`, `node:readline`, `node:http`, `node:worker\_threads`
Fri, 26 Apr 2024 23:13:58 GMT

bun.report is Bun's new crash reporter
https://bun.com/blog/bun-report-is-buns-new-crash-reporter
https://bun.com/blog/bun-report-is-buns-new-crash-reporter
How we built an anonymous Zig/C++ crash reporter that doesn't require debug symbols to be shipped with the application.
Fri, 26 Apr 2024 16:00:00 GMT

Bun v1.1.4
https://bun.com/blog/bun-v1.1.4
https://bun.com/blog/bun-v1.1.4
Fixes 40 bugs (addressing 84 👍 reactions). `bun run --filter <workspace> <script>` lets you run multiple workspace scripts in parallel. Reinstalls get up to 50% faster in bun install. Important reliability fixes to bun install. bun:sqlite supports `using` for resource cleanup and has a few bugfixes. Memory leak impacting Next.js Standalone & Web Streams is fixed. Node.js compatibility improvements to fs and child\_process. Fix for 'Connection closed' in fetch(). A few bugfixes for Bundows.
Tue, 16 Apr 2024 18:18:13 GMT

Bun v1.1.3
https://bun.com/blog/bun-v1.1.3
https://bun.com/blog/bun-v1.1.3
Fixes 5 bugs. bun install gets 50% faster on Windows. A bug that could cause bun install to hang in rare cases has been fixed. A bug where some errors in bun install would not produce a non-zero exit code has been fixed. A bug that could cause specific certain combinations of dependencies to fail to install has been fixed. A bug on Windows where CTRL + C on cmd.exe after exiting bun would not behave as expected has been fixed. A bug where missing permissions on Windows for reading a directory could lead to a crash has been fixed.
Mon, 08 Apr 2024 15:48:44 GMT

Bun v1.1.2
https://bun.com/blog/bun-v1.1.2
https://bun.com/blog/bun-v1.1.2
Fixes 4 bugs (addressing 44 👍 reactions). EBUSY on Windows in vite dev, next dev, and saving bun.lockb has been fixed. Object cloning gets 6x faster. Bun Shell gets support for seq, yes, basename and dirname. A TypeScript parsing edgecase has been fixed. A bug causing 'unreachable code' errors has been fixed. fs.watch on Windows has been rewritten to improve performance and reliability.
Sat, 06 Apr 2024 00:37:28 GMT

Bun v1.1.1
https://bun.com/blog/bun-v1.1.1
https://bun.com/blog/bun-v1.1.1
Fixes 20 bugs (addressing 60 👍). Add subshell and positional argument support to Bun Shell, fixing an issue with bun install + sharp on Windows. Printed source code in errors no longer fill up your terminal. Upgrades JavaScriptCore, which includes performance improvements to RegExp, typed arrays, String indexOf and String replace. Error objects and JIT'd function calls use less memory. Fixes several bugs with bun install on Windows. Fixes a bug with Bun.serve() on Windows. Fixes a TOML parser bug impacting escape sequences and windows paths in .toml files
Thu, 04 Apr 2024 15:29:30 GMT

Bun 1.1
https://bun.com/blog/bun-v1.1
https://bun.com/blog/bun-v1.1
Bun now supports Windows!
Mon, 01 Apr 2024 16:00:00 GMT

Bun v1.0.36
https://bun.com/blog/bun-v1.0.36
https://bun.com/blog/bun-v1.0.36
Fixes 13 bugs. Adds support for `fs.openAsBlob` and `fs.opendir`, fixes edgecase in bun install with multiple `bin` entries in `package.json`, fixes `bun build --target bun` encoding, fixes bug with process.stdin & process.stdout, fixes bug in http2, fixes bug with .env in bun run, fixes various Bun shell bugs and improves Node.js compatibility.
Fri, 29 Mar 2024 07:03:02 GMT

Bun v1.0.34
https://bun.com/blog/bun-v1.0.34
https://bun.com/blog/bun-v1.0.34
Fixes 7 bugs, bunx uses less memory, bun install gets faster on Docker & WSL, a conflicting devDependency hoisting bug is fixed, a cyclical CommonJS & ESM import crash is fixed, cross-mount fs.cp & fs.copyFile get 50% faster on Linux, and reliability improvements for bun install & bun's runtime
Fri, 22 Mar 2024 12:49:41 GMT

Bun v1.0.32
https://bun.com/blog/bun-v1.0.32
https://bun.com/blog/bun-v1.0.32
Fixes 13 bugs, including 3 I/O regressions from v1.0.31. Improves Node.js compatibility. 'ws' package can now send & receive ping/pong events. util.promisify'd setTimeout setInterval, setImmediate work now. FileHandle methods have been implemented
Sun, 17 Mar 2024 15:30:16 GMT

Bun v1.0.33
https://bun.com/blog/bun-v1.0.33
https://bun.com/blog/bun-v1.0.33
Fixes 2 bugs, including a bug with the mv command in Bun Shell and an error in node:crypto when verifying signatures
Sun, 17 Mar 2024 15:30:16 GMT

Bun v1.0.31
https://bun.com/blog/bun-v1.0.31
https://bun.com/blog/bun-v1.0.31
Fixes 54 bugs (addresses 113 👍 reactions), introduces `bun --print`, `<stdin> | bun run -`, `bun add --trust`, `fetch()` with Unix sockets, fixes macOS binary size regression, fixes high CPU usage bug in spawn() on older linux, adds `util.styleText`, Node.js compatibiltiy improvements, bun install bugfixes, and bunx bugfixes
Thu, 14 Mar 2024 22:19:59 GMT

Bun v1.0.30
https://bun.com/blog/bun-v1.0.30
https://bun.com/blog/bun-v1.0.30
Fixes 27 bugs (addressing 103 👍 reactions), fixes an 8x perf regression in Bun.serve(), adds a new `--conditions` flag to `bun build` and Bun's runtime, adds support for `expect.assertions()` and `expect.hasAssertions()` in Bun's test runner, fixes crashes and improves Node.js compatibility
Mon, 04 Mar 2024 09:25:31 GMT

Bun v1.0.29
https://bun.com/blog/bun-v1.0.29
https://bun.com/blog/bun-v1.0.29
Fixes 8 bugs. Bun.stringWidth(a) is a ~6,756x faster drop-in replacement for the popular 'string-width' package. bunx checks for updates more frequently. Adds expect().toBeOneOf() in bun:test. Memory leak impacting Prisma is fixed. Shell now supports advanced redirects like '2>&1', '&>'. Reliability improvements to bunx, bun install, WebSocket client, and Bun Shell
Fri, 23 Feb 2024 04:50:50 GMT

Bun v1.0.28
https://bun.com/blog/bun-v1.0.28
https://bun.com/blog/bun-v1.0.28
Fixes 6 bugs (addressing 26 👍 reactions). Fixes bugs impacting Prisma and Astro, 'events', 'readline', and 'http2'. Fixes a bug in Bun Shell involving stdin redirection and fixes bugs in bun:test with test.each and describe.only
Mon, 19 Feb 2024 23:03:46 GMT

Bun v1.0.27
https://bun.com/blog/bun-v1.0.27
https://bun.com/blog/bun-v1.0.27
Fixes 72 bugs (addressing 192 👍 reactions), Bun Shell supports throwing on non-zero exit codes, stream Response bodies using async generators, improves reliability of fetch(), http2 client, Bun.Glob and Bun Shell. Fixes a regression with bun --watch on Linux. Improves Node.js compatibility
Sat, 17 Feb 2024 05:57:22 GMT

Bun v1.0.26
https://bun.com/blog/bun-v1.0.26
https://bun.com/blog/bun-v1.0.26
Fixes 30 bugs (addressing 60 👍 reactions), adds support for multi-statement queries in bun:sqlite, makes bun --watch more reliable in longer-running sessions, Bun.FileSystemRouter now supports more than 64 routes, fixes a bug with expect().toStrictEqual(), fixes 2 bugs with error.stack, improves Node.js compatibility
Sat, 03 Feb 2024 16:40:08 GMT

Bun v1.0.25
https://bun.com/blog/bun-v1.0.25
https://bun.com/blog/bun-v1.0.25
Fixes 4 bugs, adds vm.createScript. Fixes a crash in fs.readFile, a crash in Bun.file().text(), a crash in IPC, and a transpiler bug involving loose equals
Sun, 21 Jan 2024 14:30:03 GMT

Bun v1.0.24
https://bun.com/blog/bun-v1.0.24
https://bun.com/blog/bun-v1.0.24
Fixes 9 bugs and adds Bun Shell, a fast cross-platform shell with seamless JavaScript interop. Fixes a socket timeout bug, a potential crash when socket closes, a Node.js compatibility issue with Hapi, a process.exit bug, and bun install binlinking bug, bun inspect regression, and bun:test expect().toContain bug
Sat, 20 Jan 2024 05:17:49 GMT

The Bun Shell
https://bun.com/blog/the-bun-shell
https://bun.com/blog/the-bun-shell
The Bun Shell is a cross-platform shell that allows you to run shell scripts in JavaScript & TypeScript
Sat, 20 Jan 2024 05:17:49 GMT

Bun v1.0.23
https://bun.com/blog/bun-v1.0.23
https://bun.com/blog/bun-v1.0.23
Fixes 40 bugs (addressing 194 👍 reactions). import & embed sqlite databases in Bun, Resource Management ('using' TC39 stage3) support, bundler improvements when building for Node.js, bugfix for peer dependency resolution, semver bugfix, 4% faster TCP on linux, Node.js compatibility improvements and more
Tue, 16 Jan 2024 08:17:21 GMT

Bun v1.0.22
https://bun.com/blog/bun-v1.0.22
https://bun.com/blog/bun-v1.0.22
Fixes `bun install` issues on Vercel, adds `performance.mark()` APIs, adds `child\_process` support for extra pipes, makes `Buffer.concat` 10% - 400% faster, adds `toBeEmptyObject` and `toContainKeys` matchers, fixes `console.table` width using emojis, and adds support for `argv` and `execArgv` options in `worker\_threads`.
Tue, 09 Jan 2024 22:27:17 GMT

Bun v1.0.21
https://bun.com/blog/bun-v1.0.21
https://bun.com/blog/bun-v1.0.21
Fixes 33 bugs (addressing 80 👍 reactions). console.table() support. Bun.write, Bun.file, and bun:sqlite use less memory. Large file uploads with FormData use less memory. bun:sqlite error messages get more detailed. Memory leak in errors from node:fs fixed. Node.js compatibility improvements, and many crashes fixed
Tue, 02 Jan 2024 02:27:00 GMT

Bun v1.0.20
https://bun.com/blog/bun-v1.0.20
https://bun.com/blog/bun-v1.0.20
Reduced memory usage for fs.readlink, fs.writeFile, fs.stat and HTMLRewriter. Fixes a regression where setTimeout caused high CPU usage on Linux. Bun.spawn shows how much CPU & memory the process used. HTMLRewriter.transform now supports strings and ArrayBuffer. fs.writeFile() and fs.readFile() now support hex & base64 encodings
Sun, 24 Dec 2023 14:05:40 GMT

Bun v1.0.19
https://bun.com/blog/bun-v1.0.19
https://bun.com/blog/bun-v1.0.19
Fixes 26 bugs (addressing 92 👍 reactions). Use @types/bun instead of bun-types. Fixes --frozen-lockfile bug. bcrypt & argon2 packages now work. setTimeout & setInterval get 4x higher throughput. module mocks in bun:test resolve specifiers. Optimized spawnSync() for large stdio on Linux. Bun.peek() gets 90x faster, expect(map1).toEqual(map2) gets 100x faster. Bugfixes to NAPI, bun install, and Node.js compatibility improvements
Fri, 22 Dec 2023 08:26:18 GMT

Bun v1.0.18
https://bun.com/blog/bun-v1.0.18
https://bun.com/blog/bun-v1.0.18
Fixes 27 bugs (addressing 28 👍 reactions). A hang impacting create-vite & create-next & stdin has been fixed. Lifecycle scripts reporting "node" or "node-gyp" not found has been fixed. expect().rejects works like Jest now, and more bug fixes
Thu, 14 Dec 2023 07:54:01 GMT

Bun v1.0.17
https://bun.com/blog/bun-v1.0.17
https://bun.com/blog/bun-v1.0.17
Fixes 15 bugs (addressing 152 👍 reactions). bun install postinstall scripts run for top 500 packages, `bunx supabase` starts 30x faster than `npx supabase`, `bunx esbuild` starts 50x faster than `npx esbuild` and bugfixes to bun install
Tue, 12 Dec 2023 11:36:17 GMT

Bun v1.0.16
https://bun.com/blog/bun-v1.0.16
https://bun.com/blog/bun-v1.0.16
Fixes 49 bugs (addressing 38 👍 reactions). Concurrent IO for Bun.file & Bun.write gets 3x faster and now supports Google Cloud Run & Vercel, Bun.write auto-creates the parent directory if it doesn't exist, `expect.extend` inside of preload works, `napi\_create\_object` gets 2.5x faster, bugfix for module resolution impacting Astro v4 and p-limit, console.log bugfixes
Sun, 10 Dec 2023 13:28:21 GMT

Bun v1.0.15
https://bun.com/blog/bun-v1.0.15
https://bun.com/blog/bun-v1.0.15
Fixes 23 bugs (addressing 117 👍 reactions), `tsc` starts 2x faster, prettier 40% faster. Stable `WebSocket` client, syntax-highlighted errors, cleaner stack traces, add custom test matchers with `expect.extend()`, TensorFlow.js support, fs.readdir recursive is 40x faster than in Node, and more.
Sat, 02 Dec 2023 14:30:15 GMT

Bun v1.0.14
https://bun.com/blog/bun-v1.0.14
https://bun.com/blog/bun-v1.0.14
Introduces `Bun.Glob` - a fast glob matcher, fixes a race condition when extracting dependencies during `bun install`, improves TypeScript module resolution in `node\_modules`, makes error messages easier to read, and more fixes.
Wed, 22 Nov 2023 22:54:46 GMT

Bun v1.0.13
https://bun.com/blog/bun-v1.0.13
https://bun.com/blog/bun-v1.0.13
Fixes 6 bugs (addressing 317 👍 reactions). 'http2' module & gRPC.js work now. Vite 5 & Rollup 4 work. Implements process.report.getReport(), improves support for ES5 'with' statements, fixes a regression in bun install, fixes a crash when printing exceptions, fixes a Bun.spawn bug, and fixes a peer dependencies bug
Sat, 18 Nov 2023 08:05:44 GMT

Bun v1.0.12
https://bun.com/blog/bun-v1.0.12
https://bun.com/blog/bun-v1.0.12
Fixes 24 bugs, makes bun's CLI help menus easier to read, adds support for `bun -e`, `bun --env-file`, `server.url`, `import.meta.env`, `expect.unreachable()`, improves support for module mocks, allows importing builtin modules at bundle-time, and improves Node.js compatibility
Thu, 16 Nov 2023 08:05:44 GMT

Bun v1.0.11
https://bun.com/blog/bun-v1.0.11
https://bun.com/blog/bun-v1.0.11
Fixes 5 bugs, adds Bun.semver, fixes a bug in bun install and fixes bugs impacting astro and @google-cloud/storage
Wed, 08 Nov 2023 07:39:33 GMT

Bun v1.0.10
https://bun.com/blog/bun-v1.0.10
https://bun.com/blog/bun-v1.0.10
Fixes 14 bugs (addressing 102 👍 reactions), node:http gets 14% faster, stability improvements to Bun for Linux ARM64, bun install bugfix, and node:http bugfixes
Tue, 07 Nov 2023 07:39:33 GMT

Bun v1.0.9
https://bun.com/blog/bun-v1.0.9
https://bun.com/blog/bun-v1.0.9
Fixes a glibc symbol version error, illegal instruction error, a Bun.spawn bug, an edgecase with peer dependency installs, and a JSX transpiler bugfix
Sun, 05 Nov 2023 10:13:16 GMT

Bun v1.0.8
https://bun.com/blog/bun-v1.0.8
https://bun.com/blog/bun-v1.0.8
Fixes 138 bugs (addressing 257 👍 reactions), makes `require()` use 30% less memory, adds module mocking to `bun test`, and improves reliability of `bun install` and Bun.spawn
Thu, 02 Nov 2023 18:51:31 GMT

Bun v1.0.7
https://bun.com/blog/bun-v1.0.7
https://bun.com/blog/bun-v1.0.7
Fixes 59 bugs (addressing 78 👍 reactions), support for optional `peerDependencies`, improvements to Node.js compatibility, and more stability for `bun install`.
Fri, 20 Oct 2023 23:39:51 GMT

Bun v1.0.6
https://bun.com/blog/bun-v1.0.6
https://bun.com/blog/bun-v1.0.6
Fixes 3 bugs (addressing 85 👍 reactions), implements support for the 'overrides' & 'resolutions' fields in package.json and a regression impacting Docker usage with Bun
Wed, 11 Oct 2023 23:39:51 GMT

Bun v1.0.5
https://bun.com/blog/bun-v1.0.5
https://bun.com/blog/bun-v1.0.5
Fixes 41 bugs + a memory leak in `fetch()`, `KeyObject` support in `crypto` module, import package-lock.json, install peer dependencies, bun pm migrate subcommand, bun install bugfixes, and `toEqualIgnoringWhitespace` matcher in `bun:test`
Wed, 11 Oct 2023 10:33:40 GMT

Bun v1.0.4
https://bun.com/blog/bun-v1.0.4
https://bun.com/blog/bun-v1.0.4
Bun v1.0.4 fixes 62 bugs, adds `server.requestIP`, supports virtual modules in runtime plugins, fixes many bun install bugs, and reduces memory consumption in `Bun.serve()`
Tue, 03 Oct 2023 12:00:00 GMT

Bun v1.0.3
https://bun.com/blog/bun-v1.0.3
https://bun.com/blog/bun-v1.0.3
emitDecoratorMetadata, Nest.js support, better private registry support, bunx bugfix, console.log() depth 8 -> 2, silence .env loaded message, and many bugfixes
Fri, 22 Sep 2023 12:00:00 GMT

Bun v1.0.2
https://bun.com/blog/bun-v1.0.2
https://bun.com/blog/bun-v1.0.2
Faster watch mode, bunx @latest bugfix, Bun uses V8's date parser, bugfixes to node:readline, node:dns, bun run, http streaming, transpiler, node:tty and more
Fri, 15 Sep 2023 16:51:51 GMT

Bun v1.0.1
https://bun.com/blog/bun-v1.0.1
https://bun.com/blog/bun-v1.0.1
Named imports for .json & .toml files, bugfixes to bun install, node:path, Buffer. Support for NODE\_TLS\_REJECT\_UNAUTHORIZED=0
Tue, 12 Sep 2023 15:19:15 GMT

Bun 1.0
https://bun.com/blog/bun-v1.0
https://bun.com/blog/bun-v1.0
Bun is stable and ready for production.
Fri, 08 Sep 2023 01:40:20 GMT

Bun v0.8.1
https://bun.com/blog/bun-v0.8.1
https://bun.com/blog/bun-v0.8.1
Bun.serve() gets unix domain socket support, a performance regression has been fixed, and bugs in bun install, node:http and napi have been fixed
Sat, 26 Aug 2023 00:21:35 GMT

Bun v0.8.0
https://bun.com/blog/bun-v0.8.0
https://bun.com/blog/bun-v0.8.0
Bun gets debugger support, fetch streaming, and `bun update`. ReadStream and WriteStream from `node:tty` are implemented, including raw mode on `process.stdin`. SvelteKit now works in Bun. Plus bug fixes and stability improvements.
Thu, 24 Aug 2023 00:21:35 GMT

Bun v0.7.3
https://bun.com/blog/bun-v0.7.3
https://bun.com/blog/bun-v0.7.3
bun test gets code coverage reporting. bun test -t pattern lets you filter tests to run by regex pattern. Fixes a crash in bun:sqlite, node.js compatiblity improvements, and more.
Sun, 06 Aug 2023 12:12:00 GMT

Bun v0.7.2
https://bun.com/blog/bun-v0.7.2
https://bun.com/blog/bun-v0.7.2
worker\_threads, BroadcastChannel, diagnostics\_channel, Node.js compatibility improvements, bun ., bugfixes and 2 memory leaks fixed
Thu, 03 Aug 2023 12:00:00 GMT

Bun v0.7.1
https://bun.com/blog/bun-v0.7.1
https://bun.com/blog/bun-v0.7.1
Node.js compatibility improvements for Vite & frameworks. Better workspace support in bun installl & a bugfix for private registries. ES Modules load 30% faster. `vite dev` starts 90% faster on Linux. Transpiler bugfixes. fetch() file urls. MessagePort & MessageChannel.
Sat, 29 Jul 2023 00:57:49 GMT

Bun v0.7.0
https://bun.com/blog/bun-v0.7.0
https://bun.com/blog/bun-v0.7.0
vite dev support, Workers, bun --smol, WebSocket.ping(), structuredClone(), serialize() and better Node.js compatibility
Fri, 21 Jul 2023 00:57:49 GMT

Bun v0.6.14
https://bun.com/blog/bun-v0.6.14
https://bun.com/blog/bun-v0.6.14
Better support for Node.js `process` and lots of fixed bugs.
Wed, 12 Jul 2023 00:57:49 GMT

Bun v0.6.13
https://bun.com/blog/bun-v0.6.13
https://bun.com/blog/bun-v0.6.13
Mock `Date`, 10x faster base64 encoding, WebSocket client reliability improvements, support for postgres tls and nodemailer, and various bug fixes.
Tue, 04 Jul 2023 10:00:00 GMT

CommonJS is not going away
https://bun.com/blog/commonjs-is-not-going-away
https://bun.com/blog/commonjs-is-not-going-away
CommonJS is here to stay, and that's okay. Better tooling will solve today's developer experience issues.
Fri, 30 Jun 2023 23:18:20 GMT

Bun v0.6.12
https://bun.com/blog/bun-v0.6.12
https://bun.com/blog/bun-v0.6.12
Sourcemapped stack traces at runtime, Node.js compatibility improvements, Bun.file(path).exists, minifier and bundler bugfixes
Fri, 30 Jun 2023 20:15:43 GMT

Bun v0.6.10
https://bun.com/blog/bun-v0.6.10
https://bun.com/blog/bun-v0.6.10
Reduced memory usage, fs.watch(), better CommonJS support, improvements to `bun test`, `bun install`, and many bugfixes.
Mon, 26 Jun 2023 20:15:43 GMT

Bun v0.6.9
https://bun.com/blog/bun-v0.6.9
https://bun.com/blog/bun-v0.6.9
Memory usage reductions in Bun.serve(), bun install, module imports, and crypto hashing. Crash in CommonJS modules fixed, plus additional bugfixes.
Tue, 13 Jun 2023 15:05:43 GMT

Bun v0.6.8
https://bun.com/blog/bun-v0.6.8
https://bun.com/blog/bun-v0.6.8
Password hashing, function mocking, debugging, and bug squashing
Fri, 09 Jun 2023 12:00:00 GMT

Bun v0.6.7
https://bun.com/blog/bun-v0.6.7
https://bun.com/blog/bun-v0.6.7
Discord.js, Prisma, and Puppeteer support, faster node:crypto hashing, and lots of bug fixes
Fri, 02 Jun 2023 00:00:00 GMT

Bun v0.6.6
https://bun.com/blog/bun-v0.6.6
https://bun.com/blog/bun-v0.6.6
Lots of improvements to `bun test`, including Github Actions support, `bun test --only`, `test.if()`, `describe.skip()`, and more matchers
Wed, 31 May 2023 17:56:51 GMT

JavaScript Macros in Bun
https://bun.com/blog/bun-macros
https://bun.com/blog/bun-macros
Call JavaScript functions at bundle-time and inline results into the AST
Wed, 31 May 2023 12:01:00 GMT

Bun v0.6.5
https://bun.com/blog/bun-v0.6.5
https://bun.com/blog/bun-v0.6.5
Native CommonJS support, $npm\_lifecycle\_event, bugfix for Bun.serve() with streaming files, bugfix for Node.js createConnection and a bundler bugfix
Mon, 29 May 2023 00:00:00 GMT

Bun v0.6.4
https://bun.com/blog/bun-v0.6.4
https://bun.com/blog/bun-v0.6.4
Up to 80% faster bun test, test timeouts, timezone support, bundler bugfixes, console.log() improvements, node:http bugfixes, and more
Fri, 26 May 2023 00:00:00 GMT

Bun v0.6.3
https://bun.com/blog/bun-v0.6.3
https://bun.com/blog/bun-v0.6.3
Introducing `node:vm` support, support for `socket.io` and `mongodb`, `test.todo()`, and many bug fixes for the bundler.
Mon, 22 May 2023 18:06:10 GMT

Bun v0.6.2
https://bun.com/blog/bun-v0.6.2
https://bun.com/blog/bun-v0.6.2
Up to 20% faster JSON.parse, 15% faster JSON.stringify, and Proxy gets faster. A couple bugfixes to the minifier and bundler
Wed, 17 May 2023 12:00:00 GMT

The Bun Bundler
https://bun.com/blog/bun-bundler
https://bun.com/blog/bun-bundler
The Bun toolkit gets a new addition. Bun's fast native bundler is now in beta.
Tue, 16 May 2023 12:01:00 GMT

Bun v0.6.0
https://bun.com/blog/bun-v0.6.0
https://bun.com/blog/bun-v0.6.0
A new JavaScript bundler, standalone executables, and lots of new features and improvements
Tue, 16 May 2023 12:00:00 GMT

Bun v0.5.9
https://bun.com/blog/bun-v0.5.9
https://bun.com/blog/bun-v0.5.9
Introducing watch mode using `bun --watch`, tarball dependencies in `bun install`, and lots of bug fixes and compatibility improvements.
Tue, 04 Apr 2023 00:00:00 GMT

Bun v0.5.8
https://bun.com/blog/bun-v0.5.8
https://bun.com/blog/bun-v0.5.8
Introducing `expect()` snapshots in `bun test`, preloading modules using `bun --preload`, basic glob star support in bun install, improvements to Web & Node.js compatibility, lots of bug fixes, and a teaser of what's next.
Sat, 18 Mar 2023 00:00:00 GMT

Bun has docs now
https://bun.com/blog/bun-has-docs-now
https://bun.com/blog/bun-has-docs-now
Bun has docs now? Bun has docs now.
Fri, 24 Feb 2023 12:00:00 GMT

Bun v0.5.7
https://bun.com/blog/bun-v0.5.7
https://bun.com/blog/bun-v0.5.7
Support for `FormData` and `git` dependencies, better `setTimeout()` compatibility, `bun wiptest` is now `bun test`, and better support on AWS Lambda and GitHub Actions.
Fri, 24 Feb 2023 00:00:50 GMT

Bun v0.5.6
https://bun.com/blog/bun-v0.5.6
https://bun.com/blog/bun-v0.5.6
Support for `Bun.sleep`, improved Docker support, and improvements to Node.js and npm compatibility
Thu, 09 Feb 2023 01:19:03 GMT

Bun v0.5.5
https://bun.com/blog/bun-v0.5.5
https://bun.com/blog/bun-v0.5.5
Improved compatibility for `node:http`, support for `http.request()` and `stripe-node`, and fixed various bugs.
Thu, 02 Feb 2023 22:39:43 GMT

Bun v0.5.2
https://bun.com/blog/bun-v0.5.2
https://bun.com/blog/bun-v0.5.2
MongoDB support, `github:` dependencies in `bun install`, faster `Buffer`, `bun run` for WebAssembly, express' `body-parser` package, and many bug fixes.
Tue, 31 Jan 2023 03:43:44 GMT

Bun v0.5.1
https://bun.com/blog/bun-v0.5.1
https://bun.com/blog/bun-v0.5.1
Support for aliasing package.json dependencies, a better error message when a workspace is not found, and a few important bug fixes.
Thu, 19 Jan 2023 18:10:45 GMT

Bun v0.5
https://bun.com/blog/bun-v0.5.0
https://bun.com/blog/bun-v0.5.0
Support for npm workspaces, DNS lookups, database drivers, and lots of improvements to bun install.
Wed, 18 Jan 2023 18:10:45 GMT

Bun v0.4
https://bun.com/blog/bun-v0.4.0
https://bun.com/blog/bun-v0.4.0
Introducing bunx. Install and run an executable from npm, 100x faster than npx.
Fri, 23 Dec 2022 07:00:00 GMT

Bun v0.3.0
https://bun.com/blog/bun-v0.3.0
https://bun.com/blog/bun-v0.3.0
Massive reduction in memory usage, faster text encoding, improved Jest compatibility, file-system routing, automatic package installs, and a lot more
Wed, 07 Dec 2022 06:00:00 GMT

Bun v0.2.2
https://bun.com/blog/bun-v0.2.2
https://bun.com/blog/bun-v0.2.2
Release notes for Bun v0.2.2
Thu, 27 Oct 2022 08:14:11 GMT

Bun v0.2.1
https://bun.com/blog/bun-v0.2.1
https://bun.com/blog/bun-v0.2.1
Release notes for Bun v0.2.1
Wed, 19 Oct 2022 06:10:52 GMT

Bun v0.2.0
https://bun.com/blog/bun-v0.2.0
https://bun.com/blog/bun-v0.2.0
Release notes for Bun v0.2.0
Thu, 13 Oct 2022 23:48:34 GMT

Bun v0.1.12
https://bun.com/blog/bun-v0.1.12
https://bun.com/blog/bun-v0.1.12
Release notes for Bun v0.1.12
Sun, 18 Sep 2022 06:37:55 GMT

Bun v0.1.11
https://bun.com/blog/bun-v0.1.11
https://bun.com/blog/bun-v0.1.11
Release notes for Bun v0.1.11
Wed, 07 Sep 2022 19:56:07 GMT

Bun v0.1.10
https://bun.com/blog/bun-v0.1.10
https://bun.com/blog/bun-v0.1.10
Release notes for Bun v0.1.10
Fri, 19 Aug 2022 07:49:38 GMT

Bun v0.1.9
https://bun.com/blog/bun-v0.1.9
https://bun.com/blog/bun-v0.1.9
Release notes for Bun v0.1.9
Thu, 18 Aug 2022 08:49:36 GMT

Bun v0.1.8
https://bun.com/blog/bun-v0.1.8
https://bun.com/blog/bun-v0.1.8
Release notes for Bun v0.1.8
Thu, 11 Aug 2022 08:18:30 GMT

Bun v0.1.7
https://bun.com/blog/bun-v0.1.7
https://bun.com/blog/bun-v0.1.7
Release notes for Bun v0.1.7
Sat, 06 Aug 2022 08:15:30 GMT

Bun v0.1.6
https://bun.com/blog/bun-v0.1.6
https://bun.com/blog/bun-v0.1.6
Release notes for Bun v0.1.6
Mon, 01 Aug 2022 23:29:18 GMT

Bun v0.1.5
https://bun.com/blog/bun-v0.1.5
https://bun.com/blog/bun-v0.1.5
Release notes for Bun v0.1.5
Sat, 23 Jul 2022 02:11:34 GMT

Bun v0.1.4
https://bun.com/blog/bun-v0.1.4
https://bun.com/blog/bun-v0.1.4
Release notes for Bun v0.1.4
Wed, 13 Jul 2022 08:49:38 GMT

Bun v0.1.3
https://bun.com/blog/bun-v0.1.3
https://bun.com/blog/bun-v0.1.3
Release notes for Bun v0.1.3
Mon, 11 Jul 2022 19:38:25 GMT

Bun v0.1.2
https://bun.com/blog/bun-v0.1.2
https://bun.com/blog/bun-v0.1.2
Release notes for Bun v0.1.2
Thu, 07 Jul 2022 23:32:48 GMT

Bun v0.1.1
https://bun.com/blog/bun-v0.1.1
https://bun.com/blog/bun-v0.1.1
Release notes for Bun v0.1.1
Tue, 05 Jul 2022 20:35:35 GMT