---
url: https://bun.com/docs/quickstart
title: Quickstart - Bun
source_domain: bun.com
---

# Quickstart - Bun

## [​](https://bun.com/docs/quickstart#overview) Overview

Build a minimal HTTP server with `Bun.serve`, run it locally, then evolve it by installing a package.

Prerequisites: Bun installed and available on your `PATH`. See [installation](https://bun.com/docs/installation) for setup.

---

1

Step 1

Initialize a new project with `bun init`.

terminal

Copy

```
bun init my-app
```

It’ll prompt you to pick a template, either `Blank`, `React`, or `Library`. For this guide, we’ll pick `Blank`.

terminal

Copy

```
bun init my-app
```

Copy

```
✓ Select a project template: Blank

- .gitignore
- CLAUDE.md
- .cursor/rules/use-bun-instead-of-node-vite-npm-pnpm.mdc -> CLAUDE.md
- index.ts
- tsconfig.json (for editor autocomplete)
- README.md
```

This automatically creates a `my-app` directory with a basic Bun app.

2

Step 2

Run the `index.ts` file using `bun run index.ts`.

terminal

Copy

```
cd my-app
bun run index.ts
```

Copy

```
Hello via Bun!
```

You should see a console output saying `"Hello via Bun!"`.

3

Step 3

Replace the contents of `index.ts` with the following code:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
const server = Bun.serve({
  port: 3000,
  routes: {
    "/": () => new Response('Bun!'),
  }
});

console.log(`Listening on ${server.url}`);
```

Run the `index.ts` file again using `bun run index.ts`.

terminal

Copy

```
bun run index.ts
```

Copy

```
Listening on http://localhost:3000
```

Visit [`http://localhost:3000`](http://localhost:3000) to test the server. You should see a simple page that says `"Bun!"`.

Seeing TypeScript errors on Bun?

If you used `bun init`, Bun will have automatically installed Bun’s TypeScript declarations and configured your `tsconfig.json`. If you’re trying out Bun in an existing project, you may see a type error on the `Bun` global.To fix this, first install `@types/bun` as a dev dependency.

terminal

Copy

```
bun add -d @types/bun
```

Then add the following to your `compilerOptions` in `tsconfig.json`:

tsconfig.json

Copy

```
{
  "compilerOptions": {
    "lib": ["ESNext"],
    "target": "ESNext",
    "module": "Preserve",
    "moduleDetection": "force",
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "verbatimModuleSyntax": true,
    "noEmit": true
  }
}
```

4

Step 4

Install the `figlet` package and its type declarations. Figlet is a utility for converting strings into ASCII art.

terminal

Copy

```
bun add figlet
bun add -d @types/figlet # TypeScript users only
```

Update `index.ts` to use `figlet` in `routes`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
import figlet from 'figlet'; 

const server = Bun.serve({
  port: 3000,
  routes: {
    "/": () => new Response('Bun!'),
    "/figlet": () => { 
      const body = figlet.textSync('Bun!'); 
      return new Response(body); 
    } 
  }
});

console.log(`Listening on ${server.url}`);
```

Run the `index.ts` file again using `bun run index.ts`.

terminal

Copy

```
bun run index.ts
```

Copy

```
Listening on http://localhost:3000
```

Visit [`http://localhost:3000/figlet`](http://localhost:3000/figlet) to test the server. You should see a simple page that says `"Bun!"` in ASCII art.

Copy

```
____              _
| __ ) _   _ _ __ | |
|  _ \| | | | '_ \| |
| |_) | |_| | | | |_|
|____/ \__,_|_| |_(_)
```

5

Step 5

Let’s add some HTML. Create a new file called `index.html` and add the following code:

index.html

Copy

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bun</title>
  </head>
  <body>
    <h1>Bun!</h1>
  </body>
</html>
```

Then, import this file in `index.ts` and serve it from the root `/` route.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
import figlet from 'figlet';
import index from './index.html'; 

const server = Bun.serve({
  port: 3000,
  routes: {
    "/": index, 
    "/figlet": () => {
      const body = figlet.textSync('Bun!');
      return new Response(body);
    }
  }
});

console.log(`Listening on ${server.url}`);
```

Run the `index.ts` file again using `bun run index.ts`.

terminal

Copy

```
bun run index.ts
```

Copy

```
Listening on http://localhost:3000
```

Visit [`http://localhost:3000`](http://localhost:3000) to test the server. You should see the static HTML page.

🎉 Congratulations! You’ve built a simple HTTP server with Bun and installed a package.

---

## [​](https://bun.com/docs/quickstart#run-a-script) Run a script

Bun can also execute `"scripts"` from your `package.json`. Add the following script:

package.json

Copy

```
{
  "name": "quickstart",
  "module": "index.ts",
  "type": "module",
  "private": true,
  "scripts": { 
    "start": "bun run index.ts"
  }, 
  "devDependencies": {
    "@types/bun": "latest"
  },
  "peerDependencies": {
    "typescript": "^5"
  }
}
```

Then run it with `bun run start`.

terminal

Copy

```
bun run start
```

Copy

```
Listening on http://localhost:3000
```

⚡️ **Performance** — `bun run` is roughly 28x faster than `npm run` (6ms vs 170ms of overhead).

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/quickstart.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /quickstart)

⌘I