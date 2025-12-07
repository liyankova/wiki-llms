---
url: https://bun.com/docs/guides/ecosystem/mongoose
title: Read and write data to MongoDB using Mongoose and Bun - Bun
source_domain: bun.com
---

# Read and write data to MongoDB using Mongoose and Bun - Bun

MongoDB and Mongoose work out of the box with Bun. This guide assumes you’ve already installed MongoDB and are running it as background process/service on your development machine. Follow [this guide](https://www.mongodb.com/docs/manual/installation/) for details.

---

Once MongoDB is running, create a directory and initialize it with `bun init`.

terminal

Copy

```
mkdir mongoose-app
cd mongoose-app
bun init
```

---

Then add Mongoose as a dependency.

terminal

Copy

```
bun add mongoose
```

---

In `schema.ts` we’ll declare and export a simple `Animal` model.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)schema.ts

Copy

```
import * as mongoose from "mongoose";

const animalSchema = new mongoose.Schema(
  {
    title: { type: String, required: true },
    sound: { type: String, required: true },
  },
  {
    methods: {
      speak() {
        console.log(`${this.sound}!`);
      },
    },
  },
);

export type Animal = mongoose.InferSchemaType<typeof animalSchema>;
export const Animal = mongoose.model("Animal", animalSchema);
```

---

Now from `index.ts` we can import `Animal`, connect to MongoDB, and add some data to our database.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
import * as mongoose from "mongoose";
import { Animal } from "./schema";

// connect to database
await mongoose.connect("mongodb://127.0.0.1:27017/mongoose-app");

// create new Animal
const cow = new Animal({
  title: "Cow",
  sound: "Moo",
});
await cow.save(); // saves to the database

// read all Animals
const animals = await Animal.find();
animals[0].speak(); // logs "Moo!"

// disconnect
await mongoose.disconnect();
```

---

Let’s run this with `bun run`.

terminal

Copy

```
bun run index.ts
```

Copy

```
Moo!
```

---

This is a simple introduction to using Mongoose with TypeScript and Bun. As you build your application, refer to the official [MongoDB](https://www.mongodb.com/docs) and [Mongoose](https://mongoosejs.com/docs/) sites for complete documentation.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/ecosystem/mongoose.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/ecosystem/mongoose)

⌘I