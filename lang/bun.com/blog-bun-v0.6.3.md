---
url: https://bun.com/blog/bun-v0.6.3
title: Bun v0.6.3 | Bun Blog
source_domain: bun.com
---

# Bun v0.6.3 | Bun Blog

# Bun v0.6.3

---

[Ashcon Partovi](https://twitter.com/ashconpartovi) · May 22, 2023

We're hiring C/C++ and Zig engineers to build the future of JavaScript! [Join our team →](https://bun.com/careers)

Last week, we launched our new JavaScript [bundler](https://bun.com/blog/bun-bundler) in Bun [v0.6.0](https://bun.com/blog/bun-v0.6.0).

Today, we're releasing support for [`node:vm`](https://nodejs.org/api/vm.html#vm-executing-javascript), improvements to [`node:tls`](https://nodejs.org/api/tls.html#tls-ssl) and [`node:http`](https://nodejs.org/api/http.html#http) — which fixes support for `socket.io` and `mongodb`, improvements to `bun test` — which introduces `test.todo()`, test timeouts, and better preloading, and many fixes to Bun's bundler.

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

## [Introducing `node:vm`](https://bun.com/blog/bun-v0.6.3#introducing-node-vm)

Bun now has support for the built-in [`node:vm`](https://nodejs.org/api/vm.html#vm-executing-javascript) module. It can be used to execute code, similar to [`eval()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval), except with more control over which `globalThis` JavaScript context the code is executed.

[![image](https://github.com/oven-sh/bun/assets/709451/98bda1f7-fbe5-47ee-bc14-3fd0a5f47f7e)](https://github.com/oven-sh/bun/assets/709451/98bda1f7-fbe5-47ee-bc14-3fd0a5f47f7e)

```
import { runInContext } from "node:vm";

let context = {
  foo: "bar",
  baz: 123,
};

runInContext(`foo = "fizz"; delete baz;`, context);

console.log(context.foo); // "fizz"
console.log(context.baz); // undefined
```

You can also use [`runInNewContext`](https://nodejs.org/api/vm.html#scriptruninnewcontextcontextobject-options) to run code in a separate JavaScript context.

```
import { runInNewContext } from "node:vm";

runInNewContext(`globalThis.fetch = undefined;`);

console.log(globalThis.fetch); // [Function fetch]
```

Thanks to [@silversquirl](https://github.com/silversquirl) for implementing this feature!

## [Fixes for `node:tls` and `node:http`](https://bun.com/blog/bun-v0.6.3#fixes-for-node-tls-and-node-http)

We've fixed a lot of code with TLS and HTTP, such as TLS handshaking, so you can now use `socket.io` and `mongodb` authentication in Bun.

> In the next version of Bun<https://t.co/Pc0bps2VFV> server works, and it runs 2x faster in Bun.  
>   
> left: bun (400k msgs/sec)  
> right: node (200k msgs/sec) [pic.twitter.com/9jW09NiGGc](https://t.co/9jW09NiGGc)
>
> — Jarred Sumner (@jarredsumner) [May 21, 2023](https://twitter.com/jarredsumner/status/1660351943901057025?ref_src=twsrc%5Etfw)

Thanks to [@cirospaciari](https://github.com/cirospaciari) for working on this!

## [Improvments to `bun test`](https://bun.com/blog/bun-v0.6.3#improvments-to-bun-test)

### [`test.todo()`](https://bun.com/blog/bun-v0.6.3#test-todo)

You can now use [`test.todo()`](https://jestjs.io/docs/api#testtodoname) to mark tests that you want to implement later.

[![image](https://github.com/oven-sh/bun/assets/709451/053a3dfe-3734-47e8-b59d-4d0f541fa05a)](https://github.com/oven-sh/bun/assets/709451/053a3dfe-3734-47e8-b59d-4d0f541fa05a)

### [`expect().toBeCloseTo()`](https://bun.com/blog/bun-v0.6.3#expect-tobecloseto)

You can also use [`expect().toBeCloseTo()`](https://jestjs.io/docs/expect#tobeclosetonumber-numdigits) to compare two floating-point numbers.

```
import { test, expect } from "bun:test";

test("toBeCloseTo()", () => {
  expect(3 + 0.14).toBeCloseTo(3.14);
  expect(3.14).toBeCloseTo(Math.PI, 2);
});
```

Thanks to [@blackmann](https://github.com/blackmann) for working on both of these features!

### [Test timeouts](https://bun.com/blog/bun-v0.6.3#test-timeouts)

You can now set a timeout for your tests with a third argument to [`test()`](https://jestjs.io/docs/api#testname-fn-timeout).

```
import { test } from "bun:test";

test("i took too long", async () => {
  await Bun.sleep(100);
}, 50); // the last argument is a timeout in milliseconds
```

[![image](https://github.com/oven-sh/bun/assets/709451/f40c2326-5da4-41ef-bece-786c21c934f6)](https://github.com/oven-sh/bun/assets/709451/f40c2326-5da4-41ef-bece-786c21c934f6)

### [Hook support with `--preload`](https://bun.com/blog/bun-v0.6.3#hook-support-with-preload)

You can now use `beforeAll`, `beforeEach`, `afterEach`, and `afterAll` with the `--preload` flag.

This lets you run code before and after all files instead of just the current file. This is useful for libraries that need to be initialized before running tests.

```
import { test, beforeAll, beforeEach, afterEach, afterAll } from "bun:test";

beforeEach(() => {
  console.log("This runs before each test in every file");
});
```

### [Fixes to pretty-printing](https://bun.com/blog/bun-v0.6.3#fixes-to-pretty-printing)

We also fixed bug that would cause code like this to print values as `undefined` in the test runner.

```
import { test, expect } from "bun:test";

test("wat", () => {
  const left = {};
  const right = {};
  for (let i = 0; i < 2; i++) {
    left[i] = i + 1;
    right[i] = i + 2;
  }
  expect(left).toBe(right);
});
```

| Before | After |
| --- | --- |
| [image](https://github.com/oven-sh/bun/assets/709451/6ce87cb5-b789-425f-9adc-1874d1e2bb17) | [image](https://github.com/oven-sh/bun/assets/709451/bb8b03bf-78e3-4ba0-a9f4-5a58af5ca7cf) |

## [Fixes to `bun build`](https://bun.com/blog/bun-v0.6.3#fixes-to-bun-build)

* A crash that was highlighted in [*Using Bun.js as a bundler*](https://shaneosullivan.wordpress.com/2023/05/17/using-bun-js-as-a-bundler/) when `--minify` with multiple entry points was enabled has been fixed. It was a race condition when merging adjacent top-level variable declarations.
* A bug that caused assets to copy to an incorrect output path has been fixed.
* A minifier bug involving template literals being incorrectly merged has been fixed.
* A race condition that could occur when generating sourcemaps has been fixed.
* A bug that allowed generated variable names to start with numbers has been fixed.
* A crash that could occur when creating the `BuildArtifact` objects after saving to disk has been fixed.
* A memory leak in the logs has been fixed.
* Improved an error message when using a Node.js built-in when building for browsers to suggest g the `--target` option to `node` or `bun`.

## [`fetch()` memory leak](https://bun.com/blog/bun-v0.6.3#fetch-memory-leak)

Two memory leaks found in `fetch()` have been fixed.

1. The callback was creating two strongly-held references to the `Promise<Response>` object, which prevented it from being garbage collected.
2. The input validation logic would potentially create a strongly held `Promise<Response>` and immediately discarded it, without releasing the strong reference. This prevented the `Promise<Response>` from being garbage collected.

This was embarrassing and we've improved our test coverage for memory leak tests to make sure this doesn't happen again. Here was graph of the memory leak, courtesy of @dimka3553:

[![](https://user-images.githubusercontent.com/37512400/239773697-5eb7334e-ee26-4ef1-9bdd-9bf9f30b9aa5.png)](https://user-images.githubusercontent.com/37512400/239773697-5eb7334e-ee26-4ef1-9bdd-9bf9f30b9aa5.png)

## [Improvements to `console.log()`](https://bun.com/blog/bun-v0.6.3#improvements-to-console-log)

### [Mismatched quotes](https://bun.com/blog/bun-v0.6.3#mismatched-quotes)

Previously, `console.log()` would print mismatched quotes for non-ascii property names. This is now fixed.

```
{
  '🐛 Bug with mismatched quotes": 'fixed'
}
```

### [Set depth limit](https://bun.com/blog/bun-v0.6.3#set-depth-limit)

Previously, `console.log()` would print an infinite amount of nested objects, excluding circular references. This was sometimes undesirable and caused crashes when printing sufficiently large objects. This has been fixed with a depth limit of 8.

### [Remove unnecessary quote identifiers](https://bun.com/blog/bun-v0.6.3#remove-unnecessary-quote-identifiers)

Previously, Bun would unnecessarily quote object keys in `console.log` and this was a little noisy. After a Twitter poll voted 90% in favor of removing the quotes, we did it.

> in the next version of bun  
>   
> console.log(obj) property keys with valid identifiers are no longer quoted [pic.twitter.com/w1uSCovyRM](https://t.co/w1uSCovyRM)
>
> — Jarred Sumner (@jarredsumner) [May 19, 2023](https://twitter.com/jarredsumner/status/1659688553255948288?ref_src=twsrc%5Etfw)

## [Changes to `WebSocket`](https://bun.com/blog/bun-v0.6.3#changes-to-websocket)

### [Breaking change to `publishToSelf` behaviour](https://bun.com/blog/bun-v0.6.3#breaking-change-to-publishtoself-behaviour)

Bun supports [publish/subscribe](https://bun.sh/docs/api/websockets#pub-sub) in its server-side `WebSocket` APIs. You can use `Server.publish()` or `ServerWebSocket.publish()` to send a message to each connected client.

However, we made a design mistake with the `ServerWebSocket.publish()` API, as it also sent a message to itself — when the typical behaviour is to exclude it. We patched this mistake by introducing an optional `publishToSelf` option, but the default behaviour was still confusing, as highlighted by [various](https://github.com/oven-sh/bun/issues/1803) [issues](https://github.com/oven-sh/bun/issues/2709).

So we're relunctantly fixing this behaviour, with a breaking change, to match developers' intuition. We rarely make these types of decisions, but when we do, we make sure there is overwhelming evidence and feedback that maintaing the status-quo is more harmful than any potential breakage.

```
const server = Bun.serve({
  websocket: {
    open(ws) {
      ws.subscribe("topic");
      // <= Bun v0.6.2
      ws.publish("topic", "send to all clients, including `ws`");
      // >= Bun v0.6.3
      ws.publish("topic", "send to all clients, excluding `ws`");
    },
  },
  fetch(request, server) {
    if (server.upgrade(request)) {
      return;
    }
    return new Response();
  },
});
```

### [`Buffer` support in `WebSocket` messages](https://bun.com/blog/bun-v0.6.3#buffer-support-in-websocket-messages)

Many npm packages expect `Buffer` objects as `WebSocket` messages. Instead of asking you to re-create the `Buffer` object yourself when passing through to a library, Bun now lets you directly receive a `"nodebuffer"` value for binary WebSocket messages.

```
const server = Bun.serve({
  websocket: {
    open(ws) {
      ws.binaryType = "nodebuffer";
      ws.send(Buffer.from("hello world"));
    },
    message(ws, message) {
      console.log(Buffer.isBuffer(message)); // true
    },
  },
  fetch(request, server) {
    if (server.upgrade(request)) {
      return;
    }
    return new Response("hello world");
  },
});

const client = new WebSocket("ws://localhost:3000");
client.binaryType = "nodebuffer";
client.onmessage = ({ data }) => {
  console.log(Buffer.isBuffer(data)); // true
};
```

## [More bug fixes](https://bun.com/blog/bun-v0.6.3#more-bug-fixes)

* `fs.writeFile({ flag: "a" })` now appends to files instead of overwriting it
* N-API finalizers are now called with the correct data pointer and finalizer hint
* A crash that could occur when creating many Error objects inside a bound function has been fixed, thanks to [@Constellation](https://github.com/Constellation)
* Setting megamorphic property values gets faster in this release, thanks to [@Constellation](https://github.com/Constellation)

## [Changelog](https://bun.com/blog/bun-v0.6.3#changelog)

| [`2544742`](https://github.com/oven-sh/bun/commit/25447426f19702a0fff808b3d426d66f4d8e558d) | Fixed memory leak with `BuildError` and `ResolveError` by [@Jarred-Sumner](https://github.com/Jarred-Sumner) |
| [`4f7198f`](https://github.com/oven-sh/bun/commit/4f7198f780fa5e345c6eeed3f98f30b03f2a6d32) | Fixed incorrect behaviour with `fs.writeFile({ flag: "a" })` by [@Jarred-Sumner](https://github.com/Jarred-Sumner) |
| [`aacbef3`](https://github.com/oven-sh/bun/commit/aacbef3cf99206aa15e71491c55aba7156fe2caf) | Improved error message when node built-in could not be resolved by [@Jarred-Sumner](https://github.com/Jarred-Sumner) |
| [`#2939`](https://github.com/oven-sh/bun/pull/2939) | Fixed incorrect encoding of utf8 property names by [@Jarred-Sumner](https://github.com/Jarred-Sumner) |
| [`#2937`](https://github.com/oven-sh/bun/pull/2937) | Fixed bug with incorrect `String.raw` output by [@dylan-conway](https://github.com/dylan-conway) |
| [`#2870`](https://github.com/oven-sh/bun/pull/2870) | Implemented `expect().toBeCloseTo()` by [@blackmann](https://github.com/blackmann) |
| [`#2947`](https://github.com/oven-sh/bun/pull/2947) | Fixed crash when bundling with multiple entrypoints by [@Jarred-Sumner](https://github.com/Jarred-Sumner) |
| [`#2949`](https://github.com/oven-sh/bun/pull/2949) | Fixed "Numeric separators are not allowed at the end of numeric literals" by [@Jarred-Sumner](https://github.com/Jarred-Sumner) |
| [`5bec025`](https://github.com/oven-sh/bun/commit/5bec0252a0223e45571f56dc49c240366df99852) | Fixed issue where the cwd is not writable during bundling by [@Jarred-Sumner](https://github.com/Jarred-Sumner) |
| [`b76974a`](https://github.com/oven-sh/bun/commit/b76974a2a8a794db41b72e174b86d8536793f8e6) | Fixed bug where `IncomingMessage.socket` was not writable by [@Jarred-Sumner](https://github.com/Jarred-Sumner) |
| [`#2785`](https://github.com/oven-sh/bun/pull/2785) | Implemented `node:vm` by [@silversquirl](https://github.com/silversquirl) |
| [`#2962`](https://github.com/oven-sh/bun/pull/2962) | Improved `node-fetch` polyfill to include more exports by [@Jarred-Sumner](https://github.com/Jarred-Sumner) |

---

[#### Bun v0.6.2](https://bun.com/blog/bun-v0.6.2)[#### Bun v0.6.4](https://bun.com/blog/bun-v0.6.4)