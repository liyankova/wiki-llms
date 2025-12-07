---
url: https://bun.com/docs/bundler
title: Bundler - Bun
source_domain: bun.com
---

# Bundler - Bun

Bun’s fast native bundler can be used via the `bun build` CLI command or the `Bun.build()` JavaScript API.

### [​](https://bun.com/docs/bundler#at-a-glance) At a Glance

* JS API: `await Bun.build({ entrypoints, outdir })`
* CLI: `bun build <entry> --outdir ./out`
* Watch: `--watch` for incremental rebuilds
* Targets: `--target browser|bun|node`
* Formats: `--format esm|cjs|iife` (experimental for cjs/iife)

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.tsx'],
  outdir: './build',
});
```

It’s fast. The numbers below represent performance on esbuild’s [three.js benchmark](https://github.com/oven-sh/bun/tree/main/bench/bundle).

![](https://mintcdn.com/bun-1dd33a4e/PY1574V41bdK8wNs/images/bundler-speed.png?fit=max&auto=format&n=PY1574V41bdK8wNs&q=85&s=0a549e542fceb7d51f84976fe1d151e4)

## [​](https://bun.com/docs/bundler#why-bundle) Why bundle?

The bundler is a key piece of infrastructure in the JavaScript ecosystem. As a brief overview of why bundling is so important:

* **Reducing HTTP requests.** A single package in `node_modules` may consist of hundreds of files, and large applications may have dozens of such dependencies. Loading each of these files with a separate HTTP request becomes untenable very quickly, so bundlers are used to convert our application source code into a smaller number of self-contained “bundles” that can be loaded with a single request.
* **Code transforms.** Modern apps are commonly built with languages or tools like TypeScript, JSX, and CSS modules, all of which must be converted into plain JavaScript and CSS before they can be consumed by a browser. The bundler is the natural place to configure these transformations.
* **Framework features.** Frameworks rely on bundler plugins & code transformations to implement common patterns like file-system routing, client-server code co-location (think `getServerSideProps` or Remix loaders), and server components.
* **Full-stack Applications.** Bun’s bundler can handle both server and client code in a single command, enabling optimized production builds and single-file executables. With build-time HTML imports, you can bundle your entire application — frontend assets and backend server — into a single deployable unit.

Let’s jump into the bundler API.

The Bun bundler is not intended to replace `tsc` for typechecking or generating type declarations.

## [​](https://bun.com/docs/bundler#basic-example) Basic example

Let’s build our first bundle. You have the following two files, which implement a simple client-side rendered React app.

Copy

```
import * as ReactDOM from "react-dom/client";
import { Component } from "./Component";

const root = ReactDOM.createRoot(document.getElementById("root")!);
root.render(<Component message="Sup!" />);
```

Here, `index.tsx` is the “entrypoint” to our application. Commonly, this will be a script that performs some side effect, like starting a server or—in this case—initializing a React root. Because we’re using TypeScript & JSX, we need to bundle our code before it can be sent to the browser.
To create our bundle:

Copy

```
await Bun.build({
  entrypoints: ["./index.tsx"],
  outdir: "./out",
});
```

For each file specified in `entrypoints`, Bun will generate a new bundle. This bundle will be written to disk in the `./out` directory (as resolved from the current working directory). After running the build, the file system looks like this:

file system

Copy

```
.
├── index.tsx
├── Component.tsx
└── out
    └── index.js
```

The contents of `out/index.js` will look something like this:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/javascript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=81efd0ad0d779debfa163bfd906ef6a6](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/javascript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=81efd0ad0d779debfa163bfd906ef6a6)out/index.js

Copy

```
// out/index.js
// ...
// ~20k lines of code
// including the contents of `react-dom/client` and all its dependencies
// this is where the $jsxDEV and $createRoot functions are defined

// Component.tsx
function Component(props) {
  return $jsxDEV(
    "p",
    {
      children: props.message,
    },
    undefined,
    false,
    undefined,
    this,
  );
}

// index.tsx
var rootNode = document.getElementById("root");
var root = $createRoot(rootNode);
root.render(
  $jsxDEV(
    Component,
    {
      message: "Sup!",
    },
    undefined,
    false,
    undefined,
    this,
  ),
);
```

## [​](https://bun.com/docs/bundler#watch-mode) Watch mode

Like the runtime and test runner, the bundler supports watch mode natively.

terminal

Copy

```
bun build ./index.tsx --outdir ./out --watch
```

## [​](https://bun.com/docs/bundler#content-types) Content types

Like the Bun runtime, the bundler supports an array of file types out of the box. The following table breaks down the bundler’s set of standard “loaders”. Refer to [Bundler > File types](https://bun.com/docs/bundler/loaders) for full documentation.

| Extensions | Details |
| --- | --- |
| `.js` `.jsx` `.cjs` `.mjs` `.mts` `.cts` `.ts` `.tsx` | Uses Bun’s built-in transpiler to parse the file and transpile TypeScript/JSX syntax to vanilla JavaScript. The bundler executes a set of default transforms including dead code elimination and tree shaking. At the moment Bun does not attempt to down-convert syntax; if you use recently ECMAScript syntax, that will be reflected in the bundled code. |
| `.json` | JSON files are parsed and inlined into the bundle as a JavaScript object.  `js<br/>import pkg from "./package.json";<br/>pkg.name; // => "my-package"<br/>` |
| `.jsonc` | JSON with comments. Files are parsed and inlined into the bundle as a JavaScript object.  `js<br/>import config from "./config.jsonc";<br/>config.name; // => "my-config"<br/>` |
| `.toml` | TOML files are parsed and inlined into the bundle as a JavaScript object.  `js<br/>import config from "./bunfig.toml";<br/>config.logLevel; // => "debug"<br/>` |
| `.yaml` `.yml` | YAML files are parsed and inlined into the bundle as a JavaScript object.  `js<br/>import config from "./config.yaml";<br/>config.name; // => "my-app"<br/>` |
| `.txt` | The contents of the text file are read and inlined into the bundle as a string.  `js<br/>import contents from "./file.txt";<br/>console.log(contents); // => "Hello, world!"<br/>` |
| `.html` | HTML files are processed and any referenced assets (scripts, stylesheets, images) are bundled. |
| `.css` | CSS files are bundled together into a single `.css` file in the output directory. |
| `.node` `.wasm` | These files are supported by the Bun runtime, but during bundling they are treated as assets. |

