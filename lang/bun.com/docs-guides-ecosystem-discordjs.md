---
url: https://bun.com/docs/guides/ecosystem/discordjs
title: Create a Discord bot - Bun
source_domain: bun.com
---

# Create a Discord bot - Bun

Discord.js works out of the box with Bun. Let’s write a simple bot. First create a directory and initialize it with `bun init`.

terminal

Copy

```
mkdir my-bot
cd my-bot
bun init
```

---

Now install Discord.js.

terminal

Copy

```
bun add discord.js
```

---

Before we go further, we need to go to the [Discord developer portal](https://discord.com/developers/applications), login/signup, create a new *Application*, then create a new *Bot* within that application. Follow the [official guide](https://discordjs.guide/legacy/preparations/app-setup#creating-your-bot) for step-by-step instructions.

---

Once complete, you’ll be presented with your bot’s *private key*. Let’s add this to a file called `.env.local`. Bun automatically reads this file and loads it into `process.env`.

This is an example token that has already been invalidated.

.env.local

Copy

```
DISCORD_TOKEN=NzkyNz
```

---

Be sure to add `.env.local` to your `.gitignore`! It is dangerous to check your bot’s private key into version control.

.gitignore

Copy

```
node_modules
.env.local
```

---

Now let’s actually write our bot in a new file called `bot.ts`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)bot.ts

Copy

```
// import discord.js
import { Client, Events, GatewayIntentBits } from "discord.js";

// create a new Client instance
const client = new Client({ intents: [GatewayIntentBits.Guilds] });

// listen for the client to be ready
client.once(Events.ClientReady, c => {
  console.log(`Ready! Logged in as ${c.user.tag}`);
});

// login with the token from .env.local
client.login(process.env.DISCORD_TOKEN);
```

---

Now we can run our bot with `bun run`. It may take a several seconds for the client to initialize the first time you run the file.

terminal

Copy

```
bun run bot.ts
```

Copy

```
Ready! Logged in as my-bot#1234
```

---

You’re up and running with a bare-bones Discord.js bot! This is a basic guide to setting up your bot with Bun; we recommend the [official discord.js docs](https://discordjs.guide/) for complete information on the `discord.js` API.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/ecosystem/discordjs.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/ecosystem/discordjs)

⌘I
