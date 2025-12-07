---
url: https://bun.com/docs/guides/http/cluster
title: Start a cluster of HTTP servers - Bun
source_domain: bun.com
---

# Start a cluster of HTTP servers - Bun

To run multiple HTTP servers concurrently, use the `reusePort` option in `Bun.serve()` which shares the same port across multiple processes.
This automatically load balances incoming requests across multiple instances of Bun.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)server.ts

Copy

```
import { serve } from "bun";

const id = Math.random().toString(36).slice(2);

serve({
  port: process.env.PORT || 8080,
  development: false,

  // Share the same port across multiple processes
  // This is the important part!
  reusePort: true,

  async fetch(request) {
    return new Response("Hello from Bun #" + id + "!\n");
  },
});
```

---

**Linux only** — Windows and macOS ignore the `reusePort` option. This is an operating system limitation with
`SO_REUSEPORT`, unfortunately.

After saving the file, start your servers on the same port.
Under the hood, this uses the Linux `SO_REUSEPORT` and `SO_REUSEADDR` socket options to ensure fair load balancing across multiple processes. [Learn more about `SO_REUSEPORT` and `SO_REUSEADDR`](https://lwn.net/Articles/542629/)

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)cluster.ts

Copy

```
import { spawn } from "bun";

const cpus = navigator.hardwareConcurrency; // Number of CPU cores
const buns = new Array(cpus);

for (let i = 0; i < cpus; i++) {
  buns[i] = spawn({
    cmd: ["bun", "./server.ts"],
    stdout: "inherit",
    stderr: "inherit",
    stdin: "inherit",
  });
}

function kill() {
  for (const bun of buns) {
    bun.kill();
  }
}

process.on("SIGINT", kill);
process.on("exit", kill);
```

---

Bun has also implemented the `node:cluster` module, but this is a faster, simple, and limited alternative.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/http/cluster.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/http/cluster)

⌘I