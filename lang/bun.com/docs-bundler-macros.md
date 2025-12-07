---
url: https://bun.com/docs/bundler/macros
title: Macros - Bun
source_domain: bun.com
---

# Macros - Bun

Macros are a mechanism for running JavaScript functions at bundle-time. The value returned from these functions are directly inlined into your bundle.
As a toy example, consider this simple function that returns a random number.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)random.ts

Copy

```
export function random() {
  return Math.random();
}
```

This is just a regular function in a regular file, but we can use it as a macro like so:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)cli.tsx

Copy

```
import { random } from "./random.ts" with { type: "macro" };

console.log(`Your random number is ${random()}`);
```

Macros are indicated using import attribute syntax. If you haven’t seen this syntax before, it’s a Stage 3 TC39
proposal that lets you attach additional metadata to import statements.

Now we’ll bundle this file with `bun build`. The bundled file will be printed to stdout.

terminal

Copy

```
bun build ./cli.tsx
```

Copy

```
console.log(`Your random number is ${0.6805550949689833}`);
```

As you can see, the source code of the `random` function occurs nowhere in the bundle. Instead, it is executed during bundling and function call (`random()`) is replaced with the result of the function. Since the source code will never be included in the bundle, macros can safely perform privileged operations like reading from a database.

## [​](https://bun.com/docs/bundler/macros#when-to-use-macros) When to use macros

If you have several build scripts for small things where you would otherwise have a one-off build script, bundle-time code execution can be easier to maintain. It lives with the rest of your code, it runs with the rest of the build, it is automatically parallelized, and if it fails, the build fails too.
If you find yourself running a lot of code at bundle-time though, consider running a server instead.

## [​](https://bun.com/docs/bundler/macros#import-attributes) Import attributes

Bun Macros are import statements annotated using either:

* `with { type: 'macro' }` — an import attribute, a Stage 3 ECMA Script proposal
* `assert { type: 'macro' }` — an import assertion, an earlier incarnation of import attributes that has now been abandoned (but is already supported by a number of browsers and runtimes)

## [​](https://bun.com/docs/bundler/macros#security-considerations) Security considerations

Macros must explicitly be imported with `{ type: "macro" }` in order to be executed at bundle-time. These imports have no effect if they are not called, unlike regular JavaScript imports which may have side effects.
You can disable macros entirely by passing the `--no-macros` flag to Bun. It produces a build error like this:

Copy

```
error: Macros are disabled

foo();
^
./hello.js:3:1 53
```

To reduce the potential attack surface for malicious packages, macros cannot be invoked from inside `node_modules/**/*`. If a package attempts to invoke a macro, you’ll see an error like this:

Copy

```
error: For security reasons, macros cannot be run from node_modules.

beEvil();
^
node_modules/evil/index.js:3:1 50
```

Your application code can still import macros from `node_modules` and invoke them.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)cli.tsx

Copy

```
import { macro } from "some-package" with { type: "macro" };

macro();
```

## [​](https://bun.com/docs/bundler/macros#export-condition-“macro”) Export condition “macro”

When shipping a library containing a macro to npm or another package registry, use the `"macro"` export condition to provide a special version of your package exclusively for the macro environment.

package.json

Copy

```
{
  "name": "my-package",
  "exports": {
    "import": "./index.js",
    "require": "./index.js",
    "default": "./index.js",
    "macro": "./index.macro.js"
  }
}
```

With this configuration, users can consume your package at runtime or at bundle-time using the same import specifier:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
import pkg from "my-package"; // runtime import
import { macro } from "my-package" with { type: "macro" }; // macro import
```

The first import will resolve to `./node_modules/my-package/index.js`, while the second will be resolved by Bun’s bundler to `./node_modules/my-package/index.macro.js`.

## [​](https://bun.com/docs/bundler/macros#execution) Execution

When Bun’s transpiler sees a macro import, it calls the function inside the transpiler using Bun’s JavaScript runtime and converts the return value from JavaScript into an AST node. These JavaScript functions are called at bundle-time, not runtime.
Macros are executed synchronously in the transpiler during the visiting phase—before plugins and before the transpiler generates the AST. They are executed in the order they are imported. The transpiler will wait for the macro to finish executing before continuing. The transpiler will also await any Promise returned by a macro.
Bun’s bundler is multi-threaded. As such, macros execute in parallel inside of multiple spawned JavaScript “workers”.

## [​](https://bun.com/docs/bundler/macros#dead-code-elimination) Dead code elimination

The bundler performs dead code elimination after running and inlining macros. So given the following macro:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)returnFalse.ts

Copy

```
export function returnFalse() {
  return false;
}
```

…then bundling the following file will produce an empty bundle, provided that the minify syntax option is enabled.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
import { returnFalse } from "./returnFalse.ts" with { type: "macro" };

if (returnFalse()) {
  console.log("This code is eliminated");
}
```

