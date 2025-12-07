---
url: https://bun.com/docs/runtime/node-api
title: Node-API - Bun
source_domain: bun.com
---

# Node-API - Bun

Node-API is an interface for building native add-ons to Node.js. Bun implements 95% of this interface from scratch, so most existing Node-API extensions will work with Bun out of the box. Track the completion status of it in [this issue](https://github.com/oven-sh/bun/issues/158).
As in Node.js, `.node` files (Node-API modules) can be required directly in Bun.

Copy

```
const napi = require("./my-node-module.node");
```

Alternatively, use `process.dlopen`:

Copy

```
let mod = { exports: {} };
process.dlopen(mod, "./my-node-module.node");
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/runtime/node-api.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /runtime/node-api)

⌘I