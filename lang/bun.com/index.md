---
url: https://bun.com/
title: Bun — A fast all-in-one JavaScript runtime
source_domain: bun.com
---

# Bun — A fast all-in-one JavaScript runtime

[Bun is joining Anthropic & Anthropic is betting on Bun →](https://bun.com/blog/bun-joins-anthropic)

[Bun v1.3.3 is here! →](https://bun.com/blog/bun-v1.3.3)

# Bun is a fast JavaScript all-in-one toolkit|

Bun is a fast, **incrementally adoptable** all-in-one JavaScript, TypeScript & JSX toolkit. Use individual tools like bun test or **bun install in Node.js** projects, or adopt the complete stack with a fast JavaScript runtime, bundler, [test runner](https://bun.com/docs/cli/test), and [package manager](https://bun.com/package-manager) built in. Bun aims for 100% Node.js compatibility.

Install Bun v1.3.3

[View install script](https://bun.sh/install)

```
curl -fsSL https://bun.sh/install | bash
```

```
powershell -c "irm bun.sh/install.ps1 | iex"
```

USED BY

![](https://bun.com/images/logo-bar.png)

![Lovable logo](https://bun.com/logos/lovable.svg)![CodeRabbit logo](https://bun.com/logos/coderabbit.svg)![Replit logo](https://bun.com/logos/replit-wordmark.svg)![Cursor logo](https://bun.com/logos/cursor.svg)

## Bundling 10,000 React components

Build time in milliseconds (Linux x64, Hetzner)

Bun

v1.3.0

269.1 ms

Rolldown

v1.0.0-beta.42

494.9 ms

esbuild

v0.25.10

571.9 ms

Farm

v1.0.5

1,608 ms

Rspack

v1.5.8

2,137 ms

[View benchmark →](https://github.com/rolldown/benchmarks/blob/134f936777397f5d1246b5ef8974f01e2f799690/apps/10000/package.json)

## Express.js 'hello world'

HTTP requests per second (Linux x64)

* bun: 59,026 requests per second

  59,026
* deno: 25,335 requests per second

  25,335
* node: 19,039 requests per second

  19,039

[Bun

v1.2](https://github.com/oven-sh/bun/blob/246936a7a4a0c5c8025a14072f49fde11d599a71/bench/express/express.mjs)[Deno

v2.1.6](https://github.com/oven-sh/bun/blob/246936a7a4a0c5c8025a14072f49fde11d599a71/bench/express/express.mjs)[Node.js

v23.6.0](https://github.com/oven-sh/bun/blob/246936a7a4a0c5c8025a14072f49fde11d599a71/bench/express/express.mjs)

[View benchmark →](https://github.com/oven-sh/bun/tree/main/bench/express "$ bombardier <url> -d 5s")

## WebSocket chat server

Messages sent per second (Linux x64, 32 clients)

* bun: 2,536,227 messages sent per second

  2,536,227
* deno: 1,320,525 messages sent per second

  1,320,525
* node: 435,099 messages sent per second

  435,099

[Bun.serve()

v1.2](https://github.com/oven-sh/bun/blob/58417217d6c68c2fcf5169f0e5031b0ce9005bf3/bench/websocket-server/chat-server.bun.js)[Deno.serve()

v1.2.6](https://github.com/oven-sh/bun/blob/58417217d6c68c2fcf5169f0e5031b0ce9005bf3/bench/websocket-server/chat-server.deno.mjs)[ws (Node.js)

v23.6.0](https://github.com/oven-sh/bun/blob/58417217d6c68c2fcf5169f0e5031b0ce9005bf3/bench/websocket-server/chat-server.node.mjs)

[View benchmark →](https://github.com/oven-sh/bun/tree/main/bench/websocket-server)

## Load a huge table

Queries per second. 100 rows x 100 parallel queries

* bun: 28,571 queries per second

  28,571
* node: 14,522 queries per second

  14,522
* deno: 11,169 queries per second

  11,169

[Bun

v1.2.22](https://github.com/oven-sh/bun/blob/main/bench/postgres/index.mjs)[Node.js

v24.8.0](https://github.com/oven-sh/bun/blob/main/bench/postgres/index.mjs)[Deno

v2.5.1](https://github.com/oven-sh/bun/blob/main/bench/postgres/index.mjs)

[View benchmark →](https://github.com/oven-sh/bun/tree/main/bench/postgres)

## Four tools, one toolkit

Use them together as an all-in-one toolkit, or adopt them incrementally. `bun test` works in Node.js projects. `bun install` can be used as the fastest npm client. Each tool stands on its own.

[### JavaScript Runtime

Starts 3x faster than Node.js

A fast JavaScript runtime designed as a drop-in replacement for Node.js

`$ bun ./index.ts`](https://bun.com/docs/runtime)

* ✓[Node.js API compatibility](https://bun.com/docs/runtime/nodejs-apis)
* ✓[TypeScript, JSX & React (zero config)](https://bun.com/docs/runtime/typescript)
* ✓[Comprehensive builtin standard library](https://bun.com/docs/api/fetch)
* ✓[PostgreSQL, Redis, MySQL, SQLite](https://bun.com/docs/api/sql)
* ✓[Hot & watch mode built-in](https://bun.com/docs/cli/run)
* ✓[Environment variables with .env](https://bun.com/docs/runtime/env)

[### Package Manager

30x faster

Install packages up to 30x faster than npm with a global cache and workspaces

`$ bun install`](https://bun.com/docs/cli/install)

* ✓[Simple migration from npm/pnpm/yarn](https://bun.com/docs/cli/install)
* ✓[Eliminate phantom dependencies](https://bun.com/docs/install/isolated)
* ✓[Workspaces, monorepos](https://bun.com/docs/install/workspaces)
* ✓[Lifecycle scripts & postinstall handling](https://bun.com/docs/cli/install#lifecycle-scripts)
* ✓[Dependency auditing with bun audit](https://bun.com/docs/install/audit)
* ✓[Block malicious packages](https://bun.com/docs/cli/install#trusted)

[### Test Runner

Replaces Jest & Vitest

Jest-compatible test runner with built-in code coverage and watch mode

`$ bun test`](https://bun.com/docs/cli/test)

* ✓[Jest-compatible expect() API](https://bun.com/docs/cli/test)
* ✓[Snapshot testing](https://bun.com/docs/cli/test#snapshot)
* ✓[Watch mode & lifecycle hooks](https://bun.com/docs/cli/test#watch-mode)
* ✓[DOM APIs via happy-dom](https://bun.com/docs/cli/test#dom)
* ✓Concurrent test execution
* ✓[Built-in code coverage](https://bun.com/docs/cli/test#coverage)

[### Bundler

Replaces Vite and esbuild

Bundle TypeScript, JSX, React & CSS for both browsers and servers

`$ bun build ./app.tsx`](https://bun.com/docs/bundler)

* ✓[TypeScript & JSX built-in (no config)](https://bun.com/docs/bundler)
* ✓[CSS imports & bundling](https://bun.com/docs/bundler/loaders)
* ✓React support out of the box
* ✓[Build for the browser, Bun, and Node.js](https://bun.com/docs/bundler)
* ✓[Single-file executables](https://bun.com/docs/bundler/executables)
* ✓[.html, .css, .ts, .tsx, .jsx & more](https://bun.com/docs/bundler/loaders)

## Who uses Bun?

### Claude Code uses Bun

Bun's [single file executables](https://bun.com/docs/bundler/executables) & fast start times are great for CLIs.

[Learn about single file executables](https://bun.com/docs/bundler/executables)

[![](/bun-homepage-cc-boris-poster.jpg)](/bun-homepage-cc-boris_1080p.mp4)

[![](/bun-homepage-railway-jake-poster.jpg)](/bun-homepage-railway-jake_1080p.mp4)

### Railway Functions powered by Bun

Bun's all-in-one toolkit makes Railway's serverless functions fast and easy to use.

[Deploy on Railway](https://railway.com/new/function?utm_source=bun.com)

### Midjourney uses Bun

Bun's built-in [WebSocket server](https://bun.com/docs/api/websockets) helps Midjourney publish image generation notifications at scale.

[Learn about Bun's WebSocket server](https://bun.com/docs/api/websockets)

[![](/bun-homepage-midjourney-cheng-poster.jpg)](/bun-homepage-midjourney-cheng_1080p.mp4)

## What's different about Bun?

Bun provides extensive builtin APIs and tooling

|  |  |  |  |
| --- | --- | --- | --- |
| Builtin Core Features Essential runtime capabilities | Bun  Bun | Node | Deno |
| [Node.js compatibility  Aiming to be a drop-in replacement for Node.js apps](https://bun.com/docs/runtime/nodejs-apis) |  |  |  |
| [Web Standard APIs  Support for web standard APIs like `fetch`, `URL`, `EventTarget`, `Headers`, etc.](https://bun.com/docs/api/fetch) | Powered by WebCore (from WebKit/Safari) |  |  |
| [Native Addons  Call C-compatible native code from JavaScript](https://bun.com/docs/api/ffi) | Bun.ffi, NAPI, partial V8 C++ API |  |  |
| [TypeScript  First-class support, including `"paths"` `enum` `namespace`](https://bun.com/docs/runtime/typescript) |  |  |  |
| [JSX  First-class support without configuration](https://bun.com/docs/runtime/jsx) |  |  |  |
| [Module loader plugins  Plugin API for importing/requiring custom file types](https://bun.com/docs/runtime/plugins) | `Bun.plugin` works in browsers & Bun | 3 different loader APIs. Server-side only |  |
| Builtin APIs Built-in performance and native APIs designed for production | Bun  Bun | Node | Deno |
| [PostgreSQL, MySQL, and SQLite drivers  Connect to any SQL database with one fast, unified API](https://bun.com/docs/api/sql) | Fastest available, with query pipelining |  |  |
| [S3 Cloud Storage driver  Upload and download from S3-compatible storage, built-in](https://bun.com/docs/api/s3) | Fastest available |  |  |
| [Redis client  Redis client built into Bun with Pub/Sub support](https://bun.com/docs/api/redis) |  |  |  |
| [WebSocket server (including pub/sub)  WebSocket server built into `Bun.serve()` with backpressure handling](https://bun.com/docs/api/websockets) | `Bun.serve()` |  |  |
| [HTTP server  Lightning-fast HTTP server built into Bun](https://bun.com/docs/api/http) | Bun.serve() |  |  |
| [HTTP router  Route HTTP requests with dynamic paths and wildcards, built into `Bun.serve()`](https://bun.com/docs/api/http) | Bun.serve({routes: {'/api/:path': (req) => { ... }}}}) |  |  |
| [Single-file executables  Compile your app to a standalone executable that runs anywhere](https://bun.com/docs/bundler/executables) | bun build --compile with cross-compilation & code signing | No native addons, embedded files, cross-compilation or bytecode. Multi-step process. | No native addons, no cross-compilation |
| [YAML  YAML is a first-class citizen in Bun, just like JSON](https://bun.com/docs/api/yaml) | Bun.YAML & import from .yaml files |  |  |
| [Cookies API  Parse and set cookies with zero overhead using a Map-like API](https://bun.com/docs/api/cookie) | request.cookies Map-like API |  |  |
| [Encrypted Secrets Storage  Store secrets securely using your OS's native keychain](https://bun.com/docs/api/secrets) | Bun.secrets (Keychain/libsecret/Windows Credential Manager) |  |  |
| Builtin Tooling Built-in developer tooling | Bun  Bun | Node | Deno |
| [npm package management  Install, manage, and publish npm-compatible dependencies](https://bun.com/docs/cli/install) | With catalogs, isolated installs, bun audit, bun why |  | Limited features |
| [Bundler  Build production-ready code for frontend & backend](https://bun.com/docs/bundler) | Bun.build |  |  |
| [Cross-platform $ shell API  Native bash-like shell for cross-platform shell scripting](https://bun.com/docs/runtime/shell) | `Bun.$` |  | Requires 'dax' |
| [Jest-compatible test runner  Testing library compatible with the most popular testing framework](https://bun.com/docs/cli/test) | bun test with VS Code integration & concurrent execution |  |  |
| [Hot reloading (server)  Reload your backend without disconnecting connections, preserving state](https://bun.com/docs/runtime/hot) | bun --hot |  |  |
| [Monorepo support  Install workspaces packages and run commands across workspaces](https://bun.com/docs/cli/filter) | bun run --filter=package-glob ... |  |  |
| [Frontend Development Server  Run modern frontend apps with a fully-featured dev server](https://bun.com/docs/bundler/html) | bun ./index.html |  |  |
| Formatter & Linter  Built-in formatter and linter |  |  |  |
| Builtin Utilities APIs that make your life easier as a developer | Bun  Bun | Node | Deno |
| [Password & Hashing APIs  `bcrypt`, `argon2`, and non-cryptographic hash functions](https://bun.com/docs/api/hashing) | `Bun.password` & `Bun.hash` |  |  |
| [String Width API  Calculate the width of a string as displayed in the terminal](https://bun.com/docs/api/utils) | Bun.stringWidth |  |  |
| [Glob API  Glob patterns for file matching](https://bun.com/docs/api/glob) | Bun.Glob | fs.promises.glob |  |
| [Semver API  Compare and sort semver strings](https://bun.com/docs/api/semver) | Bun.semver |  |  |
| [CSS color conversion API  Convert between CSS color formats](https://bun.com/docs/api/color) | Bun.color |  |  |
| CSRF API  Generate and verify CSRF tokens | Bun.CSRF |  |  |

## Everything you need to build & ship

Production-ready APIs and tools, built into Bun

### HTTP & WebSockets

* [`Bun.serve()`

  HTTP & WebSocket server](https://bun.com/docs/api/http)
* [`routes`

  Built-in routing with dynamic paths](https://bun.com/docs/api/http#routing)
* [`request.cookies`

  Zero-overhead cookie parsing](https://bun.com/docs/api/cookie)

### Databases

* [`Bun.sql`

  PostgreSQL, MySQL, SQLite](https://bun.com/docs/api/sql)
* [`Bun.s3`

  S3-compatible cloud storage](https://bun.com/docs/api/s3)
* [`Bun.redis`

  Redis client with Pub/Sub](https://bun.com/docs/api/redis)

### File System

* [`Bun.file()`

  Fast file reading & streaming](https://bun.com/docs/api/file-io)
* [`Bun.Glob`

  Fast file pattern matching](https://bun.com/docs/api/glob)
* [`Bun.write()`

  Write files efficiently](https://bun.com/docs/api/file-io#writing-files)

### Testing

* [`bun test`

  Jest-compatible test runner](https://bun.com/docs/cli/test)
* [`snapshots`

  Snapshot testing built-in](https://bun.com/docs/cli/test#snapshot)
* [`expect()`

  Jest-compatible assertions](https://bun.com/docs/cli/test#matchers)

### Build & Deploy

* [`bun build`

  Fast bundler with tree-shaking](https://bun.com/docs/bundler)
* [`--compile`

  Single-file executables](https://bun.com/docs/bundler/executables)
* [`--hot`

  Hot reload without restarts](https://bun.com/docs/runtime/hot)

### TypeScript & DX

* [`TypeScript & JSX`

  No config required](https://bun.com/docs/runtime/typescript)
* [`import "*.yaml"`

  YAML & TOML imports](https://bun.com/docs/api/yaml)
* [`import "*.css"`

  CSS & asset imports](https://bun.com/docs/bundler/loaders)

### Security

* [`Bun.password`

  bcrypt, argon2 hashing](https://bun.com/docs/api/hashing)
* [`Bun.CSRF`

  CSRF token generation](https://bun.com/docs/api/csrf)
* [`Bun.secrets`

  OS keychain integration](https://bun.com/docs/api/secrets)

### System Integration

* [`Bun.$`

  Cross-platform shell scripting](https://bun.com/docs/runtime/shell)
* [`Bun.spawn()`

  Spawn child processes](https://bun.com/docs/api/spawn)
* [`bun:ffi`

  Call native C/C++ libraries](https://bun.com/docs/api/ffi)

### Utilities

* [`Bun.hash()`

  Fast hashing utilities](https://bun.com/docs/api/hashing)
* [`Bun.semver`

  Version comparison](https://bun.com/docs/api/semver)
* [`Bun.escapeHTML()`

  HTML escaping & sanitization](https://bun.com/docs/api/utils)

$ bun run

## Bun is a JavaScript runtime.

Bun is a new JavaScript runtime built from scratch to serve the modern JavaScript ecosystem. It has three major design goals:

* **Speed.** Bun starts fast and runs fast. It extends JavaScriptCore, the performance-minded JS engine built for Safari. Fast start times mean fast apps and fast APIs.
* **Elegant APIs.** Bun provides a minimal set of highly-optimized APIs for performing common tasks, like starting an HTTP server and writing files.
* **Cohesive DX.** Bun is a complete toolkit for building JavaScript apps, including a package manager, test runner, and bundler.

Bun is designed as a drop-in replacement for Node.js. It natively implements thousands of Node.js and Web APIs, including `fs`, `path`, `Buffer` and more.

The goal of Bun is to run most of the world's server-side JavaScript and provide tools to improve performance, reduce complexity, and multiply developer productivity.

## Bun works with Next.js

[![](/bun-homepage-cursor-leerob-1-poster.jpg)](/bun-homepage-cursor-leerob-1_1080p.mp4)

### Lee Robinson

VP of Developer Experience at Cursor (Anysphere)

app/blog/[slug]/page.tsx

import { s3, $, sql } from "bun";

export default async function BlogPage({ params }) {

const [post] = await sql`

SELECT title, image\_key, content

FROM posts

WHERE slug = ${params.slug}

`;

const imgUrl = s3.file(post.image\_key).presign({•••expiresIn: 3600 });

const wordCount = await $`echo ${post.content} | wc -w`;

return (

<div>

<h1>{post.title}</h1>

<img src={imgUrl} />

<p>Word count: {wordCount}</p>

</div>

);

}

## Full speed full-stack

Fast frontend apps with Bun's built-in high performance development server and production bundler. You've *never* seen hot-reloading this fast!

### Develop and ship frontend apps

Bun's built-in bundler and dev server make frontend development fast and simple. Develop with instant hot reload, then ship optimized production builds—all with zero configuration.

$ bun init --react

#### Start a dev server

Run `bun ./index.html` to start a dev server. TypeScript, JSX, React, and CSS imports work out of the box.

#### Hot Module Replacement

Built-in HMR preserves application state during development. Changes appear instantly—no manual refresh needed.

#### Build for production

Build optimized bundles with `bun build ./index.html --production`. Tree-shaking, minification, and code splitting work out of the box.

[Learn more about frontend with Bun →](https://bun.com/docs/bundler/html)

[](/bun-frontend-hmr-demo.mp4)

$ bun install

## Bun is an npm-compatible package manager.

Bun

pnpm

*17x slower*

npm

*29x slower*

Yarn

*33x slower*

Installing dependencies from cache for a Remix app.   
[View benchmark](https://github.com/oven-sh/bun/tree/main/bench/install)

Replace `yarn` with `bun install` to get 30x faster package installs.

$ bun test

## Bun is a test runner that makes the rest look like test walkers.

Bun

Vitest

*5x slower*

Jest+SWC

*8x slower*

Jest+tsjest

*18x slower*

Jest+Babel

*20x slower*

Replace `jest` with `bun test` to run your tests 10-30x faster.

## The APIs you need. Baked in.

Start an HTTP server

Start a WebSocket server

Read and write files

Hash a password

Frontend dev server

Write a test

Query PostgreSQL

Use Redis

Import YAML

Set cookies

Run a shell script

Call a C function

index.tsx

```
import { sql, serve } from "bun";

const server = serve({
  port: 3000,
  routes: {
    "/": new Response("Welcome to Bun!"),
    "/api/users": async (req) => {
      const users = await sql`SELECT * FROM users LIMIT 10`;
      return Response.json({ users });
    },
  },
});

console.log(`Listening on localhost:${server.port}`);
```

index.tsx

```
const server = Bun.serve<{ authToken: string; }>({
  fetch(req, server) {
    // use a library to parse cookies
    const cookies = parseCookies(req.headers.get("Cookie"));
    server.upgrade(req, {
      data: { authToken: cookies['X-Token'] },
    });
  },
  websocket: {
    // handler called when a message is received
    async message(ws, message) {
      console.log(`Received: ${message}`);
      const user = getUserFromToken(ws.data.authToken);
      await db.Message.insert({
        message: String(message),
        userId: user.id,
      });
    },
  },
});

console.log(`Listening on localhost:${server.port}`);
```

index.tsx

```
const file = Bun.file(import.meta.dir + '/package.json'); // BunFile

const pkg = await file.json(); // BunFile extends Blob
pkg.name = 'my-package';
pkg.version = '1.0.0';

await Bun.write(file, JSON.stringify(pkg, null, 2));
```

index.tsx

```
const password = "super-secure-pa$$word";

const hash = await Bun.password.hash(password);
// => $argon2id$v=19$m=65536,t=2,p=1$tFq+9AVr1bfPxQdh...

const isMatch = await Bun.password.verify(password, hash);
// => true
```

server.ts

```
// Run 'bun init --react' to get started
import { serve } from "bun";
import reactApp from "./index.html";

serve({
  port: 3000,
  routes: {
    "/": reactApp,
    "/api/hello": () => Response.json({ message: "Hello!" }),
  },
  development: {
    console: true, // Stream browser logs to terminal
    hmr: true, // Enable hot module reloading
  },
});
```

index.test.tsx

```
import { test, expect } from "bun:test";

// Run tests concurrently for better performance
test.concurrent("fetch user 1", async () => {
  const res = await fetch("https://api.example.com/users/1");
  expect(res.status).toBe(200);
});

test.concurrent("fetch user 2", async () => {
  const res = await fetch("https://api.example.com/users/2");
  expect(res.status).toBe(200);
});

test("addition", () => {
  expect(2 + 2).toBe(4);
});
```

index.tsx

```
import { sql } from "bun";

// Query with automatic SQL injection prevention
const users = await sql`
  SELECT * FROM users
  WHERE active = ${true}
  LIMIT 10
`;

// Insert with object notation
const [user] = await sql`
  INSERT INTO users ${sql({
    name: "Alice",
    email: "alice@example.com"
  })}
  RETURNING *
`;
```

config.yaml

```
// Import YAML files directly
import config from "./config.yaml";

console.log(config.database.host);
// => "localhost"

// Or parse YAML at runtime
const data = Bun.YAML.parse(`
name: my-app
version: 1.0.0
database:
  host: localhost
  port: 5432
`);
```

index.tsx

```
import { serve } from "bun";

serve({
  port: 3000,
  routes: {
    "/": (request) => {
      // Read cookies with built-in parsing
      const sessionId = request.cookies.get("session_id");

      // Set cookies
      request.cookies.set("session_id", "abc123", {
        path: "/",
        httpOnly: true,
        secure: true,
      });

      return Response.json({ success: true });
    },
  },
});
```

index.tsx

```
import { redis } from "bun";

// Set a key
await redis.set("greeting", "Hello from Bun!");

console.log(db.query("SELECT 1 as x").get());
// { x: 1 }
```

index.tsx

```
import { $ } from 'bun';

// Run a shell command (also works on Windows!)
await $`echo "Hello, world!"`;

const response = await fetch("https://example.com");

// Pipe the response body to gzip
const data = await $`gzip < ${response}`.arrayBuffer();
```

index.tsx

```
import { dlopen, FFIType, suffix } from "bun:ffi";

// `suffix` is either "dylib", "so", or "dll" depending on the platform
const path = `libsqlite3.${suffix}`;

const {
  symbols: {
    sqlite3_libversion, // the function to call
  },
} = dlopen(path, {
  sqlite3_libversion: {
    args: [], // no arguments
    returns: FFIType.cstring, // returns a string
  },
});

console.log(`SQLite 3 version: ${sqlite3_libversion()}`);
```

## Learn more

[### Documentation

Get started with Bun and learn how to use all of its features](https://bun.com/docs)[### API Reference

Explore the complete API reference for Bun's runtime and toolkit](https://bun.com/docs/api)

## Developers love Bun.

Sainder

Jan 17

@Sainder\_Pradipt

Bun

Lic

Jan 18

@Lik228

bun

Martin Navrátil

Jan 17

@martin\_nav\_

Bun....

SaltyAom

Jan 17

@saltyAom

bun

reaxios

Jan 17

@reaxios

bun install bun

kyge

Jan 17

@0xkyge

bun

James Landrum

Jan 17

@JamesRLandrum

Node

orlowdev

Jan 17

@orlowdev

Yeah, bun, but my code does not have dependencies.

hola

Jan 17

@jdggggyujhbc

bun

std::venom

Jan 17

@std\_venom

Bun

tiago

Jan 19

@tiagorangel23

should have used Bun instead of npm

Sainder

Jan 17

@Sainder\_Pradipt

Bun

Lic

Jan 18

@Lik228

bun

Martin Navrátil

Jan 17

@martin\_nav\_

Bun....

SaltyAom

Jan 17

@saltyAom

bun

reaxios

Jan 17

@reaxios

bun install bun

kyge

Jan 17

@0xkyge

bun

James Landrum

Jan 17

@JamesRLandrum

Node

orlowdev

Jan 17

@orlowdev

Yeah, bun, but my code does not have dependencies.

hola

Jan 17

@jdggggyujhbc

bun

std::venom

Jan 17

@std\_venom

Bun

tiago

Jan 19

@tiagorangel23

should have used Bun instead of npm

46officials

Jan 19

@46officials

Bun

yuki

Jan 19

@staticdots

Bun

Stefan

Jan 17

@stefangarofalo

Bun

Samuel

Jan 17

@samueldans0

Bun always

Divin Prince

Jan 17

@divinprnc

Yeah Bun

Gibson

Jan 16

@GibsonSMurray

bun

Oggie Sutrisna

Jan 16

@oggiesutrisna

bun

emanon

Jan 16

@0x\_emanon

✅ bun

yuki

Jan 16

@staticdots

bun

SpiritBear

Jan 16

@0xSpiritBear

bun

Ayu

Jan 12

@Ayuu2809

Bun good 🧅

46officials

Jan 19

@46officials

Bun

yuki

Jan 19

@staticdots

Bun

Stefan

Jan 17

@stefangarofalo

Bun

Samuel

Jan 17

@samueldans0

Bun always

Divin Prince

Jan 17

@divinprnc

Yeah Bun

Gibson

Jan 16

@GibsonSMurray

bun

Oggie Sutrisna

Jan 16

@oggiesutrisna

bun

emanon

Jan 16

@0x\_emanon

✅ bun

yuki

Jan 16

@staticdots

bun

SpiritBear

Jan 16

@0xSpiritBear

bun

Ayu

Jan 12

@Ayuu2809

Bun good 🧅

Hirbod

Jan 19

@hirbod\_dev

For everything. Yes. I even run with bunx expo run:ios etc

Luis Paolini

Jan 18

@DigitalLuiggi

Jus use @bunjavascript

buraks

Jan 18

@buraks\_\_\_\_

I use bun patch and I love it!

fahadali

Jan 8

@fahadali503

Bun

Aiden Bai

Jan 1

@aidenybai

2025 will be the year of JS/TS and @bunjavascript is why

Catalin

Jan 1

@catalinmpit

Bun is goated

MadMax

Jan 3

@dr\_\_madmax

@bunjavascript is yet to get enough appreciation it deserves.

Baggi/e

Jan 3

@ManiSohi

Performant TS/JS backend needs more love
Elysia for the win

Michael Feldstein

Dec 18

@msfeldstein

holy shit bun is the solution to spending all day mucking around with typescript/module/commonjs/import bullshit and just running scripts

Hirbod

Jan 19

@hirbod\_dev

For everything. Yes. I even run with bunx expo run:ios etc

Luis Paolini

Jan 18

@DigitalLuiggi

Jus use @bunjavascript

buraks

Jan 18

@buraks\_\_\_\_

I use bun patch and I love it!

fahadali

Jan 8

@fahadali503

Bun

Aiden Bai

Jan 1

@aidenybai

2025 will be the year of JS/TS and @bunjavascript is why

Catalin

Jan 1

@catalinmpit

Bun is goated

MadMax

Jan 3

@dr\_\_madmax

@bunjavascript is yet to get enough appreciation it deserves.

Baggi/e

Jan 3

@ManiSohi

Performant TS/JS backend needs more love
Elysia for the win

Michael Feldstein

Dec 18

@msfeldstein

holy shit bun is the solution to spending all day mucking around with typescript/module/commonjs/import bullshit and just running scripts