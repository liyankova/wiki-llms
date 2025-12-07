---
url: https://bun.com/blog/bun-v1.0.21
title: Bun v1.0.21 | Bun Blog
source_domain: bun.com
---

# Bun v1.0.21 | Bun Blog

# Bun v1.0.21

---

[Jarred Sumner](https://twitter.com/jarredsumner) · January 2, 2024

Bun v1.0.21 fixes 33 bugs (addressing 80 👍 reactions). `console.table()` support. `Bun.write`, Bun.file, and bun:sqlite use less memory. Large file uploads with FormData use less memory. bun:sqlite error messages get more detailed. Memory leak in errors from node:fs fixed. Node.js compatibility improvements, and many crashes fixed

Bun is an incredibly fast JavaScript runtime, bundler, transpiler, and package manager — all in one. In case you missed it, here are some of the recent changes to Bun:

* [`v1.0.18`](https://bun.com/blog/bun-v1.0.18) - Fixes 27 bugs (addressing 28 👍 reactions). A hang impacting create-vite & create-next & stdin has been fixed. Lifecycle scripts reporting "node" or "node-gyp" not found has been fixed. expect().rejects works like Jest now, and more bug fixes
* [`v1.0.19`](https://bun.com/blog/bun-v1.0.19) - Fixes 26 bugs (addressing 92 👍 reactions). Use @types/bun instead of bun-types. Fixes --frozen-lockfile bug. bcrypt & argon2 packages now work. setTimeout & setInterval get 4x higher throughput. module mocks in bun:test resolve specifiers. Optimized spawnSync() for large stdio on Linux. Bun.peek() gets 90x faster, expect(map1).toEqual(map2) gets 100x faster. Bugfixes to NAPI, bun install, and Node.js compatibility improvements
* [`v1.0.20`](https://bun.com/blog/bun-v1.0.20) - Reduces memory usage in `fs.readlink`, `fs.readFile`, `fs.writeFile`, `fs.stat` and `HTMLRewriter`. Fixes a regression where setTimeout caused high CPU usage on Linux. `HTMLRewriter.transform` now supports strings and `ArrayBuffer`. `fs.writeFile()` and `fs.readFile()` now support `hex` & `base64` encodings. `Bun.spawn` shows how much CPU & memory the process used.

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

## [console.table() is now supported](https://bun.com/blog/bun-v1.0.21#console-table-is-now-supported)

[`console.table()`](https://developer.mozilla.org/en-US/docs/Web/API/console/table_static) is a Web API that prints a table from an object or iterable. It's useful for debugging.

fetch.js

```
const { headers } = await fetch("https://example.com");
console.table(headers)
```

In this example, Bun will print an ASCII table of the response headers.

```
┌────┬──────────────────┬───────────────────────────────┐
│    │ 0                │ 1                             │
├────┼──────────────────┼───────────────────────────────┤
│  0 │ age              │ 519517                        │
│  1 │ cache-control    │ max-age=604800                │
│  2 │ content-encoding │ gzip                          │
│  3 │ content-length   │ 648                           │
│  4 │ content-type     │ text/html; charset=UTF-8      │
│  5 │ date             │ Tue, 02 Jan 2024 02:37:00 GMT │
│  6 │ etag             │ "3147526947+gzip"             │
│  7 │ expires          │ Tue, 09 Jan 2024 02:37:00 GMT │
│  8 │ last-modified    │ Thu, 17 Oct 2019 07:18:26 GMT │
│  9 │ server           │ ECS (sac/2508)                │
│ 10 │ vary             │ Accept-Encoding               │
│ 11 │ x-cache          │ HIT                           │
└────┴──────────────────┴───────────────────────────────┘
```

Thanks to [@otgerrogla](https://github.com/otgerrogla) for implementing this feature!

You can also use `console.table` with a variety of different objects, including:

#### Arrays with console.table()

issues.js

```
const foo = await fetch("https://api.github.com/repos/elyisajs/elysia/issues");
console.table(await issues.json(), ["title", "status"]);
```

[![Screenshot of console.table output](https://github.com/oven-sh/bun/assets/709451/c6e5d822-dc2f-4676-aca7-d724fee0d0a7)](https://github.com/oven-sh/bun/assets/709451/c6e5d822-dc2f-4676-aca7-d724fee0d0a7)

#### Objects with console.table()

user.js

```
const user = await fetch("https://api.github.com/users/ThePrimeagen");
console.table(await user.json());
```

This prints something like:

```
┌─────────────────────┬──────────────────────────────────────────────────────────────────┐
│                     │ Values                                                           │
├─────────────────────┼──────────────────────────────────────────────────────────────────┤
│               login │ ThePrimeagen                                                     │
│                  id │ 4458174                                                          │
│             node_id │ MDQ6VXNlcjQ0NTgxNzQ=                                             │
│          avatar_url │ https://avatars.githubusercontent.com/u/4458174?v=4              │
│         gravatar_id │                                                                  │
│                 url │ https://api.github.com/users/ThePrimeagen                        │
│            html_url │ https://github.com/ThePrimeagen                                  │
│       followers_url │ https://api.github.com/users/ThePrimeagen/followers              │
│       following_url │ https://api.github.com/users/ThePrimeagen/following{/other_user} │
│           gists_url │ https://api.github.com/users/ThePrimeagen/gists{/gist_id}        │
│         starred_url │ https://api.github.com/users/ThePrimeagen/starred{/owner}{/repo} │
│   subscriptions_url │ https://api.github.com/users/ThePrimeagen/subscriptions          │
│   organizations_url │ https://api.github.com/users/ThePrimeagen/orgs                   │
│           repos_url │ https://api.github.com/users/ThePrimeagen/repos                  │
│          events_url │ https://api.github.com/users/ThePrimeagen/events{/privacy}       │
│ received_events_url │ https://api.github.com/users/ThePrimeagen/received_events        │
│                type │ User                                                             │
│          site_admin │ false                                                            │
│                name │ ThePrimeagen                                                     │
│             company │ CEO Of TheStartup                                                │
│                blog │ http://twitch.tv/ThePrimeagen                                    │
│            location │ 9th Ring, Vim                                                    │
│               email │ null                                                             │
│            hireable │ null                                                             │
│                 bio │ null                                                             │
│    twitter_username │ ThePrimeagen                                                     │
│        public_repos │ 199                                                              │
│        public_gists │ 0                                                                │
│           followers │ 23186                                                            │
│           following │ 3                                                                │
│          created_at │ 2013-05-17T15:05:59Z                                             │
│          updated_at │ 2023-11-22T19:47:49Z                                             │
└─────────────────────┴──────────────────────────────────────────────────────────────────┘
```

## [bun:sqlite has more detailed error messages](https://bun.com/blog/bun-v1.0.21#bun-sqlite-has-more-detailed-error-messages)

Previously, `bun:sqlite` might throw an error like:

```
7 | db.exec('INSERT INTO foo VALUES ("hello")');
    ^
error: constraint failed
      at run (bun:sqlite:185:11)
      at /private/tmp/sqlite.js:7:1
```

But now, you'll get a more detailed error like:

```
7 | db.exec('INSERT INTO foo VALUES ("hello")');
    ^
SQLiteError: UNIQUE constraint failed: foo.bar
 errno: 2067
  code: "SQLITE_CONSTRAINT_UNIQUE"

      at run (bun:sqlite:185:11)
      at /private/tmp/fetch.js:7:1
```

#### What changed?

* `error.name` is now `SQLiteError` instead of `Error`
* `error.message` now uses the extended error message from SQLite which frequently includes the table and column name
* `error.errno` is the extended error code from SQLite
* `error.code` is the extended error code from SQLite as a string
* `error.byteOffset` reports the byte offset in the SQL statement where the error occurred, if available

```
+ SQLiteError: UNIQUE constraint failed: foo.bar
- error: constraint failed
+  errno: 2067
+   code: "SQLITE_CONSTRAINT_UNIQUE"
      at run (bun:sqlite:185:11)
      at /private/tmp/sqlite.js:7:1
```

### [bun:sqlite uses less memory](https://bun.com/blog/bun-v1.0.21#bun-sqlite-uses-less-memory)

`bun:sqlite` now reports SQLite's memory usage to the garbage collector, which prompts the garbage collector to free memory more aggressively when necessary.

This example, which creates 100,000 prepared statements, consumes 4x less memory:

| Memory usage | Bun version |
| --- | --- |
| 71 MB | Bun v1.0.21 |
| 287 MB | Bun v1.0.20 |

```
import { Database } from "bun:sqlite";

const db = new Database(":memory:");

db.exec("CREATE TABLE test (id INTEGER PRIMARY KEY, content TEXT)");
db.exec('INSERT INTO test VALUES (NULL, "hello")');

for (let i = 0; i < 100_000; i++) {
  db.prepare(`SELECT content as content${i} FROM test`);
}

console.log((process.memoryUsage.rss() / 1024 / 1024) | 0, "MB");
```

We've also fixed a bug in the bindings implementation that caused the internal `SQLStatement` object to not call the destructor for the prepared statement when it was garbage collected.

### [Fixed: Crash in bun:sqlite with latin1 characters](https://bun.com/blog/bun-v1.0.21#fixed-crash-in-bun-sqlite-with-latin1-characters)

There was a crash in `bun:sqlite` when using latin1 supplemental characters in a query, which has now been fixed.

```
const db = new Database(":memory:");

db.run(
  "CREATE TABLE foo (id INTEGER PRIMARY KEY AUTOINCREMENT, copyright© TEXT)",
);
```

The `©` symbol is a valid latin1 supplemental character, and previously the code for sending the query to SQLite incorrectly assumed that latin1 strings were always ASCII strings.

## [Copy-on-write file uploads on Linux](https://bun.com/blog/bun-v1.0.21#copy-on-write-file-uploads-on-linux)

When you upload a large file with [`FormData`](https://developer.mozilla.org/en-US/docs/Web/API/FormData), each file becomes a `Blob` object (or `File` object) in memory.

What happens if you need to get the data as an `ArrayBuffer`?

```
const blob = formData.get("image");

// This clones the data, doubling the memory usage!
const bytes = await blob.arrayBuffer();
```

It clones. Suddenly, **if you uploaded a 128 MB file, you're now using 256 MB of memory** just to get the data as an `ArrayBuffer`.

One could argue that this is an API design issue. Should `.arrayBuffer()` *really* clone the data? But that's the standard Web API, it's what we have to work with.

**Can we do better, without changing the API?** Yes!

It's called copy-on-write memory.

[![](https://github.com/oven-sh/bun/assets/709451/d23be814-7b03-4f58-9e7f-6567adf0e8c5)](https://github.com/oven-sh/bun/assets/709451/d23be814-7b03-4f58-9e7f-6567adf0e8c5)

Through some virtual-memory trickery, we can make it so that when you call [`blob.arrayBuffer()`](https://developer.mozilla.org/en-US/docs/Web/API/Blob/arrayBuffer), it doesn't actually clone the data. Instead, it creates a new virtual memory mapping that points to the same data, and only clones the data (in chunks of 4 KB) when you write to it.

This release implements support for copy-on-write `blob.arrayBuffer()` when `blob` is at least 8 MB (1 MB when `--smol` is enabled).

| Memory usage after 100 copies | Bun version |
| --- | --- |
| 192 MB | Bun v1.0.21 |
| 12.9 GB | Bun v1.0.20 |

blob-arrayBuffer.js

```
const blob = new Blob([new Uint8Array(1024 * 1024 * 128).fill(42)]);

const arrayBuffers = await Array.fromAsync({ length: 100 }, () =>
  blob.arrayBuffer(),
);

console.log("RSS", (process.memoryUsage.rss() / 1024 / 1024) | 0, "MB");
```

If you make 100 copies of a 128 MB blob, it will only use 192 MB of memory. Before, it would use 12,993 MB MB of memory.

There is overhead to this, of course. Creating a unique memory mapping for each blob is expensive. Bun only does this for blobs larger than 8 MB (or 1 MB when `--smol` is enabled since `--smol` optimizes memory usage over execution time).

## [Hash file uploads from `FormData` with `Bun.CryptoHasher`](https://bun.com/blog/bun-v1.0.21#hash-file-uploads-from-formdata-with-bun-cryptohasher)

[`Bun.CryptoHasher`](https://bun.sh/docs/api/hashing#bun-cryptohasher) now supports [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob) objects, which simplifies hashing file uploads from [`FormData`](https://developer.mozilla.org/en-US/docs/Web/API/FormData).

```
import { serve, CryptoHasher } from "bun";

serve({
  async fetch(req) {
    const formData = await req.formData();

    const image = formData.get("file");
    const sha1 = CryptoHasher.hash("sha1", image, "hex");

    return new Response(`SHA-1: ${sha1}`);
  },
});
```

Previously, you'd have to convert the `Blob` to an `ArrayBuffer` before hashing it.

```
import { serve, CryptoHasher } from "bun";

serve({
  async fetch(req) {
    const formData = await req.formData();

     const image = formData.get("file");
     const image = await formData.get("file").arrayBuffer();

    const sha1 = CryptoHasher.hash("sha1", image, "hex");

    return new Response(`SHA-1: ${sha1}`);
  },
});
```

Note that we haven't added support for Bun.file() to `Bun.CryptoHasher` yet. It's tricky because `Bun.file()` is asynchronous and `Bun.CryptoHasher` is synchronous. We'll investigate adding support for that in a future release.

## [`expect(...).toBeObject` is a new matcher in bun:test](https://bun.com/blog/bun-v1.0.21#expect-tobeobject-is-a-new-matcher-in-bun-test)

The `toBeObject` matcher is now available in `bun:test`.

```
import { test, expect } from "bun:test";

test("object is an object", () => {
  expect({}).toBeObject();
});

test("number is not an object", () => {
  expect(1).not.toBeObject();
});
```

Thanks to [@coratgerl](https://github.com/coratgerl) for adding this matcher!

## [Fixed: Memory leak in Bun.file()](https://bun.com/blog/bun-v1.0.21#fixed-memory-leak-in-bun-file)

Previously, the following code would leak memory:

```
import { file } from "bun";

for (let i = 0; i < 100_000; i++) {
  file("/tmp/" + i + "/foo.txt");
}
```

The file path string was being duplicated without being freed. This is now fixed.

## [Fixed: Memory leak in Bun.write()](https://bun.com/blog/bun-v1.0.21#fixed-memory-leak-in-bun-write)

Similar to the above, `Bun.write` would leak memory when called repeatedly.

```
import { write } from "bun";

for (let i = 0; i < 100_000; i++) {
  await write("/tmp/" + i + "/foo.txt", "Hello!");
}
```

Again, the file path string was being duplicated without being freed. This is now fixed.

## [Fixed: Memory leak in errors from node:fs](https://bun.com/blog/bun-v1.0.21#fixed-memory-leak-in-errors-from-node-fs)

When you call `fs.readdir(path, { throwIfNoEntries: true })` and the directory doesn't exist, that error message would leak memory.

This has been fixed.

This leak wasn't specific to `readdirSync`, this occurred for nearly all errors from `node:fs` which contained a file path string or a message that was dynamically generated. This includes `fs.readFile`, `fs.writeFile`, `fs.stat`, `fs.readlink`, and more.

> in the next version of Bun  
>   
> a memory leak in errors from node:fs & Bun.write has been fixed [pic.twitter.com/FuY34GLlB9](https://t.co/FuY34GLlB9)
>
> — Jarred Sumner (@jarredsumner) [December 28, 2023](https://twitter.com/jarredsumner/status/1740290481530253468?ref_src=twsrc%5Etfw)

## [Fixed: `bun build` now supports `--public-path`](https://bun.com/blog/bun-v1.0.21#fixed-bun-build-now-supports-public-path)

`bun build` now supports the `--public-path` flag, which allows you to specify the public path for your assets to be served from.

```
bun build ./entry.ts --public-path=/assets/ --outdir=dist
```

This is useful if you're serving your assets from a CDN and want to make sure assets use absolute URLs.

This feature was already implemented in `Bun.build`, using the JavaScript API but was mistakenly omitted from the CLI.

## [Fixed: Crash in fetch() after redirect in certain cases](https://bun.com/blog/bun-v1.0.21#fixed-crash-in-fetch-after-redirect-in-certain-cases)

A crash that sometimes occurred when making multiple `fetch()` calls in quick succession with some that redirect has been fixed, thanks to [@cirospaciari](https://github.com/cirospaciari).

## [Fixed: Crash in WebSocket client when the server responds with a non-101 status code](https://bun.com/blog/bun-v1.0.21#fixed-crash-in-websocket-client-when-the-server-responds-with-a-non-101-status-code)

A bug in the `WebSocket` client that potentially caused a crash when the server responds with unexpected HTTP response headers has been fixed. This bug happened more frequently on macOS than Linux.

## [Fixed: Crash in WebSocket client when TLS handshake fails](https://bun.com/blog/bun-v1.0.21#fixed-crash-in-websocket-client-when-tls-handshake-fails)

A bug in the `WebSocket` client that potentially caused a crash when the server responded with an invalid TLS certificate. This bug happened more frequently on macOS than Linux.

## [Fixed: Crash in Bun.listen & Bun.connect when TLS handshake fails](https://bun.com/blog/bun-v1.0.21#fixed-crash-in-bun-listen-bun-connect-when-tls-handshake-fails)

Similar to the above, a bug in `Bun.listen` and `Bun.connect` that potentially caused a crash when the server responded with an invalid TLS certificate has been fixed.

## [Fixed: Possible crash in `bun test` with invalid surrogate pairs in error messages](https://bun.com/blog/bun-v1.0.21#fixed-possible-crash-in-bun-test-with-invalid-surrogate-pairs-in-error-messages)

When an error message contained invalid surrogate pairs (or otherwise, invalid UTF-8) in `bun test`, it could cause a crash due to an assertion failure when converting the error message to UTF-8 before it reaches the terminal. This has been fixed.

## [Fixed: Extraneous terminating chunk in `Bun.serve`](https://bun.com/blog/bun-v1.0.21#fixed-extraneous-terminating-chunk-in-bun-serve)

A bug in `Bun.serve` that could cause an extra terminating empty chunk to be sent when streaming has been fixed, thanks to [@cirospaciari](https://github.com/cirospaciari).

## [Fixed: `"call"` property missing in console.log() output](https://bun.com/blog/bun-v1.0.21#fixed-call-property-missing-in-console-log-output)

A bug in `console.log()` that caused the `"call"` property to be missing in the output has been fixed.

```
console.log({ call: "where did i go??", a: 1 });
```

Before:

```
{
  a: 1,
}
```

After:

```
{
  call: "where did i go??",
  a: 1,
}
```

## [Fixed: `expect(error).toStrictEqual()` compares only message & name](https://bun.com/blog/bun-v1.0.21#fixed-expect-error-tostrictequal-compares-only-message-name)

The `expect(error).toStrictEqual()` matcher now compares the `message` and `name` properties of the error, instead of all properties.

```
import { test, expect } from "bun:test";

test("errors match up", () => {
  const err = new Error("foo");
  err.stack;
  expect(err).toStrictEqual(new Error("foo"));
});
```

This test now passes, which aligns the behavior with Jest and node's `assert` module. Thanks to [@Kkaioduarte](https://github.com/Kkaioduarte) for fixing this bug!

### [Fixed: "duplicate dependencies" in `bun install` is now a warning instead of an error](https://bun.com/blog/bun-v1.0.21#fixed-duplicate-dependencies-in-bun-install-is-now-a-warning-instead-of-an-error)

When you run `bun install` and there are duplicate dependencies defined in package.json, it now warns instead of errors.

```
bun install
```

```
bun install v1.0.21 (f721bbe3)
6 |     "@types/bun": "latest",
        ^
warn: Duplicate dependency: "@types/bun" specified in package.json
   at errory/package.json:6:5

10 |       "@types/bun": "latest"
                         ^
note: "@types/bun" originally specified here
   at errory/package.json:10:21
```

Thanks to [@knightspore](https://github.com/knightspore) for fixing this bug!

## [Thanks to 20 contributors!](https://bun.com/blog/bun-v1.0.21#thanks-to-20-contributors)

* [@aarvinr](https://github.com/aarvinr)
* [@cirospaciari](https://github.com/cirospaciari)
* [@coratgerl](https://github.com/coratgerl)
* [@Hanaasagi](https://github.com/Hanaasagi)
* [@huseeiin](https://github.com/huseeiin)
* [@Jarred-Sumner](https://github.com/Jarred-Sumner)
* [@jeroenpg](https://github.com/jeroenpg)
* [@johnpyp](https://github.com/johnpyp)
* [@kaioduarte](https://github.com/kaioduarte)
* [@knightspore](https://github.com/knightspore)
* [@L422Y](https://github.com/L422Y)
* [@malthe](https://github.com/malthe)
* [@nektro](https://github.com/nektro)
* [@o-az](https://github.com/o-az)
* [@o2sevruk](https://github.com/o2sevruk)
* [@otgerrogla](https://github.com/otgerrogla)
* [@RiskyMH](https://github.com/RiskyMH)
* [@rtxanson](https://github.com/rtxanson)
* [@thunfisch987](https://github.com/thunfisch987)
* [@xlc](https://github.com/xlc)

[**Full Changelog**](https://github.com/oven-sh/bun/compare/bun-v1.0.20...bun-v1.0.21)

---

[#### Bun v1.0.20](https://bun.com/blog/bun-v1.0.20)[#### Bun v1.0.22](https://bun.com/blog/bun-v1.0.22)