### [​](https://bun.com/docs/bundler#assets) Assets

If the bundler encounters an import with an unrecognized extension, it treats the imported file as an external file. The referenced file is copied as-is into `outdir`, and the import is resolved as a path to the file.

Copy

```
// bundle entrypoint
import logo from "./logo.svg";
console.log(logo);
```

The exact behavior of the file loader is also impacted by [`naming`](https://bun.com/docs/bundler#naming) and [`publicPath`](https://bun.com/docs/bundler#publicpath).

Refer to the [Bundler > Loaders](https://bun.com/docs/bundler/loaders) page for more complete documentation on the file loader.

### [​](https://bun.com/docs/bundler#plugins) Plugins

The behavior described in this table can be overridden or extended with plugins. Refer to the [Bundler > Loaders](https://bun.com/docs/bundler/loaders) page for complete documentation.

## [​](https://bun.com/docs/bundler#api) API

### [​](https://bun.com/docs/bundler#entrypoints) entrypoints

Required
An array of paths corresponding to the entrypoints of our application. One bundle will be generated for each entrypoint.

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
const result = await Bun.build({
  entrypoints: ["./index.ts"],
});
// => { success: boolean, outputs: BuildArtifact[], logs: BuildMessage[] }
```

### [​](https://bun.com/docs/bundler#outdir) outdir

The directory where output files will be written.

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
const result = await Bun.build({
  entrypoints: ['./index.ts'],
  outdir: './out'
});
// => { success: boolean, outputs: BuildArtifact[], logs: BuildMessage[] }
```

If `outdir` is not passed to the JavaScript API, bundled code will not be written to disk. Bundled files are returned in an array of `BuildArtifact` objects. These objects are Blobs with extra properties; see [Outputs](https://bun.com/docs/bundler#outputs) for complete documentation.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
const result = await Bun.build({
  entrypoints: ["./index.ts"],
});

for (const res of result.outputs) {
  // Can be consumed as blobs
  await res.text();

  // Bun will set Content-Type and Etag headers
  new Response(res);

  // Can be written manually, but you should use `outdir` in this case.
  Bun.write(path.join("out", res.path), res);
}
```

When `outdir` is set, the `path` property on a `BuildArtifact` will be the absolute path to where it was written to.

### [​](https://bun.com/docs/bundler#target) target

The intended execution environment for the bundle.

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.ts'],
  outdir: './out',
  target: 'browser', // default
})
```

Depending on the target, Bun will apply different module resolution rules and optimizations.

## browser

**Default.** For generating bundles that are intended for execution by a browser. Prioritizes the `"browser"` export
condition when resolving imports. Importing any built-in modules, like `node:events` or `node:path` will work, but
calling some functions, like `fs.readFile` will not work.

## bun

For generating bundles that are intended to be run by the Bun runtime. In many cases, it isn’t necessary to bundle server-side code; you can directly execute the source code without modification. However, bundling your server code can reduce startup times and improve running performance. This is the target to use for building full-stack applications with build-time HTML imports, where both server and client code are bundled together.All bundles generated with `target: "bun"` are marked with a special `// @bun` pragma, which indicates to the Bun runtime that there’s no need to re-transpile the file before execution.If any entrypoints contains a Bun shebang (`#!/usr/bin/env bun`) the bundler will default to `target: "bun"` instead of `"browser"`.When using `target: "bun"` and `format: "cjs"` together, the `// @bun @bun-cjs` pragma is added and the CommonJS wrapper function is not compatible with Node.js.

## node

For generating bundles that are intended to be run by Node.js. Prioritizes the `"node"` export condition when
resolving imports, and outputs `.mjs`. In the future, this will automatically polyfill the Bun global and other
built-in `bun:*` modules, though this is not yet implemented.

### [​](https://bun.com/docs/bundler#format) format

Specifies the module format to be used in the generated bundles.
Bun defaults to `"esm"`, and provides experimental support for `"cjs"` and `"iife"`.

#### [​](https://bun.com/docs/bundler#format:-“esm”-es-module) format: “esm” - ES Module

This is the default format, which supports ES Module syntax including top-level await, `import.meta`, and more.

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.tsx'],
  outdir: './out',
  format: "esm",
})
```

To use ES Module syntax in browsers, set `format` to `"esm"` and make sure your `<script type="module">` tag has `type="module"` set.

#### [​](https://bun.com/docs/bundler#format:-“cjs”-commonjs) format: “cjs” - CommonJS

To build a CommonJS module, set `format` to `"cjs"`. When choosing `"cjs"`, the default target changes from `"browser"` (esm) to `"node"` (cjs). CommonJS modules transpiled with `format: "cjs"`, `target: "node"` can be executed in both Bun and Node.js (assuming the APIs in use are supported by both).

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.tsx'],
  outdir: './out',
  format: "cjs",
})
```

#### [​](https://bun.com/docs/bundler#format:-“iife”-iife) format: “iife” - IIFE

TODO: document IIFE once we support globalNames.

### [​](https://bun.com/docs/bundler#jsx) `jsx`

Configure JSX transform behavior. Allows fine-grained control over how JSX is compiled.
**Classic runtime example** (uses `factory` and `fragment`):

Copy

```
await Bun.build({
  entrypoints: ["./app.tsx"],
  outdir: "./out",
  jsx: {
    factory: "h",
    fragment: "Fragment",
    runtime: "classic",
  },
});
```

**Automatic runtime example** (uses `importSource`):

Copy

```
await Bun.build({
  entrypoints: ["./app.tsx"],
  outdir: "./out",
  jsx: {
    importSource: "preact",
    runtime: "automatic",
  },
});
```

### [​](https://bun.com/docs/bundler#splitting) splitting

Whether to enable code splitting.

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.tsx'],
  outdir: './out',
  splitting: false, // default
})
```

When `true`, the bundler will enable code splitting. When multiple entrypoints both import the same file, module, or set of files/modules, it’s often useful to split the shared code into a separate bundle. This shared bundle is known as a chunk. Consider the following files:

Copy

```
import { shared } from "./shared.ts";
```

To bundle `entry-a.ts` and `entry-b.ts` with code-splitting enabled:

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./entry-a.ts', './entry-b.ts'],
  outdir: './out',
  splitting: true,
})
```

