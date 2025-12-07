---
url: https://bun.com/blog/bun-v0.6.7
title: Bun v0.6.7 | Bun Blog
source_domain: bun.com
---

# Bun v0.6.7 | Bun Blog

# Bun v0.6.7

---

[Jarred Sumner](https://twitter.com/jarredsumner) · June 2, 2023

We're hiring C/C++ and Zig engineers to build the future of JavaScript! [Join our team →](https://bun.com/careers)

We've been releasing a lot of changes to Bun recently, here's a recap in case you missed it:

* [`v0.6.0`](https://bun.com/blog/bun-bundler) - Introducing `bun build`, Bun's new JavaScript bundler.
* [`v0.6.2`](https://bun.com/blog/bun-v0.6.2) - Performance boosts: 20% faster `JSON.parse`, up to 2x faster `Proxy` and `arguments`.
* [`v0.6.3`](https://bun.com/blog/bun-v0.6.3) - Implemented `node:vm`, lots of fixes to `node:http` and `node:tls`.
* [`v0.6.4`](https://bun.com/blog/bun-v0.6.4) - Implemented `require.cache`, `process.env.TZ`, and 80% faster `bun test`.
* [`v0.6.5`](https://bun.com/blog/bun-v0.6.5) - Native support for CommonJS modules (*previously, Bun did CJS to ESM transpilation*),
* [`v0.6.6`](https://bun.com/blog/bun-v0.6.6) - `bun test` improvements, including Github Actions support, `test.only()`, `test.if()`, `describe.skip()`, and 15+ more `expect()` matchers; also streaming file uploads using `fetch()`.

Now we're releasing bugfixes to Node.js compatibilty that enable Discord.js, Prisma, and Puppeteer to run in Bun. We've also fixed a regression with `bun build --compile`, a regression from native CommonJS support that could cause a crash, and several bundler bugfixes.

To install Bun:

curl

npm

brew

docker

curl

```
curl -fsSL https://bun.sh/install | bash
```

npm

```
npm install -g bun
```

brew

```
brew tap oven-sh/bun
```

```
brew install bun
```

docker

```
docker pull oven/bun
```

```
docker run --rm --init --ulimit memlock=-1:-1 oven/bun
```

To upgrade Bun:

```
bun upgrade
```

## [Use Prisma in Bun](https://bun.com/blog/bun-v0.6.7#use-prisma-in-bun)

[Prisma](https://github.com/prisma/prisma) is a popular ORM for Node.js, and it now works in Bun!

```
import { PrismaClient } from "@prisma/client";

const prisma = new PrismaClient();

const user = await prisma.user.create({
  data: {
    name: "Alice",
    email: "alice@prisma.io",
  },
});

console.log(user);
```

This was a [popular feature request](https://github.com/oven-sh/bun/issues/2083) in Bun.

#### Why didn't Prisma work before?

There were several Node-API bugs that prevented Prisma from working in Bun. @cirospaciari fixed those bugs in Bun v0.6.7 (this release).

There was also a transpiler bug that was fixed in Bun v0.6.5 (two releases ago).

Several Node.js compatibility bugfixes led to resolving the issues blocking Prisma from working.

> In the next version of Bun   
>   
> Prisma works, thanks to [@cirospaciari](https://twitter.com/cirospaciari?ref_src=twsrc%5Etfw) [pic.twitter.com/CVyEDzaHnp](https://t.co/CVyEDzaHnp)
>
> — Jarred Sumner (@jarredsumner) [June 3, 2023](https://twitter.com/jarredsumner/status/1664794894609817600?ref_src=twsrc%5Etfw)

## [Use Discord.js in Bun](https://bun.com/blog/bun-v0.6.7#use-discord-js-in-bun)

Discord.js is the most popular library for building Discord bots. It now works in Bun, thanks to [@paperclover](https://github.com/paperclover).

```
import { Client, IntentsBitField } from "discord.js";

const client = new Client({
  intents: [
    IntentsBitField.Flags.Guilds,
    IntentsBitField.Flags.GuildMessages,
    IntentsBitField.Flags.MessageContent,
  ],
});

client.on("ready", () => {
  console.log(`Logged in as ${client.user.tag}!`);
});

client.on("messageCreate", (msg) => {
  console.log(msg.content);
  if (msg.content === "ping") {
    msg.reply("Pong!");
  }
});

client.login(process.env.TOKEN);
```

This also was a [popular feature request](https://github.com/oven-sh/bun/issues/2077) in Bun.

> In the next version of Bun  
>   
> Discord.js works [pic.twitter.com/bjOWgxMuLV](https://t.co/bjOWgxMuLV)
>
> — clo (@paperclover\_dev) [June 1, 2023](https://twitter.com/paperclover_dev/status/1664384878316601346?ref_src=twsrc%5Etfw)

#### Why didn't Discord.js work before?

Node.js compatibility bugs in node:http and undici in Bun, mostly. There was a couple WebSocket bugs too. @paperclover fixed those bugs in Bun v0.6.7 (this release).

We didn't make any Discord.js-specific changes to Bun's code, just Node.js compatibility bugfixes that resolved the issues blocking Discord.js from working.

## [Use Puppeteer in Bun](https://bun.com/blog/bun-v0.6.7#use-puppeteer-in-bun)

Puppeteer is a popular library for automating Chromium. It now works in Bun, thanks to [@cirospaciari](https://github.com/cirospaciari).

```
import puppeteer from "puppeteer";

const browser = await puppeteer.launch();
const page = await browser.newPage();
await page.goto("https://elysiajs.com");
await page.screenshot({ path: "example.png" });
await browser.close();
```

> In the next version of Bun  
>   
> Puppeteer works, thanks to [@cirospaciari](https://twitter.com/cirospaciari?ref_src=twsrc%5Etfw) [pic.twitter.com/DNc1wlipGA](https://t.co/DNc1wlipGA)
>
> — Jarred Sumner (@jarredsumner) [June 3, 2023](https://twitter.com/jarredsumner/status/1664892235966734337?ref_src=twsrc%5Etfw)

#### Why didn't Puppeteer work before?

Issues with `node:net` and CommonJS <> ES Module interop, mostly.

## [Faster node:crypto hashing](https://bun.com/blog/bun-v0.6.7#faster-node-crypto-hashing)

@paperclover landed performance improvements to EventEmitter and node:crypto that leads to about 2x faster hashing on small inputs in Bun.

[![image](https://github.com/oven-sh/bun/assets/709451/b93f651e-1aac-43b8-8e14-be7ca8ee579a)](https://github.com/oven-sh/bun/assets/709451/b93f651e-1aac-43b8-8e14-be7ca8ee579a)

We originally intended to land these changes around Bun v0.5.0 but the tests were failing on CI. We finally got around to fixing it and landing the changes. Thanks @paperclover!

## [Better error message for CommonJS files](https://bun.com/blog/bun-v0.6.7#better-error-message-for-commonjs-files)

> in the next version of bun  
>   
> fixed a bug with error messages while loading commonjs files [pic.twitter.com/UERe2WqL0W](https://t.co/UERe2WqL0W)
>
> — Jarred Sumner (@jarredsumner) [June 2, 2023](https://twitter.com/jarredsumner/status/1664567949716504578?ref_src=twsrc%5Etfw)

## [Bug fixes](https://bun.com/blog/bun-v0.6.7#bug-fixes)

Regressions from the CommonJS rewrite that have been fixed:

* A crash that could occur when many CommonJS files were loaded at once due to incorrectly managing the lifetime of the scope extension
* Bun was sometimes injecting `import.meta.resolveSync` into CommonJS files, which broke some packages like `@prisma/client`
* Bun was not inserting `__dirname` or `__filename` correctly in the CommonJS module wrapper

Hopefully there won't be many more of those.

Two significant differences remain for CommonJS in Bun versus Node.js:

* Module evaluation order. CommonJS files in Bun are evaluated at the time ES modules are parsed. We will see if that ends up breaking things. If it does, we will align it with Node.js' behavior.
* More named exports are available. Node.js relies on static analysis to determine named exports of CommonJS files. Bun uses runtime checks that should expose more named exports. This is a feature, as it means more named imports will work in Bun. But, it is a difference and differences can potentially break things. We'll keep an eye on this.

### [Bundler & transpiler bugfixes](https://bun.com/blog/bun-v0.6.7#bundler-transpiler-bugfixes)

* Certain modules were incorrectly adding `__esModule` to their exports which broke bundling Express apps. Thanks to [@dylan-conway](https://github.com/dylan-conway) for fixing.
* Bun was incorrectly choosing `jsxDEV` over `jsx` when transpiling JSX when specified in a tsconfig.json or jsconfig.json file. Thanks to [@dylan-conway](https://github.com/dylan-conway) for fixing.
* bun build --compile was broken in 0.6.5, it now works again and our CI will catch this in the future. Thanks to [@dylan-conway](https://github.com/dylan-conway) for fixing.
* In certain cases, Bun would incorrectly double-escape UTF-8 string literals with `$` inside backtick quotes, which broke packages like typemorph
* For JSON files, default imports were incorrectly returning an empty object. Thanks to [@dylan-conway](https://github.com/dylan-conway) for fixing.

## [More features](https://bun.com/blog/bun-v0.6.7#more-features)

Bun now supports the `NO_COLOR` environment variable, which disables colored output in the CLI. Thanks to [@electroid](https://github.com/electroid) for adding.

### [Internal changes](https://bun.com/blog/bun-v0.6.7#internal-changes)

Bun's builtin ES modules are now bundled & minified with Bun, thanks to [@paperclover](https://github.com/paperclover)

---

[#### Bun v0.6.6](https://bun.com/blog/bun-v0.6.6)[#### Bun v0.6.8](https://bun.com/blog/bun-v0.6.8)