---
url: https://bun.com/docs/guides/ecosystem/prisma
title: Use Prisma with Bun - Bun
source_domain: bun.com
---

# Use Prisma with Bun - Bun

**Note** — Prisma’s dynamic subcommand loading system currently requires npm to be installed alongside Bun. This
affects certain CLI commands like `prisma init`, `prisma migrate`, etc. Generated code works perfectly with Bun using
the new `prisma-client` generator.

1

Create a new project

Prisma works out of the box with Bun. First, create a directory and initialize it with `bun init`.

terminal

Copy

```
mkdir prisma-app
cd prisma-app
bun init
```

2

Install Prisma dependencies

Then install the Prisma CLI (`prisma`), Prisma Client (`@prisma/client`), and the LibSQL adapter as dependencies.

terminal

Copy

```
bun add -d prisma
bun add @prisma/client @prisma/adapter-libsql
```

3

Initialize Prisma with SQLite

We’ll use the Prisma CLI with `bunx` to initialize our schema and migration directory. For simplicity we’ll be using an in-memory SQLite database.

terminal

Copy

```
bunx --bun prisma init --datasource-provider sqlite
```

This creates a basic schema. We need to update it to use the new Rust-free client with Bun optimization. Open `prisma/schema.prisma` and modify the generator block, then add a simple `User` model.

![https://mintcdn.com/bun-1dd33a4e/ztkOKlOzC-ndb59O/icons/ecosystem/prisma.svg?fit=max&auto=format&n=ztkOKlOzC-ndb59O&q=85&s=e11053a2c03cc3eb38539358a21b28c9](https://mintcdn.com/bun-1dd33a4e/ztkOKlOzC-ndb59O/icons/ecosystem/prisma.svg?fit=max&auto=format&n=ztkOKlOzC-ndb59O&q=85&s=e11053a2c03cc3eb38539358a21b28c9)prisma/schema.prisma

Copy

```
  generator client {
    provider = "prisma-client"
    output = "./generated"
    engineType = "client"
    runtime = "bun"
  }

  datasource db {
    provider = "sqlite"
    url      = env("DATABASE_URL")
  }

  model User { 
    id    Int     @id @default(autoincrement()) 
    email String  @unique
    name  String?
  }
```

4

Create and run database migration

Then generate and run initial migration.This will generate a `.sql` migration file in `prisma/migrations`, create a new SQLite instance, and execute the migration against the new instance.

terminal

Copy

```
 bunx --bun prisma migrate dev --name init
```

Copy

```
Environment variables loaded from .env
Prisma schema loaded from prisma/schema.prisma
Datasource "db": SQLite database "dev.db" at "file:./dev.db"

SQLite database dev.db created at file:./dev.db

Applying migration `20251014141233_init`

The following migration(s) have been created and applied from new schema changes:

prisma/migrations/
 └─ 20251014141233_init/
   └─ migration.sql

Your database is now in sync with your schema.

✔ Generated Prisma Client (6.17.1) to ./generated in 18ms
```

5

Generate Prisma Client

As indicated in the output, Prisma re-generates our *Prisma client* whenever we execute a new migration. The client provides a fully typed API for reading and writing from our database. You can manually re-generate the client with the Prisma CLI.

terminal

Copy

```
bunx --bun prisma generate
```

6

Initialize Prisma Client with LibSQL

Now we need to create a Prisma client instance. Create a new file `prisma/db.ts` to initialize the PrismaClient with the LibSQL adapter.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)prisma/db.ts

Copy

```
import { PrismaClient } from "./generated/client";
import { PrismaLibSQL } from "@prisma/adapter-libsql";

const adapter = new PrismaLibSQL({ url: process.env.DATABASE_URL || "" });
export const prisma = new PrismaClient({ adapter });
```

7

Create a test script

Let’s write a simple script to create a new user, then count the number of users in the database.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
import { prisma } from "./prisma/db";

// create a new user
await prisma.user.create({
  data: {
    name: "John Dough",
    email: `john-${Math.random()}@example.com`,
  },
});

// count the number of users
const count = await prisma.user.count();
console.log(`There are ${count} users in the database.`);
```

8

Run and test the application

Let’s run this script with `bun run`. Each time we run it, a new user is created.

terminal

Copy

```
bun run index.ts
```

Copy

```
Created [email protected]
There are 1 users in the database.
```

terminal

Copy

```
bun run index.ts
```

Copy

```
Created [email protected]
There are 2 users in the database.
```

terminal

Copy

```
bun run index.ts
```

Copy

```
Created [email protected]
There are 3 users in the database.
```

---

That’s it! Now that you’ve set up Prisma using Bun, we recommend referring to the [official Prisma docs](https://www.prisma.io/docs/orm/prisma-client) as you continue to develop your application.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/ecosystem/prisma.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/ecosystem/prisma)

⌘I