Running this build will result in the following files:

file system

Copy

```
.
├── entry-a.tsx
├── entry-b.tsx
├── shared.tsx
└── out
    ├── entry-a.js
    ├── entry-b.js
    └── chunk-2fce6291bf86559d.js
```

The generated `chunk-2fce6291bf86559d.js` file contains the shared code. To avoid collisions, the file name automatically includes a content hash by default. This can be customized with [`naming`](https://bun.com/docs/bundler#naming).

### [​](https://bun.com/docs/bundler#plugins-2) plugins

A list of plugins to use during bundling.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ["./index.tsx"],
  outdir: "./out",
  plugins: [
    /* ... */
  ],
});
```

Bun implements a universal plugin system for both Bun’s runtime and bundler. Refer to the [plugin documentation](https://bun.com/docs/bundler/plugins) for complete documentation.

### [​](https://bun.com/docs/bundler#env) env

Controls how environment variables are handled during bundling. Internally, this uses `define` to inject environment variables into the bundle, but makes it easier to specify the environment variables to inject.

#### [​](https://bun.com/docs/bundler#env:-“inline”) env: “inline”

Injects environment variables into the bundled output by converting `process.env.FOO` references to string literals containing the actual environment variable values.

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.tsx'],
  outdir: './out',
  env: "inline",
})
```

For the input below:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/javascript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=81efd0ad0d779debfa163bfd906ef6a6](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/javascript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=81efd0ad0d779debfa163bfd906ef6a6)input.js

Copy

```
// input.js
console.log(process.env.FOO);
console.log(process.env.BAZ);
```

The generated bundle will contain the following code:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/javascript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=81efd0ad0d779debfa163bfd906ef6a6](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/javascript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=81efd0ad0d779debfa163bfd906ef6a6)output.js

Copy

```
// output.js
console.log("bar");
console.log("123");
```

#### [​](https://bun.com/docs/bundler#env:-“public-”-prefix) env: “PUBLIC\_\*” (prefix)

Inlines environment variables matching the given prefix (the part before the `*` character), replacing `process.env.FOO` with the actual environment variable value. This is useful for selectively inlining environment variables for things like public-facing URLs or client-side tokens, without worrying about injecting private credentials into output bundles.

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.tsx'],
  outdir: './out',
  
  // Inline all env vars that start with "ACME_PUBLIC_"
  env: "ACME_PUBLIC_*",
})
```

For example, given the following environment variables:

terminal

Copy

```
FOO=bar BAZ=123 ACME_PUBLIC_URL=https://acme.com
```

And source code:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.tsx

Copy

```
console.log(process.env.FOO);
console.log(process.env.ACME_PUBLIC_URL);
console.log(process.env.BAZ);
```

The generated bundle will contain the following code:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/javascript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=81efd0ad0d779debfa163bfd906ef6a6](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/javascript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=81efd0ad0d779debfa163bfd906ef6a6)output.js

Copy

```
console.log(process.env.FOO);
console.log("https://acme.com");
console.log(process.env.BAZ);
```

#### [​](https://bun.com/docs/bundler#env:-“disable”) env: “disable”

Disables environment variable injection entirely.

### [​](https://bun.com/docs/bundler#sourcemap) sourcemap

Specifies the type of sourcemap to generate.

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.tsx'],
  outdir: './out',
  sourcemap: 'linked', // default 'none'
})
```

