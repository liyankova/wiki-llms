---
url: https://bun.com/blog/bun-v1.0.7
title: Bun v1.0.7 | Bun Blog
source_domain: bun.com
---

# Bun v1.0.7 | Bun Blog

# Bun v1.0.7

---

[Jarred Sumner](https://twitter.com/jarredsumner) · October 20, 2023

Bun v1.0.7 fixes 59 bugs (addressing 78 👍 reactions), implements optional peer dependencies in `bun install`, and makes improvements to Node.js compatibility.

Bun is an incredibly fast JavaScript runtime, bundler, transpiler, and package manager — all in one. In case you missed it, here are some of the recent changes to Bun:

* [`v1.0.0`](https://bun.com/blog/bun-v1.0) - First stable release!
* [`v1.0.1`](https://bun.com/blog/bun-v1.0.1) - Named imports for .json and .toml files, fixes to `bun install`, `node:path`, and `Buffer`
* [`v1.0.2`](https://bun.com/blog/bun-v1.0.2) - Make `--watch` faster and lots of bug fixes
* [`v1.0.3`](https://bun.com/blog/bun-v1.0.3) - `emitDecoratorMetadata` and Nest.js support, fixes for private registries and more
* [`v1.0.4`](https://bun.com/blog/bun-v1.0.4) - `server.requestIP`, virtual modules in runtime plugins, and more
* [`v1.0.5`](https://bun.com/blog/bun-v1.0.5) - Fixed memory leak with `fetch()`, `KeyObject` support in `node:crypto` module, `expect().toEqualIgnoringWhitespace` in `bun:test`, and more
* [`v1.0.6`](https://bun.com/blog/bun-v1.0.6) - Fixes 3 bugs (addressing 85 👍 reactions), implements `overrides` & `resolutions` in `package.json`, and fixes regression impacting Docker usage with Bun

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

## [`bun install` improvements](https://bun.com/blog/bun-v1.0.7#bun-install-improvements)

This release includes several bugfixes to `bun install`, such as:

### [New: Optional `peerDependencies`](https://bun.com/blog/bun-v1.0.7#new-optional-peerdependencies)

This release adds support for optional peer dependencies, which addresses a bug where `bun install` would potentially install more packages than `npm install`.

An optional peer dependency appears in a package.json looks like this:

package.json

```
{
  "peerDependencies": {
    "node-notifier": "^8.0.1 || ^9.0.0 || ^10.0.0"
  },
  "peerDependenciesMeta": {
    "node-notifier": {
      "optional": true
    }
  }
}
```

This tells the npm client to not install `node-notifier`, unless it is explicitly listed in the `dependencies` or `devDependencies` of the root project's `package.json`.

In the previous release, Bun would install `node-notifier` even if it wasn't listed in the root project's `package.json`. This would increase the size of node\_modules and potentially could cause issues where Bun would intall the same package under multiple versions. In Bun v1.0.7, this has been fixed.

Thanks to [@dylan-conway](https://github.com/dylan-conway) for implementing optional peer dependencies in Bun!

### [Fixed: Edgecase where wrong version of packages were installed](https://bun.com/blog/bun-v1.0.7#fixed-edgecase-where-wrong-version-of-packages-were-installed)

There was a bug where `bun install` would sometimes choose older versions of packages when matching the semver range. This has been fixed, thanks to [@dylang](https://github.com/dylang).

Specifically, we assumed the npm registry API returned the list of package versions in semver order. The official registry API *usually* does, but not always. Moreover, not everyone uses the official registry API. This caused `bun install` to sometimes choose older versions of packages that still matched the semver range.

Bun will now sort the versions retreived from the registry, before choosing the best version that matches.

### [Fixed: `bun install github:foo/foo` could save multiple times to package.json](https://bun.com/blog/bun-v1.0.7#fixed-bun-install-github-foo-foo-could-save-multiple-times-to-package-json)

A bug caused `bun install github:foo/foo` to save multiple times to package.json. If you ran it twice, the dependency would appear multiple times in package.json. This bug has been fixed, thanks to [@dylan-conway](https://github.com/dylan-conway).

### [Fixed: Edgecase causing non-deterministic `bun.lockb` on Linux](https://bun.com/blog/bun-v1.0.7#fixed-edgecase-causing-non-deterministic-bun-lockb-on-linux)

A determinism issue caused `bun.lockb` to sometimes have differing contents on Linux. This has been fixed, thanks to [@dylan-conway](https://github.com/dylan-conway).

### [Fixed: npm alias edgecase bugfix](https://bun.com/blog/bun-v1.0.7#fixed-npm-alias-edgecase-bugfix)

A bug causing `npm:` aliases in dependencies to not always be respected has been fixed, thanks to [@dylan-conway](https://github.com/dylan-conway).

## [Node.js compatibility improvements](https://bun.com/blog/bun-v1.0.7#node-js-compatibility-improvements)

This release also includes several Node.js compatibility improvements.

### [Fixed: `child_process` IPC reliability](https://bun.com/blog/bun-v1.0.7#fixed-child-process-ipc-reliability)

A reliability issue causing IPC messages to not send all their contents has been fixed, thanks to [@paperclover](https://github.com/paperclover). This helps Next.js work more reliably in Bun, though there is still have more work to be done there.

### [Fixed: Hanging socket without `end` event](https://bun.com/blog/bun-v1.0.7#fixed-hanging-socket-without-end-event)

A bug causing `node:net` sockets to not correctly emit an `end` event in all cases has been fixed, thanks to [@cirospaciari](https://github.com/cirospaciari).

This bug impacted the `pg` and `sequelize` packages, among others.

### [Fixed: `napi` memory leak](https://bun.com/blog/bun-v1.0.7#fixed-napi-memory-leak)

A memory leak in napi has been fixed, thanks to [@alangecker](https://github.com/alangecker). The root cause was a reference count that started at `1` instead of `0`.

### [Fixed: `node:stream` crash](https://bun.com/blog/bun-v1.0.7#fixed-node-stream-crash)

A crash that could potentially occur when writing many small chunks to a `node:stream` has been fixed, thanks to [@paperclover](https://github.com/paperclover).

### [Fixed: `server.address()` for Unix sockets](https://bun.com/blog/bun-v1.0.7#fixed-server-address-for-unix-sockets)

A bug causing `server.address()` in `node:http` to return incorrect values for unix sockets has been fixed, thanks to [@Hanaasagi](https://github.com/Hanaasagi).

### [Fixed: `threadId` was unset in `Worker`](https://bun.com/blog/bun-v1.0.7#fixed-threadid-was-unset-in-worker)

A bug causing `threadId` to not be set in the `Worker` instance returned in `node:worker_threads` has been fixed, thanks to [@jerome-benoit](https://github.com/jerome-benoit).

### [Fixed: `Buffer.write` with 'binary' truncated to ascii instead of latin1](https://bun.com/blog/bun-v1.0.7#fixed-buffer-write-with-binary-truncated-to-ascii-instead-of-latin1)

A bug causing `Buffer.write` with `'binary'` encoding to truncate to ascii rather than latin1 has been fixed, thanks to [@Electroid](https://github.com/Electroid).

### [Fixed: `Buffer.concat(buffers, undefined)` threw an error](https://bun.com/blog/bun-v1.0.7#fixed-buffer-concat-buffers-undefined-threw-an-error)

A bug where the following code would throw an error has been fixed, thanks to [@Hanaasagi](https://github.com/Hanaasagi).

```
Buffer.concat([Buffer(1), Buffer(1)], undefined);
```

The following code would not throw an error:

```
Buffer.concat([Buffer(1), Buffer(1)]);
Buffer.concat([Buffer(1), Buffer(1)], 2);
```

The bug was checking for the native code equivalent of `arguments.length` instead of whether or not `arguments[1]` was `undefined`.

### [Fixed: `node:dns` lookup returned wrong address for family](https://bun.com/blog/bun-v1.0.7#fixed-node-dns-lookup-returned-wrong-address-for-family)

A bug causing `node:dns`'s `lookup` function to return the wrong address type when `family` was set has been fixed, thanks to [@Electroid](https://github.com/Electroid). For example, `dns.lookup('localhost', { family: 6 })` could have returned an IPv4 address instead of an IPv6 address.

## [Runtime fixes](https://bun.com/blog/bun-v1.0.7#runtime-fixes)

We also fixed several bugs in the Bun runtime.

### [Fixed: Bug causing docker container to throw incorrect "port in use" errors](https://bun.com/blog/bun-v1.0.7#fixed-bug-causing-docker-container-to-throw-incorrect-port-in-use-errors)

A bug causing Bun to throw incorrect "port in use" errors when running in a Docker container has been fixed, thanks to [@Hanaasagi](https://github.com/Hanaasagi).

When binding to IPv6 address failed, Bun would immediately return an error. Now, it also attempts to bind to IPv4 addresses and only returns an error if that also fails. This is because of a [long-standing issue](https://github.com/moby/moby/issues/35954) where Docker would contain IPv6 entries in `/etc/hosts`, even when IPv6 was disabled.

### [Fixed: `request.url` would sometimes have incorrect port](https://bun.com/blog/bun-v1.0.7#fixed-request-url-would-sometimes-have-incorrect-port)

An edgecase causing `request.url` to sometimes have an incorrect port has been fixed, thanks to [@Electroid](https://github.com/Electroid).

### [Fixed: Missing `statusText` in `Response`](https://bun.com/blog/bun-v1.0.7#fixed-missing-statustext-in-response)

A bug causing `response.statusText` to be missing has been fixed, thanks to [@toshok](https://github.com/toshok).

### [Fixed: WebSocket client Host header missing port](https://bun.com/blog/bun-v1.0.7#fixed-websocket-client-host-header-missing-port)

A bug where the port number was not included in the `Host` header sent by the WebSocket client has been fixed, thanks to [@Electroid](https://github.com/Electroid).

### [Fixed: `Bun.write` reported wrong path in error message](https://bun.com/blog/bun-v1.0.7#fixed-bun-write-reported-wrong-path-in-error-message)

A bug causing `Bun.write` to report the wrong path in error messages has been fixed, thanks to [@Hanaasagi](https://github.com/Hanaasagi).

### [Fixed: `statement.all()` in SQLite sometimes returned a number instead of an array](https://bun.com/blog/bun-v1.0.7#fixed-statement-all-in-sqlite-sometimes-returned-a-number-instead-of-an-array)

In certain cases `bun:sqlite`'s `statement.all()` function returned a number instead of an array. This was very confusing and has been fixed to always return an array, thanks to [@HForGames](https://github.com/HForGames).

### [Fixed: `describe.only` didn't work for nested describe scopes](https://bun.com/blog/bun-v1.0.7#fixed-describe-only-didn-t-work-for-nested-describe-scopes)

A bug in `bun:test` causing `describe.only` to not work for nested describe scopes has been fixed, thanks to [@igorshapiro](https://github.com/igorshapiro).

## [Preperation for regular Windows builds](https://bun.com/blog/bun-v1.0.7#preperation-for-regular-windows-builds)

We are making changes to our build system in preparation for regular Windows builds.

Bun will soon switch to use `cmake` and `ninja` for builds, rather than a 2000+ line `Makefile`. Bun will also start using the debug builds of JavaScriptCore, which enables various assertions that help us catch bugs earlier. This release implements most of the changes necessary for that, thanks to [@paperclover](https://github.com/paperclover).

Bun will also upgrade from LLVM 16 to LLVM 17 in the next release.

## [New Contributors](https://bun.com/blog/bun-v1.0.7#new-contributors)

Thanks to our 17 new contributors 🎉

* [`@clay-curry`](https://github.com/clay-curry) made their first contribution in [`#6479`](https://github.com/oven-sh/bun/pull/6479)
* [`@jerome-benoit`](https://github.com/jerome-benoit) made their first contribution in [`#6521`](https://github.com/oven-sh/bun/pull/6521)
* [`@Voldemat`](https://github.com/Voldemat) made their first contribution in [`#6128`](https://github.com/oven-sh/bun/pull/6128)
* [`@toshok`](https://github.com/toshok) made their first contribution in [`#6151`](https://github.com/oven-sh/bun/pull/6151)
* [`@HForGames`](https://github.com/HForGames) made their first contribution in [`#5946`](https://github.com/oven-sh/bun/pull/5946)
* [`@yschroe`](https://github.com/yschroe) made their first contribution in [`#5485`](https://github.com/oven-sh/bun/pull/5485)
* [`@Connormiha`](https://github.com/Connormiha) made their first contribution in [`#4975`](https://github.com/oven-sh/bun/pull/4975)
* [`@aralroca`](https://github.com/aralroca) made their first contribution in [`#6558`](https://github.com/oven-sh/bun/pull/6558)
* [`@pierre-cm`](https://github.com/pierre-cm) made their first contribution in [`#6563`](https://github.com/oven-sh/bun/pull/6563)
* [`@klatka`](https://github.com/klatka) made their first contribution in [`#6153`](https://github.com/oven-sh/bun/pull/6153)
* [`@mountainash`](https://github.com/mountainash) made their first contribution in [`#6579`](https://github.com/oven-sh/bun/pull/6579)
* [`@owlcode`](https://github.com/owlcode) made their first contribution in [`#6587`](https://github.com/oven-sh/bun/pull/6587)
* [`@nygmaaa`](https://github.com/nygmaaa) made their first contribution in [`#6581`](https://github.com/oven-sh/bun/pull/6581)
* [`@vladaman`](https://github.com/vladaman) made their first contribution in [`#6208`](https://github.com/oven-sh/bun/pull/6208)
* [`@PaulaBurgheleaGithub`](https://github.com/PaulaBurgheleaGithub) made their first contribution in [`#6620`](https://github.com/oven-sh/bun/pull/6620)
* [`@alangecker`](https://github.com/alangecker) made their first contribution in [`#6598`](https://github.com/oven-sh/bun/pull/6598)
* [`@imcatwhocode`](https://github.com/imcatwhocode) made their first contribution in [`#6590`](https://github.com/oven-sh/bun/pull/6590)

---

[#### Bun v1.0.6](https://bun.com/blog/bun-v1.0.6)[#### Bun v1.0.8](https://bun.com/blog/bun-v1.0.8)