## [​](https://bun.com/docs/bundler/macros#serializability) Serializability

Bun’s transpiler needs to be able to serialize the result of the macro so it can be inlined into the AST. All JSON-compatible data structures are supported:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)macro.ts

Copy

```
export function getObject() {
  return {
    foo: "bar",
    baz: 123,
    array: [1, 2, { nested: "value" }],
  };
}
```

Macros can be async, or return Promise instances. Bun’s transpiler will automatically await the Promise and inline the result.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)macro.ts

Copy

```
export async function getText() {
  return "async value";
}
```

The transpiler implements special logic for serializing common data formats like `Response`, `Blob`, `TypedArray`.

* **TypedArray**: Resolves to a base64-encoded string.
* **Response**: Bun will read the `Content-Type` and serialize accordingly; for instance, a Response with type `application/json` will be automatically parsed into an object and `text/plain` will be inlined as a string. Responses with an unrecognized or undefined type will be base-64 encoded.
* **Blob**: As with Response, the serialization depends on the `type` property.

The result of `fetch` is `Promise<Response>`, so it can be directly returned.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)macro.ts

Copy

```
export function getObject() {
  return fetch("https://bun.com");
}
```

Functions and instances of most classes (except those mentioned above) are not serializable.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)macro.ts

Copy

```
export function getText(url: string) {
  // this doesn't work!
  return () => {};
}
```

## [​](https://bun.com/docs/bundler/macros#arguments) Arguments

Macros can accept inputs, but only in limited cases. The value must be statically known. For example, the following is not allowed:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
import { getText } from "./getText.ts" with { type: "macro" };

export function howLong() {
  // the value of `foo` cannot be statically known
  const foo = Math.random() ? "foo" : "bar";

  const text = getText(`https://example.com/${foo}`);
  console.log("The page is ", text.length, " characters long");
}
```

However, if the value of `foo` is known at bundle-time (say, if it’s a constant or the result of another macro) then it’s allowed:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
import { getText } from "./getText.ts" with { type: "macro" };
import { getFoo } from "./getFoo.ts" with { type: "macro" };

export function howLong() {
  // this works because getFoo() is statically known
  const foo = getFoo();
  const text = getText(`https://example.com/${foo}`);
  console.log("The page is", text.length, "characters long");
}
```

This outputs:

Copy

```
function howLong() {
  console.log("The page is", 1322, "characters long");
}
export { howLong };
```

## [​](https://bun.com/docs/bundler/macros#examples) Examples

### [​](https://bun.com/docs/bundler/macros#embed-latest-git-commit-hash) Embed latest git commit hash

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)getGitCommitHash.ts

Copy

```
export function getGitCommitHash() {
  const { stdout } = Bun.spawnSync({
    cmd: ["git", "rev-parse", "HEAD"],
    stdout: "pipe",
  });

  return stdout.toString();
}
```

When we build it, the `getGitCommitHash` is replaced with the result of calling the function:

Copy

```
import { getGitCommitHash } from "./getGitCommitHash.ts" with { type: "macro" };

console.log(`The current Git commit hash is ${getGitCommitHash()}`);
```

You’re probably thinking “Why not just use `process.env.GIT_COMMIT_HASH`?” Well, you can do that too. But can you do
this with an environment variable?

### [​](https://bun.com/docs/bundler/macros#make-fetch-requests-at-bundle-time) Make fetch() requests at bundle-time

In this example, we make an outgoing HTTP request using `fetch()`, parse the HTML response using `HTMLRewriter`, and return an object containing the title and meta tags–all at bundle-time.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)meta.ts

Copy

```
export async function extractMetaTags(url: string) {
  const response = await fetch(url);
  const meta = {
    title: "",
  };
  new HTMLRewriter()
    .on("title", {
      text(element) {
        meta.title += element.text;
      },
    })
    .on("meta", {
      element(element) {
        const name =
          element.getAttribute("name") || element.getAttribute("property") || element.getAttribute("itemprop");

        if (name) meta[name] = element.getAttribute("content");
      },
    })
    .transform(response);

  return meta;
}
```

The `extractMetaTags` function is erased at bundle-time and replaced with the result of the function call. This means that the fetch request happens at bundle-time, and the result is embedded in the bundle. Also, the branch throwing the error is eliminated since it’s unreachable.

Copy

```
import { extractMetaTags } from "./meta.ts" with { type: "macro" };

export const Head = () => {
  const headTags = extractMetaTags("https://example.com");

  if (headTags.title !== "Example Domain") {
    throw new Error("Expected title to be 'Example Domain'");
  }

  return (
    <head>
      <title>{headTags.title}</title>
      <meta name="viewport" content={headTags.viewport} />
    </head>
  );
};
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/bundler/macros.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /bundler/macros)

⌘I