| Value | Description |
| --- | --- |
| `"none"` | Default. No sourcemap is generated. |
| `"linked"` | A separate `*.js.map` file is created alongside each `*.js` bundle using a `//# sourceMappingURL` comment to link the two. Requires `--outdir` to be set. The base URL of this can be customized with `--public-path`.  `js<br/>// <bundled code here><br/><br/>//# sourceMappingURL=bundle.js.map<br/>` |
| `"external"` | A separate `*.js.map` file is created alongside each `*.js` bundle without inserting a `//# sourceMappingURL` comment.  Generated bundles contain a debug id that can be used to associate a bundle with its corresponding sourcemap. This `debugId` is added as a comment at the bottom of the file.  `js<br/>// <generated bundle code><br/><br/>//# debugId=<DEBUG ID><br/>` |
| `"inline"` | A sourcemap is generated and appended to the end of the generated bundle as a base64 payload.  `js<br/>// <bundled code here><br/><br/>//# sourceMappingURL=data:application/json;base64,<encoded sourcemap here><br/>` |

The associated `*.js.map` sourcemap will be a JSON file containing an equivalent `debugId` property.

### [​](https://bun.com/docs/bundler#minify) minify

Whether to enable minification. Default `false`.

When targeting `bun`, identifiers will be minified by default.

To enable all minification options:

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.tsx'],
  outdir: './out',
  minify: true, // default false
})
```

To granularly enable certain minifications:

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.tsx'],
  outdir: './out',
  minify: {
    whitespace: true,
    identifiers: true,
    syntax: true,
  },
})
```

### [​](https://bun.com/docs/bundler#external) external

A list of import paths to consider external. Defaults to `[]`.

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.tsx'],
  outdir: './out',
  external: ["lodash", "react"], // default: []
})
```

An external import is one that will not be included in the final bundle. Instead, the import statement will be left as-is, to be resolved at runtime.
For instance, consider the following entrypoint file:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.tsx

Copy

```
import _ from "lodash";
import { z } from "zod";

const value = z.string().parse("Hello world!");
console.log(_.upperCase(value));
```

Normally, bundling `index.tsx` would generate a bundle containing the entire source code of the “zod” package. If instead, we want to leave the import statement as-is, we can mark it as external:

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.tsx'],
  outdir: './out',
  external: ['zod'],
})
```

The generated bundle will look something like this:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/javascript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=81efd0ad0d779debfa163bfd906ef6a6](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/javascript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=81efd0ad0d779debfa163bfd906ef6a6)out/index.js

Copy

```
import { z } from "zod";

// ...
// the contents of the "lodash" package
// including the `_.upperCase` function

var value = z.string().parse("Hello world!");
console.log(_.upperCase(value));
```

To mark all imports as external, use the wildcard `*`:

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.tsx'],
  outdir: './out',
  external: ['*'],
})
```

### [​](https://bun.com/docs/bundler#packages) packages

Control whether package dependencies are included to bundle or not. Possible values: `bundle` (default), `external`. Bun treats any import which path do not start with `.`, `..` or `/` as package.

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.ts'],
  packages: 'external',
})
```

### [​](https://bun.com/docs/bundler#naming) naming

Customizes the generated file names. Defaults to `./[dir]/[name].[ext]`.

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.tsx'],
  outdir: './out',
  naming: "[dir]/[name].[ext]", // default
})
```

By default, the names of the generated bundles are based on the name of the associated entrypoint.

file system

Copy

```
.
├── index.tsx
└── out
    └── index.js
```

With multiple entrypoints, the generated file hierarchy will reflect the directory structure of the entrypoints.

file system

Copy

```
.
├── index.tsx
└── nested
    └── index.tsx
└── out
    ├── index.js
    └── nested
        └── index.js
```

The names and locations of the generated files can be customized with the `naming` field. This field accepts a template string that is used to generate the filenames for all bundles corresponding to entrypoints. where the following tokens are replaced with their corresponding values:

* `[name]` - The name of the entrypoint file, without the extension.
* `[ext]` - The extension of the generated bundle.
* `[hash]` - A hash of the bundle contents.
* `[dir]` - The relative path from the project root to the parent directory of the source file.

For example:

| Token | `[name]` | `[ext]` | `[hash]` | `[dir]` |
| --- | --- | --- | --- | --- |
| `./index.tsx` | `index` | `js` | `a1b2c3d4` | `""` (empty string) |
| `./nested/entry.ts` | `entry` | `js` | `c3d4e5f6` | `"nested"` |

We can combine these tokens to create a template string. For instance, to include the hash in the generated bundle names:

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.tsx'],
  outdir: './out',
  naming: 'files/[dir]/[name]-[hash].[ext]',
})
```

This build would result in the following file structure:

file system

Copy

```
.
├── index.tsx
└── out
    └── files
        └── index-a1b2c3d4.js
```

