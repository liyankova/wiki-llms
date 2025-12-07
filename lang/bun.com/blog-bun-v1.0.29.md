---
url: https://bun.com/blog/bun-v1.0.29
title: Bun v1.0.29 | Bun Blog
source_domain: bun.com
---

# Bun v1.0.29 | Bun Blog

# Bun v1.0.29

---

[Jarred Sumner](https://twitter.com/jarredsumner) · February 23, 2024

Bun is an incredibly fast JavaScript runtime, bundler, transpiler, and package manager — all in one.

This release fixes 8 bugs. `Bun.stringWidth(a)` is a ~6,756x faster drop-in replacement for the popular `"string-width"` package. bunx now checks for updates more frequently. Adds `expect().toBeOneOf()` in `bun:test`. Memory leak impacting Prisma is fixed. Shell now supports advanced redirects like `2>&1`, `&>`. Reliability improvements to bunx, bun install, WebSocket client, and Bun Shell

#### Previous releases

* [`v1.0.28`](https://bun.com/blog/bun-v1.0.28) fixes 6 bugs (addressing 26 👍 reactions). Fixes bugs impacting Prisma and Astro, `node:events`, `node:readline`, and `node:http2`. Fixes a bug in Bun Shell involving stdin redirection and fixes bugs in `bun:test` with `test.each` and `describe.only`.
* [`v1.0.27`](https://bun.com/blog/bun-v1.0.27) fixes 72 bugs (addressing 192 👍 reactions), Bun Shell supports throwing on non-zero exit codes, stream Response bodies using async generators, improves reliability of fetch(), http2 client, Bun.Glob fixes. Fixes a regression with bun --watch on Linux. Improves Node.js compatibility
* [`v1.0.26`](https://bun.com/blog/bun-v1.0.26) fixes 30 bugs (addressing 60 👍 reactions), adds support for multi-statement queries in bun:sqlite, makes bun --watch more reliable in longer-running sessions, Bun.FileSystemRouter now supports more than 64 routes, fixes a bug with expect().toStrictEqual(), fixes 2 bugs with error.stack, improves Node.js compatibility

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

## [bunx checks for updates more frequently](https://bun.com/blog/bun-v1.0.29#bunx-checks-for-updates-more-frequently)

`bunx` is like `npx` except powered by `bun install`. It starts [100x faster than npx](https://twitter.com/jarredsumner/status/1606163655527059458?lang=en).

A cache invalidation bug in `bunx` caused it to not check for updates as frequently as it should. Now we rely on the timestamp from `stat` to determine if it's been 24 hours since the last check, which is more reliable.

We've also made it so explicitly using a tag like `bunx create-vite@latest` will always check for the latest version and delete the previously installed version if it existed.

Thanks to [@paperclover](https://github.com/paperclover) for fixing this.

## [Bun.stringWidth() ~6,756x faster `"string-width"` replacement](https://bun.com/blog/bun-v1.0.29#bun-stringwidth-6-756x-faster-string-width-replacement)

`Bun.stringWidth(string)` returns the visible width of a string in a terminal. This is useful when you want to know how many columns a string will take up in a terminal.

```
import { stringWidth } from "bun";

// text
console.log(stringWidth("hello")); // => 5

// emoji
console.log(stringWidth("👋")); // => 2

// ansi colors
console.log(stringWidth("\u001b[31mhello\u001b[39m")); // => 5

// fullwidth characters
console.log(stringWidth("你好")); // => 4

// graphemes
console.log(stringWidth("👩‍👩‍👧‍👦")); // => 2
```

It accounts for [ANSI escape codes](https://en.wikipedia.org/wiki/ANSI_escape_code), [fullwidth characters](https://en.wikipedia.org/wiki/Halfwidth_and_fullwidth_forms), graphemes, and emojis. It supports Latin1, UTF-16, and UTF-8 encodings, with optimized implementations for each.

The [`string-width`](https://www.npmjs.com/package/string-width) package gets over 100m downloads/week. Making it a built-in function in Bun means you don't need to install an extra package for this common use case, and lets us optimize it. Huge thanks to [@sindresorhus](https://github.com/sindresorhus) for creating `string-width` and for the inspiration to include it in Bun.

[In this benchmark](https://github.com/oven-sh/bun/blob/f75306db0fc6ab6e0755128d062d7451266d4f0d/bench/snippets/string-width.mjs#L1-L40), `Bun.stringWidth` performs ~6,756x faster than `string-width` for ascii input > 500 characters. The range is from 48x faster in the worst-case scenario to 137,623x faster for 25,000 ascii or ansi characters.

```
❯ bun string-width.mjs
cpu: 13th Gen Intel(R) Core(TM) i9-13900
runtime: bun 1.0.29 (x64-linux)

benchmark                                          time (avg)             (min … max)       p75       p99      p995
------------------------------------------------------------------------------------- -----------------------------
Bun.stringWidth     500 chars ascii              37.09 ns/iter   (36.77 ns … 41.11 ns)  37.07 ns  38.84 ns  38.99 ns

❯ node string-width.mjs
cpu: 13th Gen Intel(R) Core(TM) i9-13900
runtime: node v21.4.0 (x64-linux)

benchmark                                          time (avg)             (min … max)       p75       p99      p995
------------------------------------------------------------------------------------- -----------------------------
npm/string-width    500 chars ascii             249,710 ns/iter (239,970 ns … 293,180 ns) 250,930 ns  276,700 ns 281,450 ns
```

To make `Bun.stringWidth` fast, we've implemented it in Zig using optimized SIMD instructions, accounting for Latin1, UTF-16, and UTF-8 encodings. It implements the same API as `string-width` and passes their tests. This also fixes an edgecase in `console.table`. Thanks to [@nektro](https://github.com/nektro) for implementing this!

View full benchmark

As a reminder, 1 nanosecond (ns) is 1 billionth of a second. Here's a quick reference for converting between units:

| Unit | Per 1 Millisecond |
| --- | --- |
| ns | 1 / 1,000,000 |
| µs | 1 / 1,000 |
| ms | 1 |
| s | 1000 |

Bun:

```
❯ bun string-width.mjs
cpu: 13th Gen Intel(R) Core(TM) i9-13900
runtime: bun 1.0.29 (x64-linux)

benchmark                                          time (avg)             (min … max)       p75       p99      p995
------------------------------------------------------------------------------------- -----------------------------
Bun.stringWidth      5 chars ascii              16.52 ns/iter    (16.28 ns … 20.3 ns)   16.5 ns  17.44 ns  17.57 ns
Bun.stringWidth     50 chars ascii              20.02 ns/iter   (19.19 ns … 28.14 ns)  19.99 ns  21.96 ns  22.22 ns
Bun.stringWidth    500 chars ascii              37.31 ns/iter    (36.69 ns … 40.7 ns)   37.1 ns  39.21 ns  39.27 ns
Bun.stringWidth  5,000 chars ascii             216.34 ns/iter (215.71 ns … 228.52 ns) 216.22 ns 228.05 ns 228.48 ns
Bun.stringWidth 25,000 chars ascii               1.01 µs/iter     (1.01 µs … 1.06 µs)   1.01 µs   1.06 µs   1.06 µs
Bun.stringWidth      9 chars ascii+ansi         20.59 ns/iter   (20.35 ns … 22.48 ns)  20.55 ns  21.72 ns  21.83 ns
Bun.stringWidth     90 chars ascii+ansi         23.87 ns/iter   (23.61 ns … 26.56 ns)  23.84 ns  25.43 ns  26.55 ns
Bun.stringWidth    900 chars ascii+ansi         53.74 ns/iter   (53.42 ns … 56.88 ns)  53.64 ns  56.73 ns  56.76 ns
Bun.stringWidth  9,000 chars ascii+ansi        377.62 ns/iter (377.22 ns … 379.05 ns) 377.73 ns 378.96 ns 379.05 ns
Bun.stringWidth 45,000 chars ascii+ansi          1.82 µs/iter     (1.81 µs … 1.92 µs)   1.82 µs   1.92 µs   1.92 µs
Bun.stringWidth      7 chars ascii+emoji        54.06 ns/iter   (53.43 ns … 55.01 ns)  54.21 ns  54.74 ns   54.8 ns
Bun.stringWidth     70 chars ascii+emoji        355.6 ns/iter (350.89 ns … 378.26 ns) 356.72 ns 375.33 ns 378.26 ns
Bun.stringWidth    700 chars ascii+emoji          3.3 µs/iter     (3.28 µs … 3.38 µs)    3.3 µs   3.38 µs   3.38 µs
Bun.stringWidth  7,000 chars ascii+emoji        32.72 µs/iter   (32.23 µs … 815.5 µs)  32.73 µs  33.85 µs  33.95 µs
Bun.stringWidth 35,000 chars ascii+emoji       163.83 µs/iter (161.33 µs … 177.04 µs) 163.99 µs 174.15 µs 175.94 µs
Bun.stringWidth      8 chars ansi+emoji         67.94 ns/iter   (67.31 ns … 69.56 ns)  68.09 ns  68.56 ns  68.68 ns
Bun.stringWidth     80 chars ansi+emoji        495.47 ns/iter (488.47 ns … 524.57 ns) 496.08 ns 523.26 ns 524.57 ns
Bun.stringWidth    800 chars ansi+emoji          4.72 µs/iter      (4.7 µs … 4.82 µs)   4.72 µs   4.82 µs   4.82 µs
Bun.stringWidth  8,000 chars ansi+emoji         46.84 µs/iter   (46.35 µs … 56.24 µs)  46.92 µs  47.91 µs  48.07 µs
Bun.stringWidth 40,000 chars ansi+emoji        235.04 µs/iter (231.83 µs … 249.74 µs) 234.89 µs 247.96 µs 248.18 µs
Bun.stringWidth     19 chars ansi+emoji+ascii  136.22 ns/iter (135.02 ns … 139.89 ns) 136.47 ns 139.26 ns 139.56 ns
Bun.stringWidth    190 chars ansi+emoji+ascii    1.17 µs/iter     (1.16 µs … 1.23 µs)   1.17 µs   1.23 µs   1.23 µs
Bun.stringWidth  1,900 chars ansi+emoji+ascii   11.45 µs/iter   (11.25 µs … 16.09 µs)  11.45 µs  12.09 µs  12.15 µs
Bun.stringWidth 19,000 chars ansi+emoji+ascii     114 µs/iter (112.86 µs … 120.02 µs) 114.18 µs 116.39 µs 116.68 µs
Bun.stringWidth 95,000 chars ansi+emoji+ascii  571.82 µs/iter (564.88 µs … 605.42 µs) 572.04 µs 603.22 µs  603.9 µs
```

Node.js:

```
❯ node string-width.mjs
cpu: 13th Gen Intel(R) Core(TM) i9-13900
runtime: node v21.4.0 (x64-linux)

benchmark                                           time (avg)             (min … max)       p75       p99      p995
-------------------------------------------------------------------------------------- -----------------------------
npm/string-width      5 chars ascii               3.16 µs/iter     (3.05 µs … 3.42 µs)   3.19 µs   3.42 µs   3.42 µs
npm/string-width     50 chars ascii              20.12 µs/iter  (18.89 µs … 415.35 µs)   19.5 µs  21.95 µs  22.77 µs
npm/string-width    500 chars ascii             250.09 µs/iter   (240.33 µs … 2.07 ms) 250.36 µs 276.33 µs 284.44 µs
npm/string-width  5,000 chars ascii               6.74 ms/iter     (6.63 ms … 6.85 ms)   6.76 ms   6.85 ms   6.85 ms
npm/string-width 25,000 chars ascii             144.36 ms/iter  (143.2 ms … 146.15 ms) 144.78 ms 146.15 ms 146.15 ms
npm/string-width      9 chars ascii+ansi          4.66 µs/iter     (4.55 µs … 5.01 µs)   4.71 µs   5.01 µs   5.01 µs
npm/string-width     90 chars ascii+ansi         36.15 µs/iter  (34.42 µs … 513.73 µs)  35.42 µs  39.33 µs 149.33 µs
npm/string-width    900 chars ascii+ansi        508.56 µs/iter (490.99 µs … 540.08 µs) 515.87 µs 533.68 µs 536.92 µs
npm/string-width  9,000 chars ascii+ansi         19.33 ms/iter   (18.92 ms … 19.55 ms)   19.4 ms  19.55 ms  19.55 ms
npm/string-width 45,000 chars ascii+ansi        451.84 ms/iter (444.37 ms … 458.41 ms) 454.91 ms 458.41 ms 458.41 ms
npm/string-width      7 chars ascii+emoji         3.75 µs/iter      (3.64 µs … 4.2 µs)    3.9 µs    4.2 µs    4.2 µs
npm/string-width     70 chars ascii+emoji        23.78 µs/iter   (22.25 µs … 395.2 µs)  23.01 µs  25.39 µs  28.46 µs
npm/string-width    700 chars ascii+emoji       251.04 µs/iter (237.56 µs … 469.57 µs) 254.47 µs 334.36 µs 407.38 µs
npm/string-width  7,000 chars ascii+emoji          4.6 ms/iter     (4.45 ms … 6.45 ms)   4.61 ms   5.48 ms   6.45 ms
npm/string-width 35,000 chars ascii+emoji        92.82 ms/iter    (91.79 ms … 95.1 ms)   92.7 ms   95.1 ms   95.1 ms
npm/string-width      8 chars ansi+emoji           4.3 µs/iter     (3.76 µs … 4.82 µs)   4.56 µs   4.82 µs   4.82 µs
npm/string-width     80 chars ansi+emoji         24.26 µs/iter  (22.67 µs … 652.98 µs)  23.45 µs  25.91 µs  27.83 µs
npm/string-width    800 chars ansi+emoji        259.56 µs/iter (244.07 µs … 490.51 µs) 257.48 µs 348.52 µs  410.1 µs
npm/string-width  8,000 chars ansi+emoji          5.33 ms/iter     (5.15 ms … 5.56 ms)   5.47 ms   5.55 ms   5.56 ms
npm/string-width 40,000 chars ansi+emoji        104.32 ms/iter (102.36 ms … 110.73 ms) 104.94 ms 110.73 ms 110.73 ms
npm/string-width     19 chars ansi+emoji+ascii    6.55 µs/iter     (6.36 µs … 6.77 µs)   6.58 µs   6.77 µs   6.77 µs
npm/string-width    190 chars ansi+emoji+ascii   55.18 µs/iter  (52.49 µs … 317.03 µs)  53.88 µs  81.87 µs 171.48 µs
npm/string-width  1,900 chars ansi+emoji+ascii  699.56 µs/iter (650.96 µs … 933.47 µs) 720.99 µs 817.92 µs 847.01 µs
npm/string-width 19,000 chars ansi+emoji+ascii   25.99 ms/iter    (25.6 ms … 27.59 ms)  26.12 ms  27.59 ms  27.59 ms
npm/string-width 95,000 chars ansi+emoji+ascii      3.7 s/iter       (3.68 s … 3.73 s)    3.71 s    3.73 s    3.73 s
```

## [`expect(a).toBeOneOf([a, b, c])` in `bun:test`](https://bun.com/blog/bun-v1.0.29#expect-a-tobeoneof-a-b-c-in-bun-test)

[`bun:test`](https://bun.sh/docs/cli/test) gets a new matcher: `toBeOneOf`. This is useful when you want to check if a value is one of a list of values.

```
import { test, expect } from "bun:test";

test("my test here", () => {
  expect(1).toBeOneOf([1, 2, 3]);
});
```

This matcher is also supported by the popular [`jest-extended`](https://jest-extended.jestcommunity.dev/docs/matchers/toBeOneOf) package.

> looks like expect().toBeOneOf() is 500x faster in bun test compared to Jest [pic.twitter.com/0sAGJ8um8v](https://t.co/0sAGJ8um8v)
>
> — Jarred Sumner (@jarredsumner) [February 22, 2024](https://twitter.com/jarredsumner/status/1760779425371836771?ref_src=twsrc%5Etfw)

##### How is this different than expect(a).toInclude(b)?

`expect(a).toInclude(b)` checks if `a` includes `b`. `expect(a).toBeOneOf([a, b, c])` checks if `a` is one of `[a, b, c]`. `toBeOneOf` operates on the actual value, while `toInclude` operates on the expected value.

```
import { test, expect } from "bun:test";

test("my test here", () => {
  expect([1, 2, 3]).toInclude(1);
  expect(1).toBeOneOf([1, 2, 3]);
});
```

When the goal is to check if a value is one of a list of values, `toBeOneOf` is more readable and gives a better error message when it fails.

## [Shell supports advanced redirects like `2>&1`, `&>`](https://bun.com/blog/bun-v1.0.29#shell-supports-advanced-redirects-like-2-1)

Bun Shell now supports advanced redirects like `2>&1` and `&>`

To output stderr to stdout, you can use `2>&1`:

```
import { $ } from "bun";

await $`vite build 2>&1 output.txt`;
```

To redirect both stdout and stderr, you can use `&>`:

```
import { $ } from "bun";

await $`next build &> output.txt`;
```

We've also added support for `2>>` to append stderr.

Thanks to [@zackradisic](https://github.com/zackradisic) for implementing this.

## [Fixed: bun install semver pre-release bug](https://bun.com/blog/bun-v1.0.29#fixed-bun-install-semver-pre-release-bug)

An edgecase where `bun install` would sometimes fail to resolve a pre-release version that `node-semver` resolved correctly has been fixed.

This bug impacted the `svelte-eslint-parser` package with an error like:

```
error: No version matching ">=0.34.0-next.4 <1.0.0" found for specifier "svelte-eslint-parser"
```

Thanks to [@dylan-conway](https://github.com/dylan-conway) for fixing this.

## [Fixed: WebSocket client short messages bug](https://bun.com/blog/bun-v1.0.29#fixed-websocket-client-short-messages-bug)

A bug where a message with a payload of 1 or 2 bytes would sometimes cause timeouts in the WebSocket client has been fixed. This bug did not impact the WebSocket server. Thanks to [@lithdew](https://github.com/lithdew) for fixing this. This was @lithdew's first PR to Bun, but we've been using @lithdew's open source code in many places throughout Bun for awhile now.

## [Fixed: Memory leak in napi impacting Prisma](https://bun.com/blog/bun-v1.0.29#fixed-memory-leak-in-napi-impacting-prisma)

A memory leak in napi (which impacted Prisma) has been fixed.

[In a microbenchmark](https://github.com/oven-sh/bun/pull/9035), it reduced memory usage from 1720 megabytes to 275 megabytes (a 6x reduction).

Thanks to [@camero2734](https://github.com/camero2734) for fixing this.

## [Fixed: Memory leak regression in response.blob()](https://bun.com/blog/bun-v1.0.29#fixed-memory-leak-regression-in-response-blob)

A regression introduced in Bun v1.0.26 causing a memory leak in `response.blob()` has been fixed. Thanks to [@nektro](https://github.com/nektro) for fixing this!

## [Fixed: Bun.password.verify on long passwords with bcrypt](https://bun.com/blog/bun-v1.0.29#fixed-bun-password-verify-on-long-passwords-with-bcrypt)

bcrypt has a maximum password length of 72 characters. This is part of the reason why `Bun.password.hash` defaults to the more modern [`Argon2`](https://en.wikipedia.org/wiki/Argon2) algorithm.

To compensate for the max password length in bcrypt, when `algorithm` is set to `bcrypt` and the password is longer than 72 characters, `Bun.password.hash` uses SHA-512 on the password input and sends the SHA-512 hash to bcrypt (the choice of SHA-512 was suggested by the author of the popular [libsodium](https://github.com/jedisct1/libsodium) cryptography library).

But, we weren't doing this for `Bun.password.verify` when the password was longer than 72 characters and the algorithm was set to `bcrypt`. This meant you could run into situations where `Bun.password.verify` would return `false` for a password that was previously hashed with `Bun.password.hash`.

This has been fixed so that `Bun.password.verify` now behaves the same as `Bun.password.hash` when the password is longer than 72 characters when using bcrypt. Thanks to [@argosphil](https://github.com/argosphil) for fixing this.

## [Fixed: bun install vendored node\_modules with hardlinks](https://bun.com/blog/bun-v1.0.29#fixed-bun-install-vendored-node-modules-with-hardlinks)

Occasionally, packages published to npm include a vendored `node_modules` directory in a subdirectory (often by accident). Previously, `bun install` would ignore these vendored node\_modules folders when using hardlinks to install, which broke packages relying on this behavior. We've fixed it so `bun install` no longer ignores vendored node\_modules folders.

Thanks to [@eemelipa](https://github.com/eemelipa) for fixing this.

## [Fixed: Shell substitution bug adding extra space character](https://bun.com/blog/bun-v1.0.29#fixed-shell-substitution-bug-adding-extra-space-character)

Previously, the following code in Bun Shell would add an extra space character:

```
echo $(echo id)/$(echo region) # => "id / region"
```

Now it correctly outputs:

```
echo $(echo id)/$(echo region) # => "id/region"
```

Thanks to [@zackradisic](https://github.com/zackradisic).

## [Fixed: Shell latin1 template encoding bug](https://bun.com/blog/bun-v1.0.29#fixed-shell-latin1-template-encoding-bug)

A bug where Bun Shell would sometimes handle non-ascii latin1 characters incorrectly has been fixed. Thanks to [@zackradisic](https://github.com/zackradisic).

## [Fixed: bunx with multiple users on the same machine](https://bun.com/blog/bun-v1.0.29#fixed-bunx-with-multiple-users-on-the-same-machine)

bunx now works correctly when multiple users on the same machine use it. Since bunx stores its cache in the temporary directory, multiple users on the same machine share the same cache directory. This sometimes caused permissions issues. We've fixed this by including the `uid` in the cache key so that different users don't share the same cache.

Thanks to [@paperclover](https://github.com/paperclover) for fixing this.

## [Bundows is soon](https://bun.com/blog/bun-v1.0.29#bundows-is-soon)

We continue to work on Windows support. Windows will be supported in Bun v1.1.

## [Thanks to 8 contributors!](https://bun.com/blog/bun-v1.0.29#thanks-to-8-contributors)

* [@argosphil](https://github.com/argosphil)
* [@camero2734](https://github.com/camero2734)
* [@dylan-conway](https://github.com/dylan-conway)
* [@eemelipa](https://github.com/eemelipa)
* [@Jarred-Sumner](https://github.com/Jarred-Sumner)
* [@lithdew](https://github.com/lithdew)
* [@nektro](https://github.com/nektro)
* [@paperclover](https://github.com/paperclover)
* [@zackradisic](https://github.com/zackradisic)

---

[#### Bun v1.0.28](https://bun.com/blog/bun-v1.0.28)[#### Bun v1.0.30](https://bun.com/blog/bun-v1.0.30)