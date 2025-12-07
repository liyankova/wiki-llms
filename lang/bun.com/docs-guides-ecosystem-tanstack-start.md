---
url: https://bun.com/docs/guides/ecosystem/tanstack-start
title: Use TanStack Start with Bun - Bun
source_domain: bun.com
---

# Use TanStack Start with Bun - Bun

[TanStack Start](https://tanstack.com/start/latest) is a full-stack framework powered by TanStack Router. It supports full-document SSR, streaming, server functions, bundling and more, powered by TanStack Router and [Vite](https://vite.dev/).

---

1

Create a new TanStack Start app

Use the interactive CLI to create a new TanStack Start app.

terminal

Copy

```
bun create @tanstack/start@latest my-tanstack-app
```

2

Start the dev server

Change to the project directory and run the dev server with Bun.

terminal

Copy

```
cd my-tanstack-app
bun --bun run dev
```

This starts the Vite dev server with Bun.

3

Update scripts in package.json

Modify the scripts field in your `package.json` by prefixing the Vite CLI commands with `bun --bun`. This ensures that Bun executes the Vite CLI for common tasks like `dev`, `build`, and `preview`.

package.json

Copy

```
{
  "scripts": {
    "dev": "bun --bun vite dev", 
    "build": "bun --bun vite build", 
    "serve": "bun --bun vite preview"
  }
}
```

---

## [​](https://bun.com/docs/guides/ecosystem/tanstack-start#hosting) Hosting

To host your TanStack Start app, you can use [Nitro](https://nitro.build/) or a custom Bun server for production deployments.

* Nitro
* Custom Server

1

Add Nitro to your project

Add [Nitro](https://nitro.build/) to your project. This tool allows you to deploy your TanStack Start app to different platforms.

terminal

Copy

```
bun add nitro
```

2

Update your `vite.config.ts` file to include the necessary plugins for TanStack Start with Bun.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)vite.config.ts

Copy

```
// other imports...
import { nitro } from "nitro/vite"; 

const config = defineConfig({
  plugins: [
    tanstackStart(),
    nitro({ preset: "bun" }), 
    // other plugins...
  ],
});

export default config;
```

The `bun` preset is optional, but it configures the build output specifically for Bun’s runtime.

3

Update the start command

Make sure `build` and `start` scripts are present in your `package.json` file:

package.json

Copy

```
  {
    "scripts": {
      "build": "bun --bun vite build", 
      // The .output files are created by Nitro when you run `bun run build`.
      // Not necessary when deploying to Vercel.
      "start": "bun run .output/server/index.mjs"
    }
  }
```

You do **not** need the custom `start` script when deploying to Vercel.

4

Deploy your app

Check out one of our guides to deploy your app to a hosting provider.

When deploying to Vercel, you can either add the `"bunVersion": "1.x"` to your `vercel.json` file, or add it to the `nitro` config in your `vite.config.ts` file:

Do **not** use the `bun` Nitro preset when deploying to Vercel.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)vite.config.ts

Copy

```
export default defineConfig({
  plugins: [
    tanstackStart(),
    nitro({
      preset: "bun", 
      vercel: { 
        functions: { 
          runtime: "bun1.x", 
        }, 
    }, 
    }),
  ],
});
```

[![https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/vercel.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=7b490676c38ef9af753b06839da7b0d5](https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/vercel.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=7b490676c38ef9af753b06839da7b0d5)

## Vercel

Deploy on Vercel](https://bun.com/docs/guides/deployment/vercel)[![https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/render.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=5ac8410728c8e2d747afc287b0b715d9](https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/render.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=5ac8410728c8e2d747afc287b0b715d9)

## Render

Deploy on Render](https://bun.com/docs/guides/deployment/render)[![https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/railway.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=da50a9424b0121975a3bd68e7038425e](https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/railway.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=da50a9424b0121975a3bd68e7038425e)

## Railway

Deploy on Railway](https://bun.com/docs/guides/deployment/railway)[![https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/digitalocean.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=b3f34ba0a9eb2c1968261738759f2542](https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/digitalocean.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=b3f34ba0a9eb2c1968261738759f2542)

## DigitalOcean

Deploy on DigitalOcean](https://bun.com/docs/guides/deployment/digital-ocean)[![https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/aws.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=9733e5ae5faecf5974cbd02661e2b4f2](https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/aws.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=9733e5ae5faecf5974cbd02661e2b4f2)

## AWS Lambda

Deploy on AWS Lambda](https://bun.com/docs/guides/deployment/aws-lambda)[![https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/gcp.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=a99e6cb0cfadfeb9ea3b6451de38cfd6](https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/gcp.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=a99e6cb0cfadfeb9ea3b6451de38cfd6)

## Google Cloud Run

Deploy on Google Cloud Run](https://bun.com/docs/guides/deployment/google-cloud-run)

---

## [​](https://bun.com/docs/guides/ecosystem/tanstack-start#templates) Templates

[![bun-tanstack-todo](https://mintcdn.com/bun-1dd33a4e/M5IN-LfyV8DoQVZm/images/templates/bun-tanstack-todo.png?fit=max&auto=format&n=M5IN-LfyV8DoQVZm&q=85&s=2158d48f96cabb9a5e4d66ff94bab5fa)

## Todo App with Tanstack + Bun

A Todo application built with Bun, TanStack Start, and PostgreSQL.](https://github.com/bun-templates/bun-tanstack-todo)[![bun-tanstack-basic](https://mintcdn.com/bun-1dd33a4e/M5IN-LfyV8DoQVZm/images/templates/bun-tanstack-basic.png?fit=max&auto=format&n=M5IN-LfyV8DoQVZm&q=85&s=9636defcaa30d79a3e8fe00740b3846f)

## Bun + TanStack Start Application

A TanStack Start template using Bun with SSR and file-based routing.](https://github.com/bun-templates/bun-tanstack-basic)[![bun-tanstack-start](https://mintcdn.com/bun-1dd33a4e/M5IN-LfyV8DoQVZm/images/templates/bun-tanstack-start.png?fit=max&auto=format&n=M5IN-LfyV8DoQVZm&q=85&s=49d7a4fab3a407cae793c7348a633ca6)

## Basic Bun + Tanstack Starter

The basic TanStack starter using the Bun runtime and Bun’s file APIs.](https://github.com/bun-templates/bun-tanstack-start)

---

[→ See TanStack Start’s official documentation](https://tanstack.com/start/latest/docs/framework/react/guide/hosting) for more information on hosting.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/ecosystem/tanstack-start.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/ecosystem/tanstack-start)

⌘I