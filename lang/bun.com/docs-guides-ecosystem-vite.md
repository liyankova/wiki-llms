---
url: https://bun.com/docs/guides/ecosystem/vite
title: Build a frontend using Vite and Bun - Bun
source_domain: bun.com
---

# Build a frontend using Vite and Bun - Bun

You can use Vite with Bun, but many projects get faster builds & drop hundreds of dependencies by switching to [HTML
imports](https://bun.com/docs/bundler/html-static).

---

Vite works out of the box with Bun. Get started with one of Vite’s templates.

terminal

Copy

```
bun create vite my-app
```

Copy

```
✔ Select a framework: › React
✔ Select a variant: › TypeScript + SWC
Scaffolding project in /path/to/my-app...
```

---

Then `cd` into the project directory and install dependencies.

terminal

Copy

```
cd my-app
bun install
```

---

Start the development server with the `vite` CLI using `bunx`.
The `--bun` flag tells Bun to run Vite’s CLI using `bun` instead of `node`; by default Bun respects Vite’s `#!/usr/bin/env node` [shebang line](https://en.wikipedia.org/wiki/Shebang_(Unix)).

terminal

Copy

```
bunx --bun vite
```

---

To simplify this command, update the `"dev"` script in `package.json` to the following.

package.json

Copy

```
  "scripts": {
    "dev": "vite", 
    "dev": "bunx --bun vite", 
    "build": "vite build",
    "serve": "vite preview"
  },
  // ...
```

---

Now you can start the development server with `bun run dev`.

terminal

Copy

```
bun run dev
```

---

The following command will build your app for production.

terminal

Copy

```
bunx --bun vite build
```

---

This is a stripped down guide to get you started with Vite + Bun. For more information, see the [Vite documentation](https://vite.dev/guide/).

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/ecosystem/vite.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/ecosystem/vite)

⌘I