When a string is provided for the `naming` field, it is used only for bundles that correspond to entrypoints. The names of chunks and copied assets are not affected. Using the JavaScript API, separate template strings can be specified for each type of generated file.

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.tsx'],
  outdir: './out',
  naming: {
    // default values
    entry: '[dir]/[name].[ext]',
    chunk: '[name]-[hash].[ext]',
    asset: '[name]-[hash].[ext]',
  },
})
```

### [​](https://bun.com/docs/bundler#root) root

The root directory of the project.

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./pages/a.tsx', './pages/b.tsx'],
  outdir: './out',
  root: '.',
})
```

If unspecified, it is computed to be the first common ancestor of all entrypoint files. Consider the following file structure:

file system

Copy

```
.
└── pages
  └── index.tsx
  └── settings.tsx
```

We can build both entrypoints in the `pages` directory:

* JavaScript
* CLI

Copy

```
await Bun.build({
  entrypoints: ['./pages/index.tsx', './pages/settings.tsx'],
  outdir: './out',
})
```

This would result in a file structure like this:

file system

Copy

```
.
└── pages
  └── index.tsx
  └── settings.tsx
└── out
  └── index.js
  └── settings.js
```

Since the `pages` directory is the first common ancestor of the entrypoint files, it is considered the project root. This means that the generated bundles live at the top level of the `out` directory; there is no `out/pages` directory.
This behavior can be overridden by specifying the `root` option:

* JavaScript
* CLI

Copy

```
await Bun.build({
  entrypoints: ['./pages/index.tsx', './pages/settings.tsx'],
  outdir: './out',
  root: '.',
})
```

By specifying `.` as `root`, the generated file structure will look like this:

Copy

```
.
└── pages
  └── index.tsx
  └── settings.tsx
└── out
  └── pages
    └── index.js
    └── settings.js
```

### [​](https://bun.com/docs/bundler#publicpath) publicPath

A prefix to be appended to any import paths in bundled code.
In many cases, generated bundles will contain no import statements. After all, the goal of bundling is to combine all of the code into a single file. However there are a number of cases with the generated bundles will contain import statements.

* **Asset imports** — When importing an unrecognized file type like `*.svg`, the bundler defers to the file loader, which copies the file into `outdir` as is. The import is converted into a variable
* **External modules** — Files and modules can be marked as external, in which case they will not be included in the bundle. Instead, the import statement will be left in the final bundle.
* **Chunking.** When `splitting` is enabled, the bundler may generate separate “chunk” files that represent code that is shared among multiple entrypoints.

In any of these cases, the final bundles may contain paths to other files. By default these imports are relative. Here is an example of a simple asset import:

Copy

```
import logo from "./logo.svg";
console.log(logo);
```

Setting `publicPath` will prefix all file paths with the specified value.

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.tsx'],
  outdir: './out',
  publicPath: 'https://cdn.example.com/', // default is undefined
})
```

The output file would now look something like this.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/javascript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=81efd0ad0d779debfa163bfd906ef6a6](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/javascript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=81efd0ad0d779debfa163bfd906ef6a6)out/index.js

Copy

```
var logo = "https://cdn.example.com/logo-a7305bdef.svg";
```

### [​](https://bun.com/docs/bundler#define) define

A map of global identifiers to be replaced at build time. Keys of this object are identifier names, and values are JSON strings that will be inlined.

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.tsx'],
  outdir: './out',
  define: {
    STRING: JSON.stringify("value"),
    "nested.boolean": "true",
  },
})
```

### [​](https://bun.com/docs/bundler#loader) loader

A map of file extensions to built-in loader names. This can be used to quickly customize how certain files are loaded.

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.tsx'],
  outdir: './out',
  loader: {
    ".png": "dataurl",
    ".txt": "file",
  },
})
```

### [​](https://bun.com/docs/bundler#banner) banner

A banner to be added to the final bundle, this can be a directive like `"use client"` for react or a comment block such as a license for the code.

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.tsx'],
  outdir: './out',
  banner: '"use client";'
})
```

### [​](https://bun.com/docs/bundler#footer) footer

A footer to be added to the final bundle, this can be something like a comment block for a license or just a fun easter egg.

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.tsx'],
  outdir: './out',
  footer: '// built with love in SF'
})
```

### [​](https://bun.com/docs/bundler#drop) drop

Remove function calls from a bundle. For example, `--drop=console` will remove all calls to `console.log`. Arguments to calls will also be removed, regardless of if those arguments may have side effects. Dropping `debugger` will remove all `debugger` statements.

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ['./index.tsx'],
  outdir: './out',
  drop: ["console", "debugger", "anyIdentifier.or.propertyAccess"],
})
```

## [​](https://bun.com/docs/bundler#outputs) Outputs

The `Bun.build` function returns a `Promise<BuildOutput>`, defined as:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
interface BuildOutput {
  outputs: BuildArtifact[];
  success: boolean;
  logs: Array<object>; // see docs for details
}

interface BuildArtifact extends Blob {
  kind: "entry-point" | "chunk" | "asset" | "sourcemap";
  path: string;
  loader: Loader;
  hash: string | null;
  sourcemap: BuildArtifact | null;
}
```

The `outputs` array contains all the files that were generated by the build. Each artifact implements the Blob interface.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
const build = await Bun.build({
  /* */
});

for (const output of build.outputs) {
  await output.arrayBuffer(); // => ArrayBuffer
  await output.bytes(); // => Uint8Array
  await output.text(); // string
}
```

