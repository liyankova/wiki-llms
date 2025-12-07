---
url: https://bun.com/blog/commonjs-is-not-going-away
title: CommonJS is not going away | Bun Blog
source_domain: bun.com
---

# CommonJS is not going away | Bun Blog

# CommonJS is not going away

---

[Jarred Sumner](https://twitter.com/jarredsumner) · June 30, 2023

We're hiring C/C++ and Zig engineers to build the future of JavaScript! [Join our team →](https://bun.com/careers)

Some may be surprised to see the [recent](https://bun.sh/blog/bun-v0.6.5) [release](https://bun.sh/blog/bun-v0.6.10) [notes](https://bun.sh/blog/bun-v0.6.12) for Bun mention CommonJS support. After all, CommonJS is a legacy module system, and the future of JavaScript is ES Modules (ESM), right? As a "forward-thinking" "next-gen" runtime, why would Bun put so much effort into improving CommonJS support?

> The latest about ESM on npm: ESM is now at 9%, dual at 3.8, faux ESM at 13.7%, and CJS at 73.6%.  
>   
> This data includes only the most popular npm packages (1m+ downloads per week and/or 500+ others depend on it), excluding the TypeScript types/\* packages. [pic.twitter.com/kdZg5tM9N6](https://t.co/kdZg5tM9N6)
>
> — Titus 🇵🇸 (@wooorm) [November 5, 2022](https://twitter.com/wooorm/status/1588905279206621184?ref_src=twsrc%5Etfw)

Because CommonJS is here to stay, and that's okay! We think that better tooling can solve today's developer experience issues with CommonJS and ESM interop.

## [The situation, explained](https://bun.com/blog/commonjs-is-not-going-away#the-situation-explained)

As you might imagine, it's often desirable to split your application into multiple files. When you do this, you need a way to reference code in other files.

The *CommonJS* module format was developed in 2009 and popularized by Node.js. Files can assign properties to a special variable called `exports`. Then, other files can reference properties from the `exports` object by "requiring" the file with a special `require` function.

a.js

b.js

a.js

```
const b = require("./b.js");

b.sayHi(); // prints "hi"
```

b.js

```
exports.sayHi = () => {
  console.log("hi");
};
```

To overly simplify how this works: when a file is `require`d, the file is *executed* and the properties of the `exports` object are made available to the importer. CommonJS is designed for server-side JavaScript (in fact, it was originally named *ServerJS*), where it's expected that all files are available on the local filesystem. This is what it means for CommonJS to be *synchronous* — you can conceptualize `require()` as a "blocking" operation that reads the imported file and runs it, then hands control back to the importer.

ECMAScript modules were introduced in 2015 as part of ES6. An ES module declares its exports with the `export` keyword. The `import` keyword is used to import from other files. Unlike `exports/require`, both `import` and `export` statements can only occur at the *top level* of a file.

a.js

b.js

a.js

```
import { sayHi } from "./b.js"

sayHi(); // prints "hi"
```

b.js

```
export const sayHi = () => {
  console.log("hi");
};
```

Because ES modules are designed to work in browsers, it's expected that files are loaded over the network. This is what it means for ES modules to be *asynchronous*. Given an ES module, a browser can see what it imports and exports *without running the file*. Commonly, the entire module graph will be resolved (which may potentially involve multiple round-trip network requests) before any code is executed.

## [The case for CommonJS](https://bun.com/blog/commonjs-is-not-going-away#the-case-for-commonjs)

### [CommonJS starts faster](https://bun.com/blog/commonjs-is-not-going-away#commonjs-starts-faster)

ES modules are slower for larger applications. Unlike require, you either need load the entire module graph when using statements or await each import with expressions. For example, if you want to lazy-load a package for use in a function, your code *must* return a promise (which can introduce additional microticks and overhead).

```
async function transpileEsm(code) {
  const { transform } = await import("@babel/core");
  // ... return must be a Promise
}

function transpileCjs(code) {
  const { transform } = require("@babel/core");
  // ... return is sync
}
```

ES Modules are slower by design. They need two passes in order to bind imports to exports. The entire module graph gets parsed and analyzed, *then* the code gets evaluated. This is split into distinct steps. It's what makes "live bindings" in ES Modules possible.

Consider these two simple files.

babel.cjs

babel.mjs

babel.cjs

```
require("@babel/core")
```

babel.mjs

```
import "@babel/core";
```

Babel is a package that consists of a huge number of files, so comparing the runtime of these two files is a decent way to evaluate performance costs associated with module resolution. The results:

[![](https://github.com/oven-sh/bun/assets/3084745/87414629-c433-4141-ba19-08a9d4451196)](https://github.com/oven-sh/bun/assets/3084745/87414629-c433-4141-ba19-08a9d4451196)

With Bun, loading Babel with CommonJS is roughly 2.4x faster than with ES modules.

There's a difference of 85ms. In the context of serverless cold starts, that is massive. With Node.js the difference was 1.8x (~60ms).

### [Incremental loading](https://bun.com/blog/commonjs-is-not-going-away#incremental-loading)

CommonJS allows for dynamic module loading—you can `require()` a file conditionally, or `require()` a dynamically constructed path/specifier, or `require()` in the body of a function. This flexibility can be advantageous in scenarios where dynamic loading is required, such as plugin systems or lazy-loading specific components based on user interactions.

ES modules provide a dynamic `import()` function with similar properties. In some sense, its existence is a testament to the fact that the CommonJS's dynamic approach has utility and is valued by developers.

### [It's already here](https://bun.com/blog/commonjs-is-not-going-away#it-s-already-here)

Millions of modules published to npm already use CommonJS. Many of these are both: (a) are no longer actively maintained, and (b) are critically important to existing projects. We will never hit a point where *all* packages can be expected to use ES modules. A runtime or framework that doesn't support CommonJS is leaving a huge amount of value on the table.

## [CommonJS in Bun](https://bun.com/blog/commonjs-is-not-going-away#commonjs-in-bun)

As of Bun v0.6.5, the Bun runtime natively implements CommonJS. Previously, Bun transpiled CommonJS files to a special "synchronous ESM" format.

### [Importing CommonJS from ESM](https://bun.com/blog/commonjs-is-not-going-away#importing-commonjs-from-esm)

You can `import` or `require` CommonJS modules from ESM modules.

```
import { stuff } from "./my-commonjs.cjs";
import Stuff from "./my-commonjs.cjs";
const myStuff = require("./my-commonjs.cjs");
```

Recently, Bun also added support for the [`__esModule` annotation](https://github.com/oven-sh/bun/pull/3393).

module.js

```
exports.__esModule = true;
exports.default = 5;
exports.foo = "foo";
```

This is a de-facto mechanism for a CommonJS module to indicate (in conjunction with `"type": "module"` in `package.json`) that `exports.default` should be interpreted as the *default export*. When `__esModule` is set in a CommonJS module, a *default `import`* (`import a from "./a.js"`) will import the `exports.default` property. Without the annotation, a default import will import the entire `exports` object.

With the annotation:

```
// with __esModule: true
import mod, { foo } from "./module.js";
mod; // 5
foo; // "foo"
```

Without the annotation:

```
// without __esModule
import mod, { foo } from "./module.js";
mod; // { default: 5 }
mod.default; // 5
foo; // "foo"
```

This is a de-facto standard way for a CommonJS module to indicate that `exports.default` should be interpreted as the *default export*.

## [In summary](https://bun.com/blog/commonjs-is-not-going-away#in-summary)

CommonJS is already here to stay. Not only that, it has real reasons to exist. We love ES modules here at Bun, but pragmatism is important. CommonJS is not a relic of a bygone era, and Bun treats it as a first-class citizen today.