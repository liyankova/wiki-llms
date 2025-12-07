---
url: https://bun.com/docs/bundler/executables
title: Single-file executable - Bun
source_domain: bun.com
---

# Single-file executable - Bun

Bun’s bundler implements a `--compile` flag for generating a standalone binary from a TypeScript or JavaScript file.

Copy

```
bun build ./cli.ts --compile --outfile mycli
```

This bundles `cli.ts` into an executable that can be executed directly:

terminal

Copy

```
./mycli
```

Copy

```
Hello world!
```

All imported files and packages are bundled into the executable, along with a copy of the Bun runtime. All built-in Bun and Node.js APIs are supported.

---

## [​](https://bun.com/docs/bundler/executables#cross-compile-to-other-platforms) Cross-compile to other platforms

The `--target` flag lets you compile your standalone executable for a different operating system, architecture, or version of Bun than the machine you’re running `bun build` on.
To build for Linux x64 (most servers):

terminal

Copy

```
bun build --compile --target=bun-linux-x64 ./index.ts --outfile myapp

# To support CPUs from before 2013, use the baseline version (nehalem)
bun build --compile --target=bun-linux-x64-baseline ./index.ts --outfile myapp

# To explicitly only support CPUs from 2013 and later, use the modern version (haswell)
# modern is faster, but baseline is more compatible.
bun build --compile --target=bun-linux-x64-modern ./index.ts --outfile myapp
```

To build for Linux ARM64 (e.g. Graviton or Raspberry Pi):

terminal

Copy

```
# Note: the default architecture is x64 if no architecture is specified.
bun build --compile --target=bun-linux-arm64 ./index.ts --outfile myapp
```

To build for Windows x64:

terminal

Copy

```
bun build --compile --target=bun-windows-x64 ./path/to/my/app.ts --outfile myapp

# To support CPUs from before 2013, use the baseline version (nehalem)
bun build --compile --target=bun-windows-x64-baseline ./path/to/my/app.ts --outfile myapp

# To explicitly only support CPUs from 2013 and later, use the modern version (haswell)
bun build --compile --target=bun-windows-x64-modern ./path/to/my/app.ts --outfile myapp

# note: if no .exe extension is provided, Bun will automatically add it for Windows executables
```

To build for macOS arm64:

terminal

Copy

```
bun build --compile --target=bun-darwin-arm64 ./path/to/my/app.ts --outfile myapp
```

To build for macOS x64:

terminal

Copy

```
bun build --compile --target=bun-darwin-x64 ./path/to/my/app.ts --outfile myapp
```

### [​](https://bun.com/docs/bundler/executables#supported-targets) Supported targets

The order of the `--target` flag does not matter, as long as they’re delimited by a `-`.

| —target | Operating System | Architecture | Modern | Baseline | Libc |
| --- | --- | --- | --- | --- | --- |
| bun-linux-x64 | Linux | x64 | ✅ | ✅ | glibc |
| bun-linux-arm64 | Linux | arm64 | ✅ | N/A | glibc |
| bun-windows-x64 | Windows | x64 | ✅ | ✅ | - |
| ~~bun-windows-arm64~~ | ~~Windows~~ | ~~arm64~~ | ❌ | ❌ | - |
| bun-darwin-x64 | macOS | x64 | ✅ | ✅ | - |
| bun-darwin-arm64 | macOS | arm64 | ✅ | N/A | - |
| bun-linux-x64-musl | Linux | x64 | ✅ | ✅ | musl |
| bun-linux-arm64-musl | Linux | arm64 | ✅ | N/A | musl |

On x64 platforms, Bun uses SIMD optimizations which require a modern CPU supporting AVX2 instructions. The `-baseline`
build of Bun is for older CPUs that don’t support these optimizations. Normally, when you install Bun we automatically
detect which version to use but this can be harder to do when cross-compiling since you might not know the target CPU.
You usually don’t need to worry about it on Darwin x64, but it is relevant for Windows x64 and Linux x64. If you or
your users see `"Illegal instruction"` errors, you might need to use the baseline version.

---

## [​](https://bun.com/docs/bundler/executables#build-time-constants) Build-time constants

Use the `--define` flag to inject build-time constants into your executable, such as version numbers, build timestamps, or configuration values:

terminal

Copy

```
bun build --compile --define BUILD_VERSION='"1.2.3"' --define BUILD_TIME='"2024-01-15T10:30:00Z"' src/cli.ts --outfile mycli
```

These constants are embedded directly into your compiled binary at build time, providing zero runtime overhead and enabling dead code elimination optimizations.