Each artifact also contains the following properties:

| Property | Description |
| --- | --- |
| `kind` | What kind of build output this file is. A build generates bundled entrypoints, code-split “chunks”, sourcemaps, bytecode, and copied assets (like images). |
| `path` | Absolute path to the file on disk |
| `loader` | The loader was used to interpret the file. See [Bundler > Loaders](https://bun.com/docs/bundler/loaders) to see how Bun maps file extensions to the appropriate built-in loader. |
| `hash` | The hash of the file contents. Always defined for assets. |
| `sourcemap` | The sourcemap file corresponding to this file, if generated. Only defined for entrypoints and chunks. |

Similar to `BunFile`, `BuildArtifact` objects can be passed directly into `new Response()`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
const build = await Bun.build({
  /* */
});

const artifact = build.outputs[0];

// Content-Type header is automatically set
return new Response(artifact);
```

The Bun runtime implements special pretty-printing of `BuildArtifact` object to make debugging easier.

Copy

```
// build.ts
const build = await Bun.build({
  /* */
});

const artifact = build.outputs[0];
console.log(artifact);
```

## [​](https://bun.com/docs/bundler#bytecode) Bytecode

The `bytecode: boolean` option can be used to generate bytecode for any JavaScript/TypeScript entrypoints. This can greatly improve startup times for large applications. Only supported for `"cjs"` format, only supports `"target": "bun"` and dependent on a matching version of Bun. This adds a corresponding `.jsc` file for each entrypoint.

* JavaScript
* CLI

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
await Bun.build({
  entrypoints: ["./index.tsx"],
  outdir: "./out",
  bytecode: true,
})
```

## [​](https://bun.com/docs/bundler#executables) Executables

Bun supports “compiling” a JavaScript/TypeScript entrypoint into a standalone executable. This executable contains a copy of the Bun binary.

terminal

Copy

```
bun build ./cli.tsx --outfile mycli --compile
./mycli
```

Refer to [Bundler > Executables](https://bun.com/docs/bundler/executables) for complete documentation.

## [​](https://bun.com/docs/bundler#logs-and-errors) Logs and errors

On failure, `Bun.build` returns a rejected promise with an `AggregateError`. This can be logged to the console for pretty printing of the error list, or programmatically read with a try/catch block.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
try {
  const result = await Bun.build({
    entrypoints: ["./index.tsx"],
    outdir: "./out",
  });
} catch (e) {
  // TypeScript does not allow annotations on the catch clause
  const error = e as AggregateError;
  console.error("Build Failed");

  // Example: Using the built-in formatter
  console.error(error);

  // Example: Serializing the failure as a JSON string.
  console.error(JSON.stringify(error, null, 2));
}
```

Most of the time, an explicit try/catch is not needed, as Bun will neatly print uncaught exceptions. It is enough to just use a top-level await on the `Bun.build` call.
Each item in `error.errors` is an instance of `BuildMessage` or `ResolveMessage` (subclasses of `Error`), containing detailed information for each error.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
class BuildMessage {
  name: string;
  position?: Position;
  message: string;
  level: "error" | "warning" | "info" | "debug" | "verbose";
}

class ResolveMessage extends BuildMessage {
  code: string;
  referrer: string;
  specifier: string;
  importKind: ImportKind;
}
```

On build success, the returned object contains a `logs` property, which contains bundler warnings and info messages.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)build.ts

Copy

```
const result = await Bun.build({
  entrypoints: ["./index.tsx"],
  outdir: "./out",
});

if (result.logs.length > 0) {
  console.warn("Build succeeded with warnings:");
  for (const message of result.logs) {
    // Bun will pretty print the message object
    console.warn(message);
  }
}
```

## [​](https://bun.com/docs/bundler#reference) Reference

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)Typescript Definitions

Copy

