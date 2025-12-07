---
url: https://bun.com/blog/bun-v0.6.6
title: Bun v0.6.6 | Bun Blog
source_domain: bun.com
---

# Bun v0.6.6 | Bun Blog

# Bun v0.6.6

---

[Ashcon Partovi](https://twitter.com/ashconpartovi) · May 31, 2023

We're hiring C/C++ and Zig engineers to build the future of JavaScript! [Join our team →](https://bun.com/careers)

We've been releasing a lot of changes to Bun recently, here's a recap in case you missed it:

* [`v0.6.0`](https://bun.com/blog/bun-bundler) - Introducing `bun build`, Bun's new JavaScript bundler.
* [`v0.6.2`](https://bun.com/blog/bun-v0.6.2) - Performance boosts: 20% faster `JSON.parse`, up to 2x faster `Proxy` and `arguments`.
* [`v0.6.3`](https://bun.com/blog/bun-v0.6.3) - Implemented `node:vm`, lots of fixes to `node:http` and `node:tls`.
* [`v0.6.4`](https://bun.com/blog/bun-v0.6.4) - Implemented `require.cache`, `process.env.TZ`, and 80% faster `bun test`.
* [`v0.6.5`](https://bun.com/blog/bun-v0.6.5) - Native support for CommonJS modules (*previously, Bun did CJS to ESM transpilation*), Vue support

Now, we're releasing Bun v0.6.6, with significant improvements to `bun test`, including Github Actions support, support for `test.only()`, `test.if()`, `describe.skip()`, and 15+ more `expect()` matchers; also streaming file uploads using `fetch()`.

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

## [`bun test` in Github Actions](https://bun.com/blog/bun-v0.6.6#bun-test-in-github-actions)

Bun will now detect if `bun test` is running in a Github Action.

First, it will collapse tests by file in the logs output to make it easier to read.

[![bun test in github action logs](https://github.com/oven-sh/bun/assets/3238291/abe19f52-87c4-441e-9ba2-19b2298bfda5)](https://github.com/oven-sh/bun/assets/3238291/abe19f52-87c4-441e-9ba2-19b2298bfda5)

Next, it will annotate errors with its name, message, and stack trace.

[![bun test in github annotations](https://github.com/oven-sh/bun/assets/3238291/8334fe38-0f4f-4046-beda-727a9b677b37)](https://github.com/oven-sh/bun/assets/3238291/8334fe38-0f4f-4046-beda-727a9b677b37)

You also don't need to install any plugins or extensions for this to work. Bun will read the `GITHUB_ACTIONS` environment variable and check if it's set to `true`.

## [`bun test --only`](https://bun.com/blog/bun-v0.6.6#bun-test-only)

You can now specify `--only` to only run tests that are marked with `test.only()` or `describe.only()`. This is useful when you want to debug a specific test in a file.

```
import { test, describe } from "bun:test";

describe.only("describe #1", () => {
  test("test #1", () => {
    // runs
  });
  test.skip("test #2", () => {
    // does not run
  });
});

test("test #3", () => {
  // does not run
});

test.only("test #4", () => {
  // runs
});
```

## [`bun test --todo`](https://bun.com/blog/bun-v0.6.6#bun-test-todo)

In addition to `test.skip()`, you can also define a test using `test.todo()` or `describe.todo()`. By default, these tests are not run, *unless* you specify `--todo`. This is useful for tests that are not yet implemented or are broken or flaky in some way.

```
import { test } from "bun:test";

test("test #1", () => {
  // runs
});

test.todo("test #2"); // never runs

test.todo("test #3", () => {
  // only runs if --todo is passed
});
```

## [`test.if()` and `describe.if()`](https://bun.com/blog/bun-v0.6.6#test-if-and-describe-if)

You can now specify a conditional test, based on a boolean value. You can also use `test.skipIf()` if you want the inverse behaviour.

So instead of doing this:

```
import { it } from "bun:test";

const macOS = process.arch === "darwin";
const test = macOS ? test : test.skip;
```

You can just do this:

```
import { test, describe } from "bun:test";

const macOS = process.arch === "darwin";

test.if(macOS)("test #1", () => {
  // runs if macOS
});

test.skipIf(macOS)("test #2", () => {
  // skips if macOS
});

describe.if(macOS)("describe #1", () => {
  test("test #3", () => {
    // runs if macOS
  });
});
```

## [Timeouts in `test()`](https://bun.com/blog/bun-v0.6.6#timeouts-in-test)

In Jest, you can specify a third argument to `test()` as a timeout value in milliseconds. In Vitest, you can also specify an object, with a `timeout` property. In Bun, you can now do both.

```
import { test } from "bun:test";
import { sleep } from "bun";

test("timeout #1", async () => {
  await sleep(10);
}, 1);

test(
  "timeout #2",
  async () => {
    await sleep(10);
  },
  { timeout: 1 },
);
```

The default timeout is 5000, you can change the default by using `--timeout`.

```
bun test --timeout 1000 # 1 second
```

## [New matchers for `expect()`](https://bun.com/blog/bun-v0.6.6#new-matchers-for-expect)

We've added a lot of new matchers to `expect()`, with more coming soon. Most of these are supported by the `jest-extended` matchers.

```
import { test, expect } from "bun:test";

test("new matchers", () => {
  expect(null).toBeNil();
  expect(true).toBeBoolean();
  expect(3.14).toBePositive();
  expect(314).toBeInteger();
  expect(3.1).toBeWithin(3, 3.14);
  expect(() => {}).toBeFunction();
  expect(new Date()).toBeDate();
  expect("bunny").toInclude("bun");
  expect("buntime").toStartWith("bun");
});
```

* [`toBeNil()`](https://jest-extended.jestcommunity.dev/docs/matchers/tobenil)
* [`toBeBoolean()`](https://jest-extended.jestcommunity.dev/docs/matchers/Boolean#tobeboolean)
* [`toBeTrue()`](https://jest-extended.jestcommunity.dev/docs/matchers/Boolean#tobetrue)
* [`toBeFalse()`](https://jest-extended.jestcommunity.dev/docs/matchers/Boolean#tobefalse)
* [`toBeNumber()`](https://jest-extended.jestcommunity.dev/docs/matchers/Number)
* [`toBeInteger()`](https://jest-extended.jestcommunity.dev/docs/matchers/Number#tobeinteger)
* [`toBeFinite()`](https://jest-extended.jestcommunity.dev/docs/matchers/Number#tobefinite)
* [`toBePositive()`](https://jest-extended.jestcommunity.dev/docs/matchers/Number#tobepositive)
* [`toBeNegative()`](https://jest-extended.jestcommunity.dev/docs/matchers/Number#tobenegative)
* [`toBeWithin(start, end)`](https://jest-extended.jestcommunity.dev/docs/matchers/Number#tobewithinstart-end)
* [`toBeSymbol()`](https://jest-extended.jestcommunity.dev/docs/matchers/Symbol)
* [`toBeFunction()`](https://jest-extended.jestcommunity.dev/docs/matchers/Function)
* [`toBeDate()`](https://jest-extended.jestcommunity.dev/docs/matchers/Date)
* [`toBeString()`](https://jest-extended.jestcommunity.dev/docs/matchers/String#tobestring)
* [`toInclude()`](https://jest-extended.jestcommunity.dev/docs/matchers/String#toincludesubstring)
* [`toStartWith()`](https://jest-extended.jestcommunity.dev/docs/matchers/String#tostartwithprefix)
* [`toEndWith()`](https://jest-extended.jestcommunity.dev/docs/matchers/String#toendwithsuffix)

## [Streaming `fetch()` file uploads](https://bun.com/blog/bun-v0.6.6#streaming-fetch-file-uploads)

You can now do a streaming upload a file using `fetch()` in Bun

```
import { file } from "bun";

await fetch("https://example.com/", {
  method: "POST",
  body: file("avatar.png"),
});
```

You can also do this with a `FormData` upload.

```
import { file } from "bun";

const formData = new FormData();
formData.set("attachment", file("data.csv"));

await fetch("https://example.com/", {
  method: "POST",
  body: formData,
});
```

When a large file is sent over HTTP, Bun automatically makes it faster using the `sendfile()` system call.

> uploading files with fetch() can be fast  
>   
> sending a 18 MB file over HTTP (client)  
>   
> Bun: 8.1ms  
> Deno: 19.0ms (2.3x slower)  
> Node: 32.3ms (3.9x slower) [pic.twitter.com/He2mnFzNAr](https://t.co/He2mnFzNAr)
>
> — Jarred Sumner (@jarredsumner) [May 31, 2023](https://twitter.com/jarredsumner/status/1663908194383708160?ref_src=twsrc%5Etfw)

## [Bug fixes](https://bun.com/blog/bun-v0.6.6#bug-fixes)

We also made various bug fixes.

Regressions in 0.6.5 from the CommonJS rewrite:

* `--watch` and `--hot` were broken when importing CommonJS modules, this is now fixed.
* Fixed a bug with `Object.defineProperty(module, "exports", { get })`, which fixes packages like `supports-color`.

More bugfixes:

* A bundler transform would incorrectly rewrite `module.exports` to `exports` when used in UMD modules, this is now fixed.
* Fixed a bug with `path.parse()` that did not resolve certain paths properly, thanks to [@cirospaciari](https://github.com/cirospaciari).
* Fixed a crash with `expect(null).toHaveProperty()`.
* Fixed a crash that could occur when an error is thrown in Bun.listen() or Bun.connect() callbacks (or `node:net` or `node:tls`)
* Fixed a bug where Bun.spawn() would attempt to chdir to an empty string
* Fixed a mistranspilation involving optional chaining with computed properties in multiple levels of nesting thanks to [@dylan-conway](https://github.com/dylan-conway)

More things:

* Added the `--no-macros` flag and disabled macros in the `node_modules` folder
* Added the `macro` package.json export condition

---

[#### Bun v0.6.5](https://bun.com/blog/bun-v0.6.5)[#### Bun v0.6.7](https://bun.com/blog/bun-v0.6.7)