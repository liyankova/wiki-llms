---
url: https://bun.com/docs/guides/deployment/vercel
title: Deploy a Bun application on Vercel - Bun
source_domain: bun.com
---

# Deploy a Bun application on Vercel - Bun

[Vercel](https://vercel.com/) is a cloud platform that lets you build, deploy, and scale your apps.

The Bun runtime is in Beta; certain features (e.g., automatic source maps, byte-code caching, metrics on
`node:http/https`) are not yet supported.

`Bun.serve` is currently not supported on Vercel Functions. Use Bun with frameworks supported by Vercel, like Next.js,
Express, Hono, or Nitro.

---

1

Configure Bun in vercel.json

To enable the Bun runtime for your Functions, add a `bunVersion` field in your `vercel.json` file:

vercel.json

Copy

```
{
	"bunVersion": "1.x"
}
```

Vercel automatically detects this configuration and runs your application on Bun. The value has to be `"1.x"`, Vercel handles the minor version internally.For best results, match your local Bun version with the version used by Vercel.

2

Next.js configuration

If you’re deploying a **Next.js** project (including ISR), update your `package.json` scripts to use the Bun runtime:

package.json

Copy

```
{
	"scripts": {
		"dev": "bun --bun next dev", 
		"build": "bun --bun next build"
	}
}
```

The `--bun` flag runs the Next.js CLI under Bun. Bundling (via Turbopack or Webpack) remains unchanged, but all commands execute within the Bun runtime.

This ensures both local development and builds use Bun.

3

Deploy your app

Connect your repository to Vercel, or deploy from the CLI:

terminal

Copy

```
# Using bunx (no global install)
bunx vercel login
bunx vercel deploy
```

Or install the Vercel CLI globally:

terminal

Copy

```
bun i -g vercel
vercel login
vercel deploy
```

[Learn more in the Vercel Deploy CLI documentation →](https://vercel.com/docs/cli/deploy)

4

Verify the runtime

To confirm your deployment uses Bun, log the Bun version:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
console.log("runtime", process.versions.bun);
```

Copy

```
runtime 1.3.3
```

[See the Vercel Bun Runtime documentation for feature support →](https://vercel.com/docs/functions/runtimes/bun#feature-support)

---

* [Fluid compute](https://vercel.com/docs/fluid-compute): Both Bun and Node.js runtimes run on Fluid compute and support the same core Vercel Functions features.
* [Middleware](https://vercel.com/docs/routing-middleware): To run Routing Middleware with Bun, set the runtime to `nodejs`:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)middleware.ts

Copy

```
export const config = { runtime: "nodejs" };
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/deployment/vercel.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/deployment/vercel)

⌘I