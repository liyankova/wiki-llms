---
url: https://bun.com/docs/guides/runtime/read-env
title: Read environment variables - Bun
source_domain: bun.com
---

# Read environment variables - Bun

The current environment variables can be accessed via `process.env`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
process.env.API_TOKEN; // => "secret"
```

---

Bun also exposes these variables via `Bun.env`, which is a simple alias of `process.env`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
Bun.env.API_TOKEN; // => "secret"
```

---

To print all currently-set environment variables to the command line, run `bun --print process.env`. This is useful for debugging.

terminal

Copy

```
bun --print process.env
```

Copy

```
BAZ=stuff
FOOBAR=aaaaaa
<lots more lines>
```

---

See [Docs > Runtime > Environment variables](https://bun.com/docs/runtime/environment-variables) for more information on using environment variables with Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/runtime/read-env.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/runtime/read-env)

⌘I