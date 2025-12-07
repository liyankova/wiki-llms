---
url: https://bun.com/docs/guides/ecosystem/stric
title: Build an HTTP server using StricJS and Bun - Bun
source_domain: bun.com
---

# Build an HTTP server using StricJS and Bun - Bun

[StricJS](https://github.com/bunsvr) is a Bun framework for building high-performance web applications and APIs.

* **Fast** — Stric is one of the fastest Bun frameworks. See [benchmark](https://github.com/bunsvr/benchmark) for more details.
* **Minimal** — The basic components like `@stricjs/router` and `@stricjs/utils` are under 50kB and require no external dependencies.
* **Extensible** — Stric includes with a plugin system, dependency injection, and optional optimizations for handling requests.

---

Use `bun init` to create an empty project.

terminal

Copy

```
mkdir myapp
cd myapp
bun init
bun add @stricjs/router @stricjs/utils
```

---

To implement a simple HTTP server with StricJS:

index.ts

Copy

```
import { Router } from "@stricjs/router";

export default new Router().get("/", () => new Response("Hi"));
```

---

To serve static files from `/public`:

index.ts

Copy

```
import { dir } from "@stricjs/utils";

export default new Router().get("/", () => new Response("Hi")).get("/*", dir("./public"));
```

---

Run the file in watch mode to start the development server.

terminal

Copy

```
bun --watch run index.ts
```

---

For more info, see Stric’s [documentation](https://stricjs.netlify.app).

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/ecosystem/stric.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/ecosystem/stric)

⌘I