```
interface Bun {
  build(options: BuildOptions): Promise<BuildOutput>;
}

interface BuildConfig {
  entrypoints: string[]; // list of file path
  outdir?: string; // output directory
  target?: Target; // default: "browser"
  /**
   * Output module format. Top-level await is only supported for `"esm"`.
   *
   * Can be:
   * - `"esm"`
   * - `"cjs"` (**experimental**)
   * - `"iife"` (**experimental**)
   *
   * @default "esm"
   */
  format?: "esm" | "cjs" | "iife";
  /**
   * JSX configuration object for controlling JSX transform behavior
   */
  jsx?: {
    runtime?: "automatic" | "classic";
    importSource?: string;
    factory?: string;
    fragment?: string;
    sideEffects?: boolean;
    development?: boolean;
  };
  naming?:
    | string
    | {
        chunk?: string;
        entry?: string;
        asset?: string;
      };
  root?: string; // project root
  splitting?: boolean; // default true, enable code splitting
  plugins?: BunPlugin[];
  external?: string[];
  packages?: "bundle" | "external";
  publicPath?: string;
  define?: Record<string, string>;
  loader?: { [k in string]: Loader };
  sourcemap?: "none" | "linked" | "inline" | "external" | boolean; // default: "none", true -> "inline"
  /**
   * package.json `exports` conditions used when resolving imports
   *
   * Equivalent to `--conditions` in `bun build` or `bun run`.
   *
   * https://nodejs.org/api/packages.html#exports
   */
  conditions?: Array<string> | string;

  /**
   * Controls how environment variables are handled during bundling.
   *
   * Can be one of:
   * - `"inline"`: Injects environment variables into the bundled output by converting `process.env.FOO`
   *   references to string literals containing the actual environment variable values
   * - `"disable"`: Disables environment variable injection entirely
   * - A string ending in `*`: Inlines environment variables that match the given prefix.
   *   For example, `"MY_PUBLIC_*"` will only include env vars starting with "MY_PUBLIC_"
   */
  env?: "inline" | "disable" | `${string}*`;
  minify?:
    | boolean
    | {
        whitespace?: boolean;
        syntax?: boolean;
        identifiers?: boolean;
      };
  /**
   * Ignore dead code elimination/tree-shaking annotations such as @__PURE__ and package.json
   * "sideEffects" fields. This should only be used as a temporary workaround for incorrect
   * annotations in libraries.
   */
  ignoreDCEAnnotations?: boolean;
  /**
   * Force emitting @__PURE__ annotations even if minify.whitespace is true.
   */
  emitDCEAnnotations?: boolean;

  /**
   * Generate bytecode for the output. This can dramatically improve cold
   * start times, but will make the final output larger and slightly increase
   * memory usage.
   *
   * Bytecode is currently only supported for CommonJS (`format: "cjs"`).
   *
   * Must be `target: "bun"`
   * @default false
   */
  bytecode?: boolean;
  /**
   * Add a banner to the bundled code such as "use client";
   */
  banner?: string;
  /**
   * Add a footer to the bundled code such as a comment block like
   *
   * `// made with bun!`
   */
  footer?: string;

  /**
   * Drop function calls to matching property accesses.
   */
  drop?: string[];

  /**
   * - When set to `true`, the returned promise rejects with an AggregateError when a build failure happens.
   * - When set to `false`, returns a {@link BuildOutput} with `{success: false}`
   *
   * @default true
   */
  throw?: boolean;

  /**
   * Custom tsconfig.json file path to use for path resolution.
   * Equivalent to `--tsconfig-override` in the CLI.
   */
  tsconfig?: string;

  outdir?: string;
}

interface BuildOutput {
  outputs: BuildArtifact[];
  success: boolean;
  logs: Array<BuildMessage | ResolveMessage>;
}

interface BuildArtifact extends Blob {
  path: string;
  loader: Loader;
  hash: string | null;
  kind: "entry-point" | "chunk" | "asset" | "sourcemap" | "bytecode";
  sourcemap: BuildArtifact | null;
}

type Loader =
  | "js"
  | "jsx"
  | "ts"
  | "tsx"
  | "css"
  | "json"
  | "jsonc"
  | "toml"
  | "yaml"
  | "text"
  | "file"
  | "napi"
  | "wasm"
  | "html";

interface BuildOutput {
  outputs: BuildArtifact[];
  success: boolean;
  logs: Array<BuildMessage | ResolveMessage>;
}

declare class ResolveMessage {
  readonly name: "ResolveMessage";
  readonly position: Position | null;
  readonly code: string;
  readonly message: string;
  readonly referrer: string;
  readonly specifier: string;
  readonly importKind:
    | "entry_point"
    | "stmt"
    | "require"
    | "import"
    | "dynamic"
    | "require_resolve"
    | "at"
    | "at_conditional"
    | "url"
    | "internal";
  readonly level: "error" | "warning" | "info" | "debug" | "verbose";

  toString(): string;
}
```

---

## [​](https://bun.com/docs/bundler#cli-usage) CLI Usage

Copy

```
bun build <entry points>
```

### [​](https://bun.com/docs/bundler#general-configuration) General Configuration

[​](https://bun.com/docs/bundler#param-production)

--production

boolean

Set `NODE_ENV=production` and enable minification

[​](https://bun.com/docs/bundler#param-bytecode)

--bytecode

boolean

Use a bytecode cache when compiling

[​](https://bun.com/docs/bundler#param-target)

--target

string

default:"browser"

Intended execution environment for the bundle. One of `browser`, `bun`, or `node`

[​](https://bun.com/docs/bundler#param-conditions)

--conditions

string

Pass custom resolution conditions

[​](https://bun.com/docs/bundler#param-env)

--env

string

default:"disable"

Inline environment variables into the bundle as `process.env.$`. To inline variables matching a
prefix, use a glob like `FOO_PUBLIC_*`

### [​](https://bun.com/docs/bundler#output-&-file-handling) Output & File Handling

[​](https://bun.com/docs/bundler#param-outdir)

--outdir

string

default:"dist"

Output directory (used when building multiple entry points)

[​](https://bun.com/docs/bundler#param-outfile)

--outfile

string

Write output to a specific file

[​](https://bun.com/docs/bundler#param-sourcemap)

--sourcemap

string

default:"none"

Generate source maps. One of `linked`, `inline`, `external`, or `none`

[​](https://bun.com/docs/bundler#param-banner)

--banner

string

Add a banner to the output (e.g. `“use client”` for React Server Components)

[​](https://bun.com/docs/bundler#param-footer)

--footer

string

Add a footer to the output (e.g. `// built with bun!`)

