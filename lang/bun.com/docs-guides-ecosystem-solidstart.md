---
url: https://bun.com/docs/guides/ecosystem/solidstart
title: Build an app with SolidStart and Bun - Bun
source_domain: bun.com
---

# Build an app with SolidStart and Bun - Bun

Initialize a SolidStart app with `create-solid`. You can specify the `--solidstart` flag to create a SolidStart project, and `--ts` for TypeScript support. When prompted for a template, select `basic` for a minimal starter app.

terminal

Copy

```
bun create solid my-app --solidstart --ts
```

Copy

```
┌
 Create-Solid v0.6.11
│
◇  Project Name
│  my-app
│
◇  Which template would you like to use?
│  basic
│
◇  Project created 🎉
│
◇  To get started, run: ─╮
│                        │
│  cd my-app             │
│  bun install           │
│  bun dev               │
│                        │
├────────────────────────╯
```

---

As instructed by the `create-solid` CLI, install the dependencies.

terminal

Copy

```
cd my-app
bun install
```

Then run the development server with `bun dev`.

terminal

Copy

```
bun dev
```

Copy

```
$ vinxi dev
vinxi v0.5.8
vinxi starting dev server

  ➜ Local:    http://localhost:3000/
  ➜ Network:  use --host to expose
```

Open [localhost:3000](http://localhost:3000). Any changes you make to `src/routes/index.tsx` will be hot-reloaded automatically.

---

Refer to the [SolidStart website](https://docs.solidjs.com/solid-start) for complete framework documentation.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/ecosystem/solidstart.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/ecosystem/solidstart)

⌘I