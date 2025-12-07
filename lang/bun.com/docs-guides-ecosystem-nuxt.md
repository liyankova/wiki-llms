---
url: https://bun.com/docs/guides/ecosystem/nuxt
title: Build an app with Nuxt and Bun - Bun
source_domain: bun.com
---

# Build an app with Nuxt and Bun - Bun

Bun supports [Nuxt](https://nuxt.com) out of the box. Initialize a Nuxt app with official `nuxi` CLI.

terminal

Copy

```
bunx nuxi init my-nuxt-app
```

Copy

```
✔ Which package manager would you like to use?
bun
◐ Installing dependencies...
bun install v1.3.3 (16b4bf34)
 + @nuxt/[email protected]
 + [email protected]
 785 packages installed [2.67s]
✔ Installation completed.
✔ Types generated in .nuxt
✨ Nuxt project has been created with the v3 template. Next steps:
 › cd my-nuxt-app
 › Start development server with bun run dev
```

---

To start the dev server, run `bun --bun run dev` from the project root. This will execute the `nuxt dev` command (as defined in the `"dev"` script in `package.json`).

The `nuxt` CLI uses Node.js by default; passing the `--bun` flag forces the dev server to use the Bun runtime instead.

terminal

Copy

```
cd my-nuxt-app
bun --bun run dev
```

Copy

```
nuxt dev
Nuxi 3.6.5
Nuxt 3.6.5 with Nitro 2.5.2
  > Local:    http://localhost:3000/
  > Network:  http://192.168.0.21:3000/
  > Network:  http://[fd8a:d31d:481c:4883:1c64:3d90:9f83:d8a2]:3000/

✔ Nuxt DevTools is enabled v0.8.0 (experimental)
ℹ Vite client warmed up in 547ms
✔ Nitro built in 244 ms
```

---

Once the dev server spins up, open <http://localhost:3000> to see the app. The app will render Nuxt’s built-in `NuxtWelcome` template component.
To start developing your app, replace `<NuxtWelcome />` in `app.vue` with your own UI.

![Demo Nuxt app running on
localhost](https://github.com/oven-sh/bun/assets/3084745/2c683ecc-3298-4bb0-b8c0-cf4cfaea1daa)

---

For production build, while the default preset is already compatible with Bun, you can also use [Bun preset](https://nitro.build/deploy/runtimes/bun) to generate better optimized builds.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)nuxt.config.ts

Copy

```
export default defineNuxtConfig({
  nitro: {
    preset: "bun", 
  },
});
```

Alternatively, you can set the preset via environment variable:

terminal

Copy

```
NITRO_PRESET=bun bun run build
```

Some packages provide Bun-specific exports that Nitro will not bundle correctly using the default preset. In this
case, you need to use Bun preset so that the packages will work correctly in production builds.

After building with bun, run:

terminal

Copy

```
bun run ./.output/server/index.mjs
```

---

Refer to the [Nuxt website](https://nuxt.com/docs) for complete documentation.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/ecosystem/nuxt.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/ecosystem/nuxt)

⌘I