For comprehensive examples and advanced patterns, see the [Build-time constants
guide](https://bun.com/docs/guides/runtime/build-time-constants).

---

## [​](https://bun.com/docs/bundler/executables#deploying-to-production) Deploying to production

Compiled executables reduce memory usage and improve Bun’s start time.
Normally, Bun reads and transpiles JavaScript and TypeScript files on `import` and `require`. This is part of what makes so much of Bun “just work”, but it’s not free. It costs time and memory to read files from disk, resolve file paths, parse, transpile, and print source code.
With compiled executables, you can move that cost from runtime to build-time.
When deploying to production, we recommend the following:

terminal

Copy

```
bun build --compile --minify --sourcemap ./path/to/my/app.ts --outfile myapp
```

### [​](https://bun.com/docs/bundler/executables#bytecode-compilation) Bytecode compilation

To improve startup time, enable bytecode compilation:

terminal

Copy

```
bun build --compile --minify --sourcemap --bytecode ./path/to/my/app.ts --outfile myapp
```

Using bytecode compilation, `tsc` starts 2x faster:

![Bytecode performance comparison](https://github.com/user-attachments/assets/dc8913db-01d2-48f8-a8ef-ac4e984f9763)

Bytecode compilation moves parsing overhead for large input files from runtime to bundle time. Your app starts faster, in exchange for making the `bun build` command a little slower. It doesn’t obscure source code.

**Experimental:** Bytecode compilation is an experimental feature. Only `cjs` format is supported (which means no
top-level-await). Let us know if you run into any issues!

### [​](https://bun.com/docs/bundler/executables#what-do-these-flags-do) What do these flags do?

The `--minify` argument optimizes the size of the transpiled output code. If you have a large application, this can save megabytes of space. For smaller applications, it might still improve start time a little.
The `--sourcemap` argument embeds a sourcemap compressed with zstd, so that errors & stacktraces point to their original locations instead of the transpiled location. Bun will automatically decompress & resolve the sourcemap when an error occurs.
The `--bytecode` argument enables bytecode compilation. Every time you run JavaScript code in Bun, JavaScriptCore (the engine) will compile your source code into bytecode. We can move this parsing work from runtime to bundle time, saving you startup time.

---

## [​](https://bun.com/docs/bundler/executables#embedding-runtime-arguments) Embedding runtime arguments

**`--compile-exec-argv="args"`** - Embed runtime arguments that are available via `process.execArgv`:

terminal

Copy

```
bun build --compile --compile-exec-argv="--smol --user-agent=MyBot" ./app.ts --outfile myapp
```

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)app.ts

Copy

```
// In the compiled app
console.log(process.execArgv); // ["--smol", "--user-agent=MyBot"]
```

---

## [​](https://bun.com/docs/bundler/executables#disabling-automatic-config-loading) Disabling automatic config loading

By default, standalone executables look for `.env` and `bunfig.toml` files in the directory where the executable is run. You can disable this behavior at build time for deterministic execution regardless of the user’s working directory.

terminal

Copy

```
# Disable .env loading
bun build --compile --no-compile-autoload-dotenv ./app.ts --outfile myapp

# Disable bunfig.toml loading
bun build --compile --no-compile-autoload-bunfig ./app.ts --outfile myapp

# Disable both
bun build --compile --no-compile-autoload-dotenv --no-compile-autoload-bunfig ./app.ts --outfile myapp
```

You can also configure this via the JavaScript API:

Copy

```
await Bun.build({
  entrypoints: ["./app.ts"],
  compile: {
    autoloadDotenv: false, // Disable .env loading
    autoloadBunfig: false, // Disable bunfig.toml loading
  },
});
```

---

## [​](https://bun.com/docs/bundler/executables#act-as-the-bun-cli) Act as the Bun CLI

New in Bun v1.2.16

You can run a standalone executable as if it were the `bun` CLI itself by setting the `BUN_BE_BUN=1` environment variable. When this variable is set, the executable will ignore its bundled entrypoint and instead expose all the features of Bun’s CLI.
For example, consider an executable compiled from a simple script:

terminal

Copy

```
echo "console.log(\"you shouldn't see this\");" > such-bun.js
bun build --compile ./such-bun.js
```

Copy

```
[3ms] bundle 1 modules
[89ms] compile such-bun
```

Normally, running `./such-bun` with arguments would execute the script.

terminal

Copy

```
# Executable runs its own entrypoint by default
./such-bun install
```

Copy

```
you shouldn't see this
```

However, with the `BUN_BE_BUN=1` environment variable, it acts just like the `bun` binary:

terminal

Copy

```
# With the env var, the executable acts like the `bun` CLI
BUN_BE_BUN=1 ./such-bun install
```

Copy

```
bun install v1.2.16-canary.1 (1d1db811)
Checked 63 installs across 64 packages (no changes) [5.00ms]
```

This is useful for building CLI tools on top of Bun that may need to install packages, bundle dependencies, run different or local files and more without needing to download a separate binary or install bun.

---

## [​](https://bun.com/docs/bundler/executables#full-stack-executables) Full-stack executables

New in Bun v1.2.17

Bun’s `--compile` flag can create standalone executables that contain both server and client code, making it ideal for full-stack applications. When you import an HTML file in your server code, Bun automatically bundles all frontend assets (JavaScript, CSS, etc.) and embeds them into the executable. When Bun sees the HTML import on the server, it kicks off a frontend build process to bundle JavaScript, CSS, and other assets.

Copy

```
import { serve } from "bun";
import index from "./index.html";

const server = serve({
  routes: {
    "/": index,
    "/api/hello": { GET: () => Response.json({ message: "Hello from API" }) },
  },
});

console.log(`Server running at http://localhost:${server.port}`);
```

To build this into a single executable:

terminal

Copy

```
bun build --compile ./server.ts --outfile myapp
```

This creates a self-contained binary that includes:

* Your server code
* The Bun runtime
* All frontend assets (HTML, CSS, JavaScript)
* Any npm packages used by your server

The result is a single file that can be deployed anywhere without needing Node.js, Bun, or any dependencies installed. Just run:

terminal

Copy

```
./myapp
```

Bun automatically handles serving the frontend assets with proper MIME types and cache headers. The HTML import is replaced with a manifest object that `Bun.serve` uses to efficiently serve pre-bundled assets.
For more details on building full-stack applications with Bun, see the [full-stack guide](https://bun.com/docs/bundler/fullstack).

---

## [​](https://bun.com/docs/bundler/executables#worker) Worker

To use workers in a standalone executable, add the worker’s entrypoint to the CLI arguments:

terminal

Copy

```
bun build --compile ./index.ts ./my-worker.ts --outfile myapp
```

Then, reference the worker in your code:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
console.log("Hello from Bun!");

// Any of these will work:
new Worker("./my-worker.ts");
new Worker(new URL("./my-worker.ts", import.meta.url));
new Worker(new URL("./my-worker.ts", import.meta.url).href);
```

When you add multiple entrypoints to a standalone executable, they will be bundled separately into the executable.
In the future, we may automatically detect usages of statically-known paths in `new Worker(path)` and then bundle those into the executable, but for now, you’ll need to add it to the shell command manually like the above example.
If you use a relative path to a file not included in the standalone executable, it will attempt to load that path from disk relative to the current working directory of the process (and then error if it doesn’t exist).

---

## [​](https://bun.com/docs/bundler/executables#sqlite) SQLite

You can use `bun:sqlite` imports with `bun build --compile`.
By default, the database is resolved relative to the current working directory of the process.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
import db from "./my.db" with { type: "sqlite" };

console.log(db.query("select * from users LIMIT 1").get());
```

That means if the executable is located at `/usr/bin/hello`, the user’s terminal is located at `/home/me/Desktop`, it will look for `/home/me/Desktop/my.db`.

terminal

Copy

```
cd /home/me/Desktop
./hello
```

---

## [​](https://bun.com/docs/bundler/executables#embed-assets-&-files) Embed assets & files

Standalone executables support embedding files.
To embed files into an executable with `bun build --compile`, import the file in your code.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
// this becomes an internal file path
import icon from "./icon.png" with { type: "file" };
import { file } from "bun";

export default {
  fetch(req) {
    // Embedded files can be streamed from Response objects
    return new Response(file(icon));
  },
};
```

Embedded files can be read using `Bun.file`’s functions or the Node.js `fs.readFile` function (in `"node:fs"`).
For example, to read the contents of the embedded file:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
import icon from "./icon.png" with { type: "file" };
import { file } from "bun";

const bytes = await file(icon).arrayBuffer();
// await fs.promises.readFile(icon)
// fs.readFileSync(icon)
```

### [​](https://bun.com/docs/bundler/executables#embed-sqlite-databases) Embed SQLite databases

If your application wants to embed a SQLite database into the compiled executable, set `type: "sqlite"` in the import attribute and the `embed` attribute to `"true"`.
The database file must already exist on disk. Then, import it in your code:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
import myEmbeddedDb from "./my.db" with { type: "sqlite", embed: "true" };

console.log(myEmbeddedDb.query("select * from users LIMIT 1").get());
```

Finally, compile it into a standalone executable:

terminal

Copy

```
bun build --compile ./index.ts --outfile mycli
```

The database file must exist on disk when you run `bun build --compile`. The `embed: "true"` attribute tells the
bundler to include the database contents inside the compiled executable. When running normally with `bun run`, the
database file is loaded from disk just like a regular SQLite import.

In the compiled executable, the embedded database is read-write, but all changes are lost when the executable exits (since it’s stored in memory).

### [​](https://bun.com/docs/bundler/executables#embed-n-api-addons) Embed N-API Addons

You can embed `.node` files into executables.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
const addon = require("./addon.node");

console.log(addon.hello());
```

Unfortunately, if you’re using `@mapbox/node-pre-gyp` or other similar tools, you’ll need to make sure the `.node` file is directly required or it won’t bundle correctly.

### [​](https://bun.com/docs/bundler/executables#embed-directories) Embed directories

To embed a directory with `bun build --compile`, use a shell glob in your `bun build` command:

terminal

Copy

```
bun build --compile ./index.ts ./public/**/*.png
```

Then, you can reference the files in your code:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
import icon from "./public/assets/icon.png" with { type: "file" };
import { file } from "bun";

export default {
  fetch(req) {
    // Embedded files can be streamed from Response objects
    return new Response(file(icon));
  },
};
```

This is honestly a workaround, and we expect to improve this in the future with a more direct API.

### [​](https://bun.com/docs/bundler/executables#listing-embedded-files) Listing embedded files

To get a list of all embedded files, use `Bun.embeddedFiles`:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
import "./icon.png" with { type: "file" };
import { embeddedFiles } from "bun";

console.log(embeddedFiles[0].name); // `icon-${hash}.png`
```

`Bun.embeddedFiles` returns an array of `Blob` objects which you can use to get the size, contents, and other properties of the files.

Copy

```
embeddedFiles: Blob[]
```

The list of embedded files excludes bundled source code like `.ts` and `.js` files.

#### [​](https://bun.com/docs/bundler/executables#content-hash) Content hash

By default, embedded files have a content hash appended to their name. This is useful for situations where you want to serve the file from a URL or CDN and have fewer cache invalidation issues. But sometimes, this is unexpected and you might want the original name instead:
To disable the content hash, pass `--asset-naming` to `bun build --compile` like this:

terminal

Copy

```
bun build --compile --asset-naming="[name].[ext]" ./index.ts
```

---

## [​](https://bun.com/docs/bundler/executables#minification) Minification

To trim down the size of the executable a little, pass `--minify` to `bun build --compile`. This uses Bun’s minifier to reduce the code size. Overall though, Bun’s binary is still way too big and we need to make it smaller.

---

## [​](https://bun.com/docs/bundler/executables#windows-specific-flags) Windows-specific flags

When compiling a standalone executable on Windows, there are two platform-specific options that can be used to customize metadata on the generated `.exe` file:

* `--windows-icon=path/to/icon.ico` to customize the executable file icon.
* `--windows-hide-console` to disable the background terminal, which can be used for applications that do not need a TTY.

These flags currently cannot be used when cross-compiling because they depend on Windows APIs.

---

## [​](https://bun.com/docs/bundler/executables#code-signing-on-macos) Code signing on macOS

To codesign a standalone executable on macOS (which fixes Gatekeeper warnings), use the `codesign` command.

terminal

Copy

```
codesign --deep --force -vvvv --sign "XXXXXXXXXX" ./myapp
```

We recommend including an `entitlements.plist` file with JIT permissions.

info.plist

Copy

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>com.apple.security.cs.allow-jit</key>
    <true/>
    <key>com.apple.security.cs.allow-unsigned-executable-memory</key>
    <true/>
    <key>com.apple.security.cs.disable-executable-page-protection</key>
    <true/>
    <key>com.apple.security.cs.allow-dyld-environment-variables</key>
    <true/>
    <key>com.apple.security.cs.disable-library-validation</key>
    <true/>
</dict>
</plist>
```

To codesign with JIT support, pass the `--entitlements` flag to `codesign`.

terminal

Copy

```
codesign --deep --force -vvvv --sign "XXXXXXXXXX" --entitlements entitlements.plist ./myapp
```

After codesigning, verify the executable:

terminal

Copy

```
codesign -vvv --verify ./myapp
./myapp: valid on disk
./myapp: satisfies its Designated Requirement
```

Codesign support requires Bun v1.2.4 or newer.

---

## [​](https://bun.com/docs/bundler/executables#code-splitting) Code splitting

Standalone executables support code splitting. Use `--compile` with `--splitting` to create an executable that loads code-split chunks at runtime.

Copy

```
bun build --compile --splitting ./src/entry.ts --outdir ./build
```

Copy

```
console.log("Entrypoint loaded");
const lazy = await import("./lazy.ts");
lazy.hello();
```

terminal

Copy

```
./build/entry
```

Copy

```
Entrypoint loaded
Lazy module loaded
```

---

## [​](https://bun.com/docs/bundler/executables#unsupported-cli-arguments) Unsupported CLI arguments

Currently, the `--compile` flag can only accept a single entrypoint at a time and does not support the following flags:

* `--outdir` — use `outfile` instead (except when using with `--splitting`).
* `--public-path`
* `--target=node` or `--target=browser`
* `--no-bundle` - we always bundle everything into the executable.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/bundler/executables.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /bundler/executables)

⌘I