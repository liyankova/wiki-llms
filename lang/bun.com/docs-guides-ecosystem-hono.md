---
url: https://bun.com/docs/guides/ecosystem/hono
title: Build an HTTP server using Hono and Bun - Bun
source_domain: bun.com
---

# Build an HTTP server using Hono and Bun - Bun

[Hono](https://github.com/honojs/hono) is a lightweight ultrafast web framework designed for the edge.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)server.ts

Copy

```
import { Hono } from "hono";
const app = new Hono();

app.get("/", c => c.text("Hono!"));

export default app;
```

---

Use `create-hono` to get started with one of Hono’s project templates. Select `bun` when prompted for a template.

terminal

Copy

```
bun create hono myapp
```

Copy

```
✔ Which template do you want to use? › bun
cloned honojs/starter#main to /path/to/myapp
✔ Copied project files
```

terminal

Copy

```
cd myapp
bun install
```

---

Then start the dev server and visit [localhost:3000](http://localhost:3000).

terminal

Copy

```
bun run dev
```

---

Refer to Hono’s guide on [getting started with Bun](https://hono.dev/getting-started/bun) for more information.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/ecosystem/hono.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/ecosystem/hono)

⌘I