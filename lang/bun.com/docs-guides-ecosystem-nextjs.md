---
url: https://bun.com/docs/guides/ecosystem/nextjs
title: Build an app with Next.js and Bun - Bun
source_domain: bun.com
---

# Build an app with Next.js and Bun - Bun

[Next.js](https://nextjs.org/) is a React framework for building full-stack web applications. It supports server-side rendering, static site generation, API routes, and more. Bun provides fast package installation and can run Next.js development and production servers.

---

1

Create a new Next.js app

Use the interactive CLI to create a new Next.js app. This will scaffold a new Next.js project and automatically install dependencies.

terminal

Copy

```
bun create next-app@latest my-bun-app
```

2

Start the dev server

Change to the project directory and run the dev server with Bun.

terminal

Copy

```
cd my-bun-app
bun --bun run dev
```

This starts the Next.js dev server with Bun’s runtime.Open [`http://localhost:3000`](http://localhost:3000) with your browser to see the result. Any changes you make to `app/page.tsx` will be hot-reloaded in the browser.

3

Update scripts in package.json

Modify the scripts field in your `package.json` by prefixing the Next.js CLI commands with `bun --bun`. This ensures that Bun executes the Next.js CLI for common tasks like `dev`, `build`, and `start`.

package.json

Copy

```
{
  "scripts": {
    "dev": "bun --bun next dev", 
    "build": "bun --bun next build", 
    "start": "bun --bun next start", 
  }
}
```

---

## [​](https://bun.com/docs/guides/ecosystem/nextjs#hosting) Hosting

Next.js applications on Bun can be deployed to various platforms.

[![https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/vercel.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=7b490676c38ef9af753b06839da7b0d5](https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/vercel.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=7b490676c38ef9af753b06839da7b0d5)

## Vercel

Deploy on Vercel](https://bun.com/docs/guides/deployment/vercel)[![https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/railway.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=da50a9424b0121975a3bd68e7038425e](https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/railway.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=da50a9424b0121975a3bd68e7038425e)

## Railway

Deploy on Railway](https://bun.com/docs/guides/deployment/railway)[![https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/digitalocean.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=b3f34ba0a9eb2c1968261738759f2542](https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/digitalocean.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=b3f34ba0a9eb2c1968261738759f2542)

## DigitalOcean

Deploy on DigitalOcean](https://bun.com/docs/guides/deployment/digital-ocean)[![https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/aws.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=9733e5ae5faecf5974cbd02661e2b4f2](https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/aws.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=9733e5ae5faecf5974cbd02661e2b4f2)

## AWS Lambda

Deploy on AWS Lambda](https://bun.com/docs/guides/deployment/aws-lambda)[![https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/gcp.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=a99e6cb0cfadfeb9ea3b6451de38cfd6](https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/gcp.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=a99e6cb0cfadfeb9ea3b6451de38cfd6)

## Google Cloud Run

Deploy on Google Cloud Run](https://bun.com/docs/guides/deployment/google-cloud-run)[![https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/render.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=5ac8410728c8e2d747afc287b0b715d9](https://mintcdn.com/bun-1dd33a4e/cfVIaCNGtFU88Wgc/icons/ecosystem/render.svg?fit=max&auto=format&n=cfVIaCNGtFU88Wgc&q=85&s=5ac8410728c8e2d747afc287b0b715d9)

## Render

Deploy on Render](https://bun.com/docs/guides/deployment/render)

---

## [​](https://bun.com/docs/guides/ecosystem/nextjs#templates) Templates

[![bun-nextjs-basic](https://mintcdn.com/bun-1dd33a4e/M5IN-LfyV8DoQVZm/images/templates/bun-nextjs-basic.png?fit=max&auto=format&n=M5IN-LfyV8DoQVZm&q=85&s=2bc9edb73c9c49d88e8ced9e2158f75a)

## Bun + Next.js Basic Starter

A simple App Router starter with Bun, Next.js, and Tailwind CSS.](https://github.com/bun-templates/bun-nextjs-basic)[![bun-nextjs-todo](https://mintcdn.com/bun-1dd33a4e/M5IN-LfyV8DoQVZm/images/templates/bun-nextjs-todo.png?fit=max&auto=format&n=M5IN-LfyV8DoQVZm&q=85&s=e8f398caf487c6b925a53025c42f4dab)

## Todo App with Next.js + Bun

A full-stack todo application built with Bun, Next.js, and PostgreSQL.](https://github.com/bun-templates/bun-nextjs-todo)

---

[→ See Next.js’s official documentation](https://nextjs.org/docs) for more information on building and deploying Next.js applications.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/ecosystem/nextjs.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/ecosystem/nextjs)

⌘I