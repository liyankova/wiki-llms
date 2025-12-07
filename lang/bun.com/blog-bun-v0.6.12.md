---
url: https://bun.com/blog/bun-v0.6.12
title: Bun v0.6.12 | Bun Blog
source_domain: bun.com
---

# Bun v0.6.12 | Bun Blog

# Bun v0.6.12

---

[Jarred Sumner](https://twitter.com/jarredsumner) · June 30, 2023

We're hiring C/C++ and Zig engineers to build the future of JavaScript! [Join our team →](https://bun.com/careers)

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
* `v0.6.11` - address a release build issue from `v0.6.10`

This release makes it easier to read runtime errors, improves Node.js compatiblity, adds `await Bun.file(path).exists()`, fixes bundler bugs and slightly reduces minifier output size.

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

## [Better runtime errors](https://bun.com/blog/bun-v0.6.12#better-runtime-errors)

We've made several improvements to runtime errors in Bun:

* Patched JavaScriptCore to allow Bun to print `Error.prototype.stack` in the same style as V8.
* Stack traces show fewer internal builtin functions
* `console.error(error)` now includes indirect function names, such as `let foo = function() {}` will now show `foo` instead of `anonymous`
* `Error.captureStackTrace(err)`'s `err.stack` property is no longer marked as read-only (this was incorrect)
* `Error.prototype.stack` is now automatically sourcemapped.

Bun transpiles every file in the runtime. Before this release, `error.stack` would show the stack for the transpiled source, which was not very useful. Now, `error.stack` shows the stack for the original source, following an internal sourcemap generated for each file.

The output of `console.log(error.stack)` after:

```
Error: hello!
    at hey (error.js:1:29)
    at module code (error.js:4:16)
```

The output of `console.log(error.stack)` before:

```
hey@error.js:1:29
module code@error.js:4:16
evaluate@[native code]
moduleEvaluation@[native code]
moduleEvaluation@[native code]
@[native code]
asyncFunctionResume@[native code]
promiseReactionJobWithoutPromise@[native code]
promiseReactionJob@[native code]
```

Input:

```
function hey() {
  return new Error("hello!").stack;
}
console.log(hey());
```

> In the next version of Bun   
>   
> error.stack is formatted like in node/V8 and automatically sourcemapped. [pic.twitter.com/BQ3uSVTloy](https://t.co/BQ3uSVTloy)
>
> — Jarred Sumner (@jarredsumner) [June 28, 2023](https://twitter.com/jarredsumner/status/1673957121472491520?ref_src=twsrc%5Etfw)

## [Improvements to CommonJS <> ES Module interop](https://bun.com/blog/bun-v0.6.12#improvements-to-commonjs-es-module-interop)

When using `require` to load an ES Module at runtime, Bun now inserts the `__esModule` annotation which many npm packages transpiled with Babel need in order to work correctly. This fixed a bug with using `@mui/styled-engine` with `bun test`.

### [package.json `"module"` field is no longer used in Bun's runtime](https://bun.com/blog/bun-v0.6.12#package-json-module-field-is-no-longer-used-in-bun-s-runtime)

Bundlers use the `"module"` field in `package.json` with a higher priority over the `"main"` field when bundling ES Modules, but Node.js does not use the `"module"` field at all.

Previously, Bun used the `"module"` at runtime (when package.json `"exports"` wasn't in use) similar to how bundlers use it, but this caused some packages to load the browser version of their code in Bun and Node.js versions in Node.

Bun's bundler continues to support the `"module"` field when building for browsers, but to improve Node.js compatibility, Bun's runtime no longer uses the `"module"` field.

## [SQLite3 Full-text search is enabled](https://bun.com/blog/bun-v0.6.12#sqlite3-full-text-search-is-enabled)

> In the next version of Bun  
>   
> You can use full text search with sqlite (via fts5), thanks to [@ItsRedraskal](https://twitter.com/ItsRedraskal?ref_src=twsrc%5Etfw) [pic.twitter.com/NCP8BezEmQ](https://t.co/NCP8BezEmQ)
>
> — Jarred Sumner (@jarredsumner) [June 28, 2023](https://twitter.com/jarredsumner/status/1673856130853011456?ref_src=twsrc%5Etfw)

## [Bun.file(path).exists()](https://bun.com/blog/bun-v0.6.12#bun-file-path-exists)

`Bun.file(path).exists()` is a new method that returns a boolean indicating whether a file exists at the given path.

```
import { file, write } from "bun";

console.log(await file("hello.txt").exists()); // false
await write("hello.txt", "hello world");
console.log(await file("hello.txt").exists()); // true
```

## [Node.js compatibility improvements](https://bun.com/blog/bun-v0.6.12#node-js-compatibility-improvements)

Several bugfixes to node:http and node:stream have landed

### [Google Maps works](https://bun.com/blog/bun-v0.6.12#google-maps-works)

The `@googlemaps/google-maps-services-js` package now works in Bun, thanks to [@dylan-conway](https://github.com/dylan-conway) fixing a bug in our `node:http` implmenetation where properties were marked as read only that shouldn't have been marked as read-only.

```
import { Client } from "@googlemaps/google-maps-services-js";

const client = new Client({});

client
  .elevation({
    params: {
      locations: [{ lat: 45, lng: -110 }],
      key: "asdf",
    },
    timeout: 1000, // milliseconds
  })
  .then((r) => {
    console.log(r.data.results[0].elevation);
  })
  .catch((e) => {
    console.log(e.response.data.error_message);
  });
```

### [ytdl-core now works](https://bun.com/blog/bun-v0.6.12#ytdl-core-now-works)

The `ytdl-core` package now works in Bun, thanks to [@paperclover](https://github.com/paperclover) fixing a couple bugs in our `node:http` and `node:stream` implementations:

```
import { createWriteStream } from "fs";
import ytdl from "ytdl-core";

ytdl("https://www.youtube.com/watch?v=dQw4w9WgXcQ").pipe(
  createWriteStream("secret-video-do-not-download.mp4"),
);
```

### [Minifier improvements](https://bun.com/blog/bun-v0.6.12#minifier-improvements)

Bun's minifier now minifies `obj["a"]` into `obj.a` and `obj["a"] = 1` into `obj.a = 1`.

Build:

```
bun build --minify ./input.js`
```

Input:

```
const obj = {};
obj["a"] = 1;
```

After:

```
const obj = {};
obj.a = 1;
```

Before:

```
const obj = {};
obj["a"] = 1;
```

This yields a 0.02% reduction in bundle size for `vue` and potentially a little faster at runtime (engines implement computed property accesses differently than regular property accesses).

### [Bundler bugfixes](https://bun.com/blog/bun-v0.6.12#bundler-bugfixes)

A bug where two consecutive files that re-export another file using CommonJS `module.exports = require()` would produce invalid code has been fixed

```
// a.js
module.exports = require("./b");
```

```
// b.js
module.exports = require("./c");
```

```
// c.js
module.exports = {};
```

* In certain cases, Bun's CommonJS -> ES Module transform in the bundler would inject `exports.foo = undefined` and that caused some packages which used Object prototype methods to throw an error and it bloated the code. This has been fixed.

### [More bugfixes](https://bun.com/blog/bun-v0.6.12#more-bugfixes)

* A regression breaking macros has been fixed
* The `resolve6` export in dns/promises was missing
* The `errorMonitor` export in `node:events` was missing

## [Changelog](https://bun.com/blog/bun-v0.6.12#changelog)

[See the changelog on GitHub](https://github.com/oven-sh/bun/compare/bun-v0.6.11...bun-v0.6.12)

---

[#### Bun v0.6.10](https://bun.com/blog/bun-v0.6.10)[#### Bun v0.6.13](https://bun.com/blog/bun-v0.6.13)