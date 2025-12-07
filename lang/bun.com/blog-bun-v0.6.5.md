---
url: https://bun.com/blog/bun-v0.6.5
title: Bun v0.6.5 | Bun Blog
source_domain: bun.com
---

# Bun v0.6.5 | Bun Blog

# Bun v0.6.5

---

[Jarred Sumner](https://twitter.com/jarredsumner) · May 29, 2023

We're hiring C/C++ and Zig engineers to build the future of JavaScript! [Join our team →](https://bun.com/careers)

Last week, we launched our new JavaScript [bundler](https://bun.com/blog/bun-bundler) in Bun [v0.6.0](https://bun.com/blog/bun-v0.6.0).

Today, we are introducing native runtime support for CommonJS, smarter CommonJS -> ES Module conversion in `Bun.build()`, `$npm_lifecycle_event` in bun run, a bugfix for Bun.serve() with streaming files, a bugfix for `createConnection` (in `node:net`) and more

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

## [Native CommonJS runtime support](https://bun.com/blog/bun-v0.6.5#native-commonjs-runtime-support)

We've reimplemented CommonJS support in Bun from being transpiler-only into natively supported in the runtime. This fixes many bugs that blocked npm packages from working in Bun, and improves compatibility with Node.js.

Here are 3 packages this unblocks:

### [Vue](https://bun.com/blog/bun-v0.6.5#vue)

Previously, importing Vue would report a missing export error. Thanks to native CommonJS support, Vue now works out of the box.

In Bun v0.6.5:

output

input.js

output

```
3.3.4
```

input.js

```
import {version} from "vue";
console.log(version);
```

In Bun v0.6.4 and earlier:

```
import {version} from "vue";
console.log(version);

> SyntaxError: Import named 'version' not found in module './node_modules/vue/index.mjs'.
```

### [Winston logger](https://bun.com/blog/bun-v0.6.5#winston-logger)

Previously, Bun would throw an error when trying to use Winston logger. Now, it works out of the box.

In Bun v0.6.5:

output

input.js

output

```
info: What time is the testing at? {"service":"user-service"}
```

input.js

```
import winston from "winston";

const logger = winston.createLogger({
  level: "info",
  format: winston.format.json(),
  defaultMeta: { service: "user-service" },
  transports: [
    //
    // - Write all logs with importance level of `error` or less to `error.log`
    // - Write all logs with importance level of `info` or less to `combined.log`
    //
    new winston.transports.File({ filename: "error.log", level: "error" }),
    new winston.transports.File({ filename: "combined.log" }),
  ],
});

//
// If we're not in production then log to the `console` with the format:
// `${info.level}: ${info.message} JSON.stringify({ ...rest }) `
//
logger.add(
  new winston.transports.Console({
    format: winston.format.simple(),
  })
);

logger.log({
  level: "info",
  message: "What time is the testing at?",
});
```

In Bun v0.6.4 and earlier:

```
1 | import winston from "winston";
2 |
3 | winston.format.json();
   ^
TypeError: undefined is not an object (evaluating 'winston.format.json')
      input.js:3:0
```

### [Viem](https://bun.com/blog/bun-v0.6.5#viem)

Previously, importing `"viem"` would throw `ReferenceError`. Thanks to native CommonJS support, viem now loads as expected.

In Bun v0.6.5

output

input.js

output

```
[Function: createClient]
```

input.js

```
import { createClient } from "viem";
console.log(createClient);
```

In Bun v0.6.4 and earlier:

```
11 |   if (param.type.startsWith("tuple"))
12 |     return `(${formatAbiParams(param.components, { includeName })})${param.type.slice(5)}`;
13 |   return param.type + (includeName && param.name ? ` ${param.name}` : "");
14 | };
15 |
16 | var {InvalidDefinitionTypeError} = import.meta.require("viem/dist/esm/errors/abi.js");
   ^
ReferenceError: Cannot access uninitialized variable.
        input.js:16:0
```

### [What changed specifically?](https://bun.com/blog/bun-v0.6.5#what-changed-specifically)

Previously Bun would transpile CommonJS modules into ES Modules shaped like this:

```
// Bun v0.6.4 and earlier wrapper:
import { cjs2ESM } from "bun:wrap";
export default cjs2ESM((module, exports) => {
  /* ...code */
});
```

Separately, all `import` of these modules were rewritten to check if it was a CommonJS module, and if so, call the function and return the CommonJS exports instead of the ES Module exports.

That step was buggy. We don't always know if a module is CommonJS until we've parsed the source code. `package.json` has some hints, but it also lies a lot.

In Node.js, statically-known CommonJS exports become named ES Module exports. For example, `module.exports = { a: 'b' }` becomes `export const a = 'b'`. We neglected to do this in Bun and instead used the transpiler to rewrite usages of CommonJS modules to use the `module.exports` directly. That approach didn't handle `export * from` or `export * as` correctly. And sometimes we failed to detect a CommonJS module (or incorrectly assumed an ES Module was CommonJS).

So we re-implemented how all that works from scratch.

Now, when Bun's JavaScript runtime detects a CommonJS module:

1. Wrap the module in a function that takes `module` and `exports` as arguments.

```
(function (module, exports, require) {
  /* ...code */
})(module, exports, require);
```

1. Evaluate the generated function
2. Append the properties of `exports` as named ES Module exports.

This means that `export * from '...'` and `export * as ...` work as expected. Also, packages that rely on "sloppy mode" features like `with` and implicit global variable assignment are now supported in Bun. As before, you can continue to use `import` and `require` in ES Modules.

## [Smarter CommonJS -> ESM conversion in the bundler](https://bun.com/blog/bun-v0.6.5#smarter-commonjs-esm-conversion-in-the-bundler)

Unrelated to the runtime CommonJS changes, we've also made `Bun.build()` smarter about converting from CommonJS modules into ES Modules.

> In the next version of Bun  
>   
> CommonJS -> ESM conversion in "bun build" gets a little smarter.   
>   
> It handles "module.exports = { a: 'b' }" now [pic.twitter.com/6wv23buf1t](https://t.co/6wv23buf1t)
>
> — Jarred Sumner (@jarredsumner) [May 28, 2023](https://twitter.com/jarredsumner/status/1662943256353837059?ref_src=twsrc%5Etfw)

## [$npm\_lifecycle\_event in bun run](https://bun.com/blog/bun-v0.6.5#npm-lifecycle-event-in-bun-run)

You can now access `$npm_lifecycle_event` in `bun run` scripts. The `$npm_lifecycle_event` environment variable is set to the name of the script that was run. This is useful for detecting which package.json script was run.

output

input.js

output

```
bun run hey
```

```
hey
```

input.js

```
console.log(process.env.npm_lifecycle_event);
```

Thanks to [@TiranexDev](https://github.com/TiranexDev) for this contribution!

## [Bugfix for Bun.serve() with streaming files](https://bun.com/blog/bun-v0.6.5#bugfix-for-bun-serve-with-streaming-files)

Bun now globally ignores `SIGPIPE` signals, which fixes a bug where Bun could crash when using `new Response(Bun.file(path))` to stream files on Linux when the client disconnects early.

## [Bugfix for `createConnection` in `node:net`](https://bun.com/blog/bun-v0.6.5#bugfix-for-createconnection-in-node-net)

This fixes an arguments parsing issue in `node:net` that caused `createConnection` to fail in some cases. Thanks to [@cirospaciari](https://github.com/cirospaciari) for this contribution!

## [Transpiler & bundler bugfix](https://bun.com/blog/bun-v0.6.5#transpiler-bundler-bugfix)

Bun was incorrectly transpiling `Symbol["for"]` and a few dozen other global side-effect free getters accessed via statically-known computed property string literal to `undefined`. This has been fixed. This bug was introduced in Bun v0.6.0, and began impacting Bun's JavaScript runtime in v0.6.4. Thanks to [@zloirock](https://github.com/zloirock) for reporting this issue.

---

[#### Bun v0.6.4](https://bun.com/blog/bun-v0.6.4)[#### Bun v0.6.6](https://bun.com/blog/bun-v0.6.6)