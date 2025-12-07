---
url: https://bun.com/docs/guides/ecosystem/elysia
title: Build an HTTP server using Elysia and Bun - Bun
source_domain: bun.com
---

# Build an HTTP server using Elysia and Bun - Bun

[Elysia](https://elysiajs.com) is a Bun-first performance focused web framework that takes full advantage of Bun’s HTTP, file system, and hot reloading APIs. Get started with `bun create`.

terminal

Copy

```
bun create elysia myapp
cd myapp
bun run dev
```

---

To define a simple HTTP route and start a server with Elysia:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)server.ts

Copy

```
import { Elysia } from "elysia";

const app = new Elysia().get("/", () => "Hello Elysia").listen(8080);

console.log(`🦊 Elysia is running at on port ${app.server?.port}...`);
```

---

Elysia is a full-featured server framework with Express-like syntax, type inference, middleware, file uploads, and plugins for JWT authentication, tRPC, and more. It’s also is one of the [fastest Bun web frameworks](https://github.com/SaltyAom/bun-http-framework-benchmark).
Refer to the Elysia [documentation](https://elysiajs.com/quick-start.html) for more information.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/ecosystem/elysia.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/ecosystem/elysia)

⌘I