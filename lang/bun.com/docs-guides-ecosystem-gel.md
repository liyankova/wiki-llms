---
url: https://bun.com/docs/guides/ecosystem/gel
title: Use Gel with Bun - Bun
source_domain: bun.com
---

# Use Gel with Bun - Bun

Gel (formerly EdgeDB) is a graph-relational database powered by Postgres under the hood. It provides a declarative schema language, migrations system, and object-oriented query language, in addition to supporting raw SQL queries. It solves the object-relational mapping problem at the database layer, eliminating the need for an ORM library in your application code.

---

First, [install Gel](https://docs.geldata.com/learn/installation) if you haven’t already.

Copy

```
curl https://www.geldata.com/sh --proto "=https" -sSf1 | sh
```

---

Use `bun init` to create a fresh project.

terminal

Copy

```
mkdir my-edgedb-app
cd my-edgedb-app
bun init -y
```

---

We’ll use the Gel CLI to initialize a Gel instance for our project. This creates a `gel.toml` file in our project root.

terminal

Copy

```
gel project init
```

Copy

```
No `gel.toml` found in `/Users/colinmcd94/Documents/bun/fun/examples/my-gel-app` or above
Do you want to initialize a new project? [Y/n]
> Y
Specify the name of Gel instance to use with this project [default: my_gel_app]:
> my_gel_app
Checking Gel versions...
Specify the version of Gel to use with this project [default: x.y]:
> x.y
┌─────────────────────┬──────────────────────────────────────────────────────────────────┐
│ Project directory   │ /Users/colinmcd94/Documents/bun/fun/examples/my-gel-app         │
│ Project config      │ /Users/colinmcd94/Documents/bun/fun/examples/my-gel-app/gel.toml│
│ Schema dir (empty)  │ /Users/colinmcd94/Documents/bun/fun/examples/my-gel-app/dbschema│
│ Installation method │ portable package                                                 │
│ Version             │ x.y+6d5921b                                                      │
│ Instance name       │ my_gel_app                                                       │
└─────────────────────┴──────────────────────────────────────────────────────────────────┘
Version x.y+6d5921b is already downloaded
Initializing Gel instance...
Applying migrations...
Everything is up to date. Revision initial
Project initialized.
To connect to my_gel_app, run `gel`
```

---

To see if the database is running, let’s open a REPL and run a simple query.

terminal

Copy

```
gel
gel> select 1 + 1;
```

Copy

```
2
```

Then run `\quit` to exit the REPL.

terminal

Copy

```
gel> \quit
```

---

With the project initialized, we can define a schema. The `gel project init` command already created a `dbschema/default.esdl` file to contain our schema.

File Tree

Copy

```
dbschema
├── default.esdl
└── migrations
```

---

Open that file and paste the following contents.

default.esdl

Copy

```
module default {
  type Movie {
    required title: str;
    releaseYear: int64;
  }
};
```

---

Then generate and apply an initial migration.

terminal

Copy

```
gel migration create
```

Copy

```
Created /Users/colinmcd94/Documents/bun/fun/examples/my-gel-app/dbschema/migrations/00001.edgeql, id: m1uwekrn4ni4qs7ul7hfar4xemm5kkxlpswolcoyqj3xdhweomwjrq
```

terminal

Copy

```
gel migrate
```

Copy

```
Applied m1uwekrn4ni4qs7ul7hfar4xemm5kkxlpswolcoyqj3xdhweomwjrq (00001.edgeql)
```

---

With our schema applied, let’s execute some queries using Gel’s JavaScript client library. We’ll install the client library and Gel’s codegen CLI, and create a `seed.ts`.file.

terminal

Copy

```
bun add gel
bun add -D @gel/generate
touch seed.ts
```

---

Paste the following code into `seed.ts`.
The client auto-connects to the database. We insert a couple movies using the `.execute()` method. We will use EdgeQL’s `for` expression to turn this bulk insert into a single optimized query.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)seed.ts

Copy

```
import { createClient } from "gel";

const client = createClient();

const INSERT_MOVIE = `
  with movies := <array<tuple<title: str, year: int64>>>$movies
  for movie in array_unpack(movies) union (
    insert Movie {
      title := movie.title,
      releaseYear := movie.year,
    }
  )
`;

const movies = [
  { title: "The Matrix", year: 1999 },
  { title: "The Matrix Reloaded", year: 2003 },
  { title: "The Matrix Revolutions", year: 2003 },
];

await client.execute(INSERT_MOVIE, { movies });

console.log(`Seeding complete.`);
process.exit();
```

---

Then run this file with Bun.

terminal

Copy

```
bun run seed.ts
```

Copy

```
Seeding complete.
```

---

Gel implements a number of code generation tools for TypeScript. To query our newly seeded database in a typesafe way, we’ll use `@gel/generate` to code-generate the EdgeQL query builder.

terminal

Copy

```
bunx @gel/generate edgeql-js
```

Copy

```
Generating query builder...
Detected tsconfig.json, generating TypeScript files.
   To override this, use the --target flag.
   Run `npx @edgedb/generate --help` for full options.
Introspecting database schema...
Writing files to ./dbschema/edgeql-js
Generation complete! 🤘
Checking the generated query builder into version control
is not recommended. Would you like to update .gitignore to ignore
the query builder directory? The following line will be added:

   dbschema/edgeql-js

[y/n] (leave blank for "y")
> y
```

---

In `index.ts`, we can import the generated query builder from `./dbschema/edgeql-js` and write a simple select query.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
import { createClient } from "gel";
import e from "./dbschema/edgeql-js";

const client = createClient();

const query = e.select(e.Movie, () => ({
  title: true,
  releaseYear: true,
}));

const results = await query.run(client);
console.log(results);

results; // { title: string, releaseYear: number | null }[]
```

---

Running the file with Bun, we can see the list of movies we inserted.

terminal

Copy

```
bun run index.ts
```

Copy

```
[
  {
    title: "The Matrix",
    releaseYear: 1999
  }, {
    title: "The Matrix Reloaded",
    releaseYear: 2003
  }, {
    title: "The Matrix Revolutions",
    releaseYear: 2003
  }
]
```

---

For complete documentation, refer to the [Gel docs](https://docs.geldata.com/).

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/ecosystem/gel.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/ecosystem/gel)

⌘I