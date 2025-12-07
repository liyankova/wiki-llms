---
url: https://bun.com/docs/guides/ecosystem/express
title: Build an HTTP server using Express and Bun - Bun
source_domain: bun.com
---

# Build an HTTP server using Express and Bun - Bun

Express and other major Node.js HTTP libraries should work out of the box. Bun implements the [`node:http`](https://nodejs.org/api/http.html) and [`node:https`](https://nodejs.org/api/https.html) modules that these libraries rely on.

Refer to the [Runtime > Node.js APIs](https://bun.com/docs/runtime/nodejs-compat#node-http) page for more detailed compatibility
information.

terminal

Copy

```
bun add express
```

---

To define a simple HTTP route and start a server with Express:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)server.ts

Copy

```
import express from "express";

const app = express();
const port = 8080;

app.get("/", (req, res) => {
  res.send("Hello World!");
});

app.listen(port, () => {
  console.log(`Listening on port ${port}...`);
});
```

---

To start the server on `localhost`:

terminal

Copy

```
bun server.ts
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/ecosystem/express.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/ecosystem/express)

⌘I