---
url: https://bun.com/docs/cli/run
title: Bun Runtime - Bun
source_domain: bun.com
---

# Bun Runtime - Bun

The Bun Runtime is designed to start fast and run fast.
Under the hood, Bun uses the [JavaScriptCore engine](https://developer.apple.com/documentation/javascriptcore), which is developed by Apple for Safari. In most cases, the startup and running performance is faster than V8, the engine used by Node.js and Chromium-based browsers. Its transpiler and runtime are written in Zig, a modern, high-performance language. On Linux, this translates into startup times [4x faster](https://twitter.com/jarredsumner/status/1499225725492076544) than Node.js.

| Command | Time |
| --- | --- |
| `bun hello.js` | `5.2ms` |
| `node hello.js` | `25.1ms` |

This benchmark is based on running a simple Hello World script on Linux

## [​](https://bun.com/docs/cli/run#run-a-file) Run a file

Use `bun run` to execute a source file.

terminal

Copy

```
bun run index.js
```

Bun supports TypeScript and JSX out of the box. Every file is transpiled on the fly by Bun’s fast native transpiler before being executed.

terminal

Copy

```
bun run index.js
bun run index.jsx
bun run index.ts
bun run index.tsx
```

Alternatively, you can omit the `run` keyword and use the “naked” command; it behaves identically.

terminal

Copy

```
bun index.tsx
bun index.js
```

### [​](https://bun.com/docs/cli/run#watch) `--watch`

To run a file in watch mode, use the `--watch` flag.

terminal

Copy

```
bun --watch run index.tsx
```

When using `bun run`, put Bun flags like `--watch` immediately after `bun`.

Copy

```
bun --watch run dev # ✔️ do this
bun run dev --watch # ❌ don't do this
```

Flags that occur at the end of the command will be ignored and passed through to the `"dev"` script itself.

## [​](https://bun.com/docs/cli/run#run-a-package-json-script) Run a `package.json` script

Compare to `npm run <script>` or `yarn <script>`

Copy

```
bun [bun flags] run <script> [script flags]
```

Your `package.json` can define a number of named `"scripts"` that correspond to shell commands.

package.json

Copy

```
{
  // ... other fields
  "scripts": {
    "clean": "rm -rf dist && echo 'Done.'",
    "dev": "bun server.ts"
  }
}
```

Use `bun run <script>` to execute these scripts.

terminal

Copy

```
bun run clean
rm -rf dist && echo 'Done.'
```

Copy

```
Cleaning...
Done.
```

Bun executes the script command in a subshell. On Linux & macOS, it checks for the following shells in order, using the first one it finds: `bash`, `sh`, `zsh`. On Windows, it uses [bun shell](https://bun.com/docs/runtime/shell) to support bash-like syntax and many common commands.

⚡️ The startup time for `npm run` on Linux is roughly 170ms; with Bun it is `6ms`.

Scripts can also be run with the shorter command `bun <script>`, however if there is a built-in bun command with the same name, the built-in command takes precedence. In this case, use the more explicit `bun run <script>` command to execute your package script.

terminal

Copy

```
bun run dev
```

To see a list of available scripts, run `bun run` without any arguments.

terminal

Copy

```
bun run
```

Copy

```
quickstart scripts:

 bun run clean
   rm -rf dist && echo 'Done.'

 bun run dev
   bun server.ts

2 scripts
```

Bun respects lifecycle hooks. For instance, `bun run clean` will execute `preclean` and `postclean`, if defined. If the `pre<script>` fails, Bun will not execute the script itself.

### [​](https://bun.com/docs/cli/run#bun) `--bun`

It’s common for `package.json` scripts to reference locally-installed CLIs like `vite` or `next`. These CLIs are often JavaScript files marked with a [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix)) to indicate that they should be executed with `node`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/javascript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=81efd0ad0d779debfa163bfd906ef6a6](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/javascript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=81efd0ad0d779debfa163bfd906ef6a6)cli.js

Copy

```
#!/usr/bin/env node

// do stuff
```

By default, Bun respects this shebang and executes the script with `node`. However, you can override this behavior with the `--bun` flag. For Node.js-based CLIs, this will run the CLI with Bun instead of Node.js.

terminal

Copy

```
bun run --bun vite
```

### [​](https://bun.com/docs/cli/run#filtering) Filtering

In monorepos containing multiple packages, you can use the `--filter` argument to execute scripts in many packages at once.
Use `bun run --filter <name_pattern> <script>` to execute `<script>` in all packages whose name matches `<name_pattern>`.
For example, if you have subdirectories containing packages named `foo`, `bar` and `baz`, running

