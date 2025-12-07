---
url: https://bun.com/docs/guides/deployment/render
title: Deploy a Bun application on Render - Bun
source_domain: bun.com
---

# Deploy a Bun application on Render - Bun

[Render](https://render.com/) is a cloud platform that lets you flexibly build, deploy, and scale your apps.
It offers features like auto deploys from GitHub, a global CDN, private networks, automatic HTTPS setup, and managed PostgreSQL and Redis.
Render supports Bun natively. You can deploy Bun apps as web services, background workers, cron jobs, and more.

---

As an example, let’s deploy a simple Express HTTP server to Render.

1

Step 1

Create a new GitHub repo named `myapp`. Git clone it locally.

Copy

```
git clone [email protected]:my-github-username/myapp.git
cd myapp
```

2

Step 2

Add the Express library.

Copy

```
bun add express
```

3

Step 3

Define a simple server with Express:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)app.ts

Copy

```
import express from "express";

const app = express();
const port = process.env.PORT || 3001;

app.get("/", (req, res) => {
	res.send("Hello World!");
});

app.listen(port, () => {
	console.log(`Listening on port ${port}...`);
});
```

4

Step 4

Commit your changes and push to GitHub.

terminal

Copy

```
git add app.ts bun.lock package.json
git commit -m "Create simple Express app"
git push origin main
```

5

Step 5

In your [Render Dashboard](https://dashboard.render.com/), click `New` > `Web Service` and connect your `myapp` repo.

6

Step 6

In the Render UI, provide the following values during web service creation:

|  |  |
| --- | --- |
| **Runtime** | `Node` |
| **Build Command** | `bun install` |
| **Start Command** | `bun app.ts` |

That’s it! Your web service will be live at its assigned `onrender.com` URL as soon as the build finishes.
You can view the [deploy logs](https://docs.render.com/logging#logs-for-an-individual-deploy-or-job) for details. Refer to [Render’s documentation](https://docs.render.com/deploys) for a complete overview of deploying on Render.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/deployment/render.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/deployment/render)

⌘I