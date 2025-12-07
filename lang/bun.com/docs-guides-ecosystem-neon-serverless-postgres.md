---
url: https://bun.com/docs/guides/ecosystem/neon-serverless-postgres
title: Use Neon's Serverless Postgres with Bun - Bun
source_domain: bun.com
---

# Use Neon's Serverless Postgres with Bun - Bun

[Neon](https://neon.tech/) is a fully managed serverless Postgres. Neon separates compute and storage to offer modern developer features such as autoscaling, branching, bottomless storage, and more.

---

Get started by creating a project directory, initializing the directory using `bun init`, and adding the [Neon serverless driver](https://github.com/neondatabase/serverless/) as a project dependency.

terminal

Copy

```
mkdir bun-neon-postgres
cd bun-neon-postgres
bun init -y
bun add @neondatabase/serverless
```

---

Create a `.env.local` file and add your [Neon Postgres connection string](https://neon.tech/docs/connect/connect-from-any-app) to it.

.env.local

Copy

```
DATABASE_URL=postgresql://usertitle:[email protected]/neondb?sslmode=require
```

---

Paste the following code into your project’s `index.ts` file.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
import { neon } from "@neondatabase/serverless";

// Bun automatically loads the DATABASE_URL from .env.local
// Refer to: https://bun.com/docs/runtime/environment-variables for more information
const sql = neon(process.env.DATABASE_URL);

const rows = await sql`SELECT version()`;

console.log(rows[0].version);
```

---

Start the program using `bun ./index.ts`. The Postgres version should be printed to the console.

terminal

Copy

```
bun ./index.ts
```

Copy

```
PostgreSQL 16.2 on x86_64-pc-linux-gnu, compiled by gcc (Debian 10.2.1-6) 10.2.1 20210110, 64-bit
```

---

This example used the Neon serverless driver’s SQL-over-HTTP functionality. Neon’s serverless driver also exposes `Client` and `Pool` constructors to enable sessions, interactive transactions, and node-postgres compatibility.
Refer to [Neon’s documentation](https://neon.tech/docs/serverless/serverless-driver) for a complete overview of the serverless driver.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/ecosystem/neon-serverless-postgres.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/ecosystem/neon-serverless-postgres)

⌘I