[​](https://bun.com/docs/bundler#param-format)

--format

string

default:"esm"

Module format of the output bundle. One of `esm`, `cjs`, or `iife`

### [​](https://bun.com/docs/bundler#file-naming) File Naming

[​](https://bun.com/docs/bundler#param-entry-naming)

--entry-naming

string

default:"[dir]/[name].[ext]"

Customize entry point filenames

[​](https://bun.com/docs/bundler#param-chunk-naming)

--chunk-naming

string

default:"[name]-[hash].[ext]"

Customize chunk filenames

[​](https://bun.com/docs/bundler#param-asset-naming)

--asset-naming

string

default:"[name]-[hash].[ext]"

Customize asset filenames

### [​](https://bun.com/docs/bundler#bundling-options) Bundling Options

[​](https://bun.com/docs/bundler#param-root)

--root

string

Root directory used when bundling multiple entry points

[​](https://bun.com/docs/bundler#param-splitting)

--splitting

boolean

Enable code splitting for shared modules

[​](https://bun.com/docs/bundler#param-public-path)

--public-path

string

Prefix to be added to import paths in bundled code

[​](https://bun.com/docs/bundler#param-external)

--external

string

Exclude modules from the bundle (supports wildcards). Alias: `-e`

[​](https://bun.com/docs/bundler#param-packages)

--packages

string

default:"bundle"

How to treat dependencies: `external` or `bundle`

[​](https://bun.com/docs/bundler#param-no-bundle)

--no-bundle

boolean

Transpile only — do not bundle

[​](https://bun.com/docs/bundler#param-css-chunking)

--css-chunking

boolean

Chunk CSS files together to reduce duplication (only when multiple entry points import CSS)

### [​](https://bun.com/docs/bundler#minification-&-optimization) Minification & Optimization

[​](https://bun.com/docs/bundler#param-emit-dce-annotations)

--emit-dce-annotations

boolean

default:"true"

Re-emit Dead Code Elimination annotations. Disabled when `—minify-whitespace` is used

[​](https://bun.com/docs/bundler#param-minify)

--minify

boolean

Enable all minification options

[​](https://bun.com/docs/bundler#param-minify-syntax)

--minify-syntax

boolean

Minify syntax and inline constants

[​](https://bun.com/docs/bundler#param-minify-whitespace)

--minify-whitespace

boolean

Minify whitespace

[​](https://bun.com/docs/bundler#param-minify-identifiers)

--minify-identifiers

boolean

Minify variable and function identifiers

[​](https://bun.com/docs/bundler#param-keep-names)

--keep-names

boolean

Preserve original function and class names when minifying

### [​](https://bun.com/docs/bundler#development-features) Development Features

[​](https://bun.com/docs/bundler#param-watch)

--watch

boolean

Rebuild automatically when files change

[​](https://bun.com/docs/bundler#param-no-clear-screen)

--no-clear-screen

boolean

Don’t clear the terminal when rebuilding with `—watch`

[​](https://bun.com/docs/bundler#param-react-fast-refresh)

--react-fast-refresh

boolean

Enable React Fast Refresh transform (for development testing)

### [​](https://bun.com/docs/bundler#standalone-executables) Standalone Executables

[​](https://bun.com/docs/bundler#param-compile)

--compile

boolean

Generate a standalone Bun executable containing the bundle. Implies `—production`

[​](https://bun.com/docs/bundler#param-compile-exec-argv)

--compile-exec-argv

string

Prepend arguments to the standalone executable’s `execArgv`

### [​](https://bun.com/docs/bundler#windows-executable-details) Windows Executable Details

[​](https://bun.com/docs/bundler#param-windows-hide-console)

--windows-hide-console

boolean

Prevent a console window from opening when running a compiled Windows executable

[​](https://bun.com/docs/bundler#param-windows-icon)

--windows-icon

string

Set an icon for the Windows executable

[​](https://bun.com/docs/bundler#param-windows-title)

--windows-title

string

Set the Windows executable product name

[​](https://bun.com/docs/bundler#param-windows-publisher)

--windows-publisher

string

Set the Windows executable company name

[​](https://bun.com/docs/bundler#param-windows-version)

--windows-version

string

Set the Windows executable version (e.g. `1.2.3.4`)

[​](https://bun.com/docs/bundler#param-windows-description)

--windows-description

string

Set the Windows executable description

[​](https://bun.com/docs/bundler#param-windows-copyright)

--windows-copyright

string

Set the Windows executable copyright notice

### [​](https://bun.com/docs/bundler#experimental-&-app-building) Experimental & App Building

[​](https://bun.com/docs/bundler#param-app)

--app

boolean

**(EXPERIMENTAL)** Build a web app for production using Bun Bake

[​](https://bun.com/docs/bundler#param-server-components)

--server-components

boolean

**(EXPERIMENTAL)** Enable React Server Components

[​](https://bun.com/docs/bundler#param-debug-dump-server-files)

--debug-dump-server-files

boolean

When `—app` is set, dump all server files to disk even for static builds

[​](https://bun.com/docs/bundler#param-debug-no-minify)

--debug-no-minify

boolean

When `—app` is set, disable all minification

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/bundler.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /bundler)

⌘I