---
url: https://bun.com/docs/guides/runtime/set-env
title: Set environment variables - Bun
source_domain: bun.com
---

# Set environment variables - Bun

The current environment variables can be accessed via `process.env` or `Bun.env`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
Bun.env.API_TOKEN; // => "secret"
process.env.API_TOKEN; // => "secret"
```

---

Set these variables in a `.env` file.
Bun reads the following files automatically (listed in order of increasing precedence).

* `.env`
* `.env.production`, `.env.development`, `.env.test` (depending on value of `NODE_ENV`)
* `.env.local` (not loaded when `NODE_ENV=test`)

.env

Copy

```
FOO=hello
BAR=world
```

---

Variables can also be set via the command line.

Copy

```
FOO=helloworld bun run dev
```

---

See [Docs > Runtime > Environment variables](https://bun.com/docs/runtime/environment-variables) for more information on using environment variables with Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/runtime/set-env.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/runtime/set-env)

⌘I