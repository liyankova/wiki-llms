---
url: https://bun.com/docs/guides/runtime/shell
title: Run a Shell Command - Bun
source_domain: bun.com
---

# Run a Shell Command - Bun

Bun Shell is a cross-platform bash-like shell built in to Bun.
It provides a simple way to run shell commands in JavaScript and TypeScript. To get started, import the `$` function from the `bun` package and use it to run shell commands.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)foo.ts

Copy

```
import { $ } from "bun";

await $`echo Hello, world!`; // => "Hello, world!"
```

---

The `$` function is a tagged template literal that runs the command and returns a promise that resolves with the command’s output.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)foo.ts

Copy

```
import { $ } from "bun";

const output = await $`ls -l`.text();
console.log(output);
```

---

To get each line of the output as an array, use the `lines` method.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)foo.ts

Copy

```
import { $ } from "bun";

for await (const line of $`ls -l`.lines()) {
  console.log(line);
}
```

---

See [Docs > API > Shell](https://bun.com/docs/runtime/shell) for complete documentation.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/runtime/shell.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/runtime/shell)

⌘I