terminal

Copy

```
bun run --filter 'ba*' <script>
```

will execute `<script>` in both `bar` and `baz`, but not in `foo`.
Find more details in the docs page for [filter](https://bun.com/docs/pm/filter#running-scripts-with-filter).

## [​](https://bun.com/docs/cli/run#bun-run-to-pipe-code-from-stdin) `bun run -` to pipe code from stdin

`bun run -` lets you read JavaScript, TypeScript, TSX, or JSX from stdin and execute it without writing to a temporary file first.

terminal

Copy

```
echo "console.log('Hello')" | bun run -
```

Copy

```
Hello
```

You can also use `bun run -` to redirect files into Bun. For example, to run a `.js` file as if it were a `.ts` file:

terminal

Copy

```
echo "console.log!('This is TypeScript!' as any)" > secretly-typescript.js
bun run - < secretly-typescript.js
```

Copy

```
This is TypeScript!
```

For convenience, all code is treated as TypeScript with JSX support when using `bun run -`.

## [​](https://bun.com/docs/cli/run#bun-run-console-depth) `bun run --console-depth`

Control the depth of object inspection in console output with the `--console-depth` flag.

terminal

Copy

```
bun --console-depth 5 run index.tsx
```

This sets how deeply nested objects are displayed in `console.log()` output. The default depth is `2`. Higher values show more nested properties but may produce verbose output for complex objects.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)console.ts

Copy

```
const nested = { a: { b: { c: { d: "deep" } } } };
console.log(nested);
// With --console-depth 2 (default): { a: { b: [Object] } }
// With --console-depth 4: { a: { b: { c: { d: 'deep' } } } }
```

## [​](https://bun.com/docs/cli/run#bun-run-smol) `bun run --smol`

In memory-constrained environments, use the `--smol` flag to reduce memory usage at a cost to performance.

terminal

Copy

```
bun --smol run index.tsx
```

This causes the garbage collector to run more frequently, which can slow down execution. However, it can be useful in environments with limited memory. Bun automatically adjusts the garbage collector’s heap size based on the available memory (accounting for cgroups and other memory limits) with and without the `--smol` flag, so this is mostly useful for cases where you want to make the heap size grow more slowly.

## [​](https://bun.com/docs/cli/run#resolution-order) Resolution order

Absolute paths and paths starting with `./` or `.\\` are always executed as source files. Unless using `bun run`, running a file with an allowed extension will prefer the file over a package.json script.
When there is a package.json script and a file with the same name, `bun run` prioritizes the package.json script. The full resolution order is:

1. package.json scripts, eg `bun run build`
2. Source files, eg `bun run src/main.js`
3. Binaries from project packages, eg `bun add eslint && bun run eslint`
4. (`bun run` only) System commands, eg `bun run ls`

---

# [​](https://bun.com/docs/cli/run#cli-usage) CLI Usage

Copy

```
bun run <file or script>
```

### [​](https://bun.com/docs/cli/run#general-execution-options) General Execution Options

[​](https://bun.com/docs/cli/run#param-silent)

--silent

boolean

Don’t print the script command

[​](https://bun.com/docs/cli/run#param-if-present)

--if-present

boolean

Exit without an error if the entrypoint does not exist

[​](https://bun.com/docs/cli/run#param-eval)

--eval

string

Evaluate argument as a script. Alias: `-e`

[​](https://bun.com/docs/cli/run#param-print)

--print

string

Evaluate argument as a script and print the result. Alias: `-p`

[​](https://bun.com/docs/cli/run#param-help)

--help

boolean

Display this menu and exit. Alias: `-h`

### [​](https://bun.com/docs/cli/run#workspace-management) Workspace Management

[​](https://bun.com/docs/cli/run#param-elide-lines)

--elide-lines

number

default:"10"

Number of lines of script output shown when using —filter (default: 10). Set to 0 to show all lines

[​](https://bun.com/docs/cli/run#param-filter)

--filter

string

Run a script in all workspace packages matching the pattern. Alias: `-F`

[​](https://bun.com/docs/cli/run#param-workspaces)

--workspaces

boolean

Run a script in all workspace packages (from the `workspaces` field in `package.json`)

### [​](https://bun.com/docs/cli/run#runtime-&-process-control) Runtime & Process Control

[​](https://bun.com/docs/cli/run#param-bun)

--bun

boolean

Force a script or package to use Bun’s runtime instead of Node.js (via symlinking node). Alias: `-b`

[​](https://bun.com/docs/cli/run#param-shell)

--shell

string

Control the shell used for `package.json` scripts. Supports either `bun` or `system`

[​](https://bun.com/docs/cli/run#param-smol)

--smol

boolean

Use less memory, but run garbage collection more often

[​](https://bun.com/docs/cli/run#param-expose-gc)

--expose-gc

boolean

Expose `gc()` on the global object. Has no effect on `Bun.gc()`

[​](https://bun.com/docs/cli/run#param-no-deprecation)

--no-deprecation

boolean

Suppress all reporting of the custom deprecation

[​](https://bun.com/docs/cli/run#param-throw-deprecation)

--throw-deprecation

boolean

Determine whether or not deprecation warnings result in errors

[​](https://bun.com/docs/cli/run#param-title)

--title

string

Set the process title

[​](https://bun.com/docs/cli/run#param-zero-fill-buffers)

--zero-fill-buffers

boolean

Boolean to force `Buffer.allocUnsafe(size)` to be zero-filled

[​](https://bun.com/docs/cli/run#param-no-addons)

--no-addons

boolean

Throw an error if `process.dlopen` is called, and disable export condition `node-addons`

[​](https://bun.com/docs/cli/run#param-unhandled-rejections)

--unhandled-rejections

string

One of `strict`, `throw`, `warn`, `none`, or
`warn-with-error-code`

[​](https://bun.com/docs/cli/run#param-console-depth)

--console-depth

number

default:"2"

Set the default depth for `console.log` object inspection (default: 2)

### [​](https://bun.com/docs/cli/run#development-workflow) Development Workflow

[​](https://bun.com/docs/cli/run#param-watch)

--watch

boolean

Automatically restart the process on file change

[​](https://bun.com/docs/cli/run#param-hot)

--hot

boolean

Enable auto reload in the Bun runtime, test runner, or bundler

[​](https://bun.com/docs/cli/run#param-no-clear-screen)

--no-clear-screen

boolean

Disable clearing the terminal screen on reload when —hot or —watch is enabled

### [​](https://bun.com/docs/cli/run#debugging) Debugging

[​](https://bun.com/docs/cli/run#param-inspect)

--inspect

string

Activate Bun’s debugger

[​](https://bun.com/docs/cli/run#param-inspect-wait)

--inspect-wait

string

Activate Bun’s debugger, wait for a connection before executing

[​](https://bun.com/docs/cli/run#param-inspect-brk)

--inspect-brk

string

Activate Bun’s debugger, set breakpoint on first line of code and wait

### [​](https://bun.com/docs/cli/run#dependency-&-module-resolution) Dependency & Module Resolution

[​](https://bun.com/docs/cli/run#param-preload)

--preload

string

Import a module before other modules are loaded. Alias: `-r`

[​](https://bun.com/docs/cli/run#param-require)

--require

string

Alias of —preload, for Node.js compatibility

[​](https://bun.com/docs/cli/run#param-import)

--import

string

Alias of —preload, for Node.js compatibility

[​](https://bun.com/docs/cli/run#param-no-install)

--no-install

boolean

Disable auto install in the Bun runtime

[​](https://bun.com/docs/cli/run#param-install)

--install

string

default:"auto"

Configure auto-install behavior. One of `auto` (default, auto-installs when no node\_modules),
`fallback` (missing packages only), `force` (always)

[​](https://bun.com/docs/cli/run#param-i)

-i

boolean

Auto-install dependencies during execution. Equivalent to —install=fallback

[​](https://bun.com/docs/cli/run#param-prefer-offline)

--prefer-offline

boolean

Skip staleness checks for packages in the Bun runtime and resolve from disk

[​](https://bun.com/docs/cli/run#param-prefer-latest)

--prefer-latest

boolean

Use the latest matching versions of packages in the Bun runtime, always checking npm

[​](https://bun.com/docs/cli/run#param-conditions)

--conditions

string

Pass custom conditions to resolve

[​](https://bun.com/docs/cli/run#param-main-fields)

--main-fields

string

Main fields to lookup in `package.json`. Defaults to —target dependent

[​](https://bun.com/docs/cli/run#param-preserve-symlinks)

--preserve-symlinks

boolean

Preserve symlinks when resolving files

[​](https://bun.com/docs/cli/run#param-preserve-symlinks-main)

--preserve-symlinks-main

boolean

Preserve symlinks when resolving the main entry point

[​](https://bun.com/docs/cli/run#param-extension-order)

--extension-order

string

default:".tsx,.ts,.jsx,.js,.json"

Defaults to: `.tsx,.ts,.jsx,.js,.json`

### [​](https://bun.com/docs/cli/run#transpilation-&-language-features) Transpilation & Language Features

[​](https://bun.com/docs/cli/run#param-tsconfig-override)

--tsconfig-override

string

Specify custom `tsconfig.json`. Default `$cwd/tsconfig.json`

[​](https://bun.com/docs/cli/run#param-define)

--define

string

Substitute K:V while parsing, e.g. `—define process.env.NODE_ENV:“development”`. Values are parsed as
JSON. Alias: `-d`

[​](https://bun.com/docs/cli/run#param-drop)

--drop

string

Remove function calls, e.g. `—drop=console` removes all `console.*` calls

[​](https://bun.com/docs/cli/run#param-loader)

--loader

string

Parse files with `.ext:loader`, e.g. `—loader .js:jsx`. Valid loaders: `js`,
`jsx`, `ts`, `tsx`, `json`, `toml`, `text`,
`file`, `wasm`, `napi`. Alias: `-l`

[​](https://bun.com/docs/cli/run#param-no-macros)

--no-macros

boolean

Disable macros from being executed in the bundler, transpiler and runtime

[​](https://bun.com/docs/cli/run#param-jsx-factory)

--jsx-factory

string

Changes the function called when compiling JSX elements using the classic JSX runtime

[​](https://bun.com/docs/cli/run#param-jsx-fragment)

--jsx-fragment

string

Changes the function called when compiling JSX fragments

[​](https://bun.com/docs/cli/run#param-jsx-import-source)

--jsx-import-source

string

default:"react"

Declares the module specifier to be used for importing the jsx and jsxs factory functions. Default: `react`

[​](https://bun.com/docs/cli/run#param-jsx-runtime)

--jsx-runtime

string

default:"automatic"

`automatic` (default) or `classic`

[​](https://bun.com/docs/cli/run#param-jsx-side-effects)

--jsx-side-effects

boolean

Treat JSX elements as having side effects (disable pure annotations)

[​](https://bun.com/docs/cli/run#param-ignore-dce-annotations)

--ignore-dce-annotations

boolean

Ignore tree-shaking annotations such as `@PURE`

### [​](https://bun.com/docs/cli/run#networking-&-security) Networking & Security

[​](https://bun.com/docs/cli/run#param-port)

--port

number

Set the default port for `Bun.serve`

[​](https://bun.com/docs/cli/run#param-fetch-preconnect)

--fetch-preconnect

string

Preconnect to a URL while code is loading

[​](https://bun.com/docs/cli/run#param-max-http-header-size)

--max-http-header-size

number

default:"16384"

Set the maximum size of HTTP headers in bytes. Default is 16KiB

[​](https://bun.com/docs/cli/run#param-dns-result-order)

--dns-result-order

string

default:"verbatim"

Set the default order of DNS lookup results. Valid orders: `verbatim` (default), `ipv4first`,
`ipv6first`

[​](https://bun.com/docs/cli/run#param-use-system-ca)

--use-system-ca

boolean

Use the system’s trusted certificate authorities

[​](https://bun.com/docs/cli/run#param-use-openssl-ca)

--use-openssl-ca

boolean

Use OpenSSL’s default CA store

[​](https://bun.com/docs/cli/run#param-use-bundled-ca)

--use-bundled-ca

boolean

Use bundled CA store

[​](https://bun.com/docs/cli/run#param-redis-preconnect)

--redis-preconnect

boolean

Preconnect to `$REDIS_URL` at startup

[​](https://bun.com/docs/cli/run#param-sql-preconnect)

--sql-preconnect

boolean

Preconnect to PostgreSQL at startup

[​](https://bun.com/docs/cli/run#param-user-agent)

--user-agent

string

Set the default User-Agent header for HTTP requests

### [​](https://bun.com/docs/cli/run#global-configuration-&-context) Global Configuration & Context

[​](https://bun.com/docs/cli/run#param-env-file)

--env-file

string

Load environment variables from the specified file(s)

[​](https://bun.com/docs/cli/run#param-cwd)

--cwd

string

Absolute path to resolve files & entry points from. This just changes the process’ cwd

[​](https://bun.com/docs/cli/run#param-config)

--config

string

Specify path to Bun config file. Default `$cwd/bunfig.toml`. Alias: `-c`

## [​](https://bun.com/docs/cli/run#examples) Examples

Run a JavaScript or TypeScript file:

Copy

```
bun run ./index.js
bun run ./index.tsx
```

Run a package.json script:

Copy

```
bun run dev
bun run lint
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/runtime.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /runtime)

⌘I