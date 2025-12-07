---
url: https://bun.com/docs/guides/ecosystem/remix
title: Build an app with Remix and Bun - Bun
source_domain: bun.com
---

# Build an app with Remix and Bun - Bun

Currently the Remix development server (`remix dev`) relies on Node.js APIs that Bun does not yet implement. The guide
below uses Bun to initialize a project and install dependencies, but it uses Node.js to run the dev server.

---

Initialize a Remix app with `create-remix`.

terminal

Copy

```
bun create remix
```

Copy

```
 remix   v1.19.3 💿 Let's build a better website...

   dir   Where should we create your new project?
         ./my-app

      ◼  Using basic template See https://remix.run/docs/en/main/guides/templates#templates for more
      ✔  Template copied

   git   Initialize a new git repository?
         Yes

  deps   Install dependencies with bun?
         Yes

      ✔  Dependencies installed
      ✔  Git initialized

  done   That's it!
         Enter your project directory using cd ./my-app
         Check out README.md for development and deploy instructions.
```

---

To start the dev server, run `bun run dev` from the project root. This will start the dev server using the `remix dev` command. Note that Node.js will be used to run the dev server.

terminal

Copy

```
cd my-app
bun run dev
```

Copy

```
$ remix dev

💿  remix dev

info  building...
info  built (263ms)
Remix App Server started at http://localhost:3000 (http://172.20.0.143:3000)
```

---

Open <http://localhost:3000> to see the app. Any changes you make to `app/routes/_index.tsx` will be hot-reloaded in the browser.

![Remix app running on localhost](https://github.com/oven-sh/bun/assets/3084745/c26f1059-a5d4-4c0b-9a88-d9902472fd77)

---

To build and start your app, run `bun run build`

terminal

Copy

```
bun run build
```

Copy

```
$ remix build
info  building... (NODE_ENV=production)
info  built (158ms)
```

Then `bun run start` from the project root.

terminal

Copy

```
bun start
```

Copy

```
$ remix-serve ./build/index.js
[remix-serve] http://localhost:3000 (http://192.168.86.237:3000)
```

---

Read the [Remix docs](https://remix.run/) for more information on how to build apps with Remix.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/ecosystem/remix.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/ecosystem/remix)

⌘I