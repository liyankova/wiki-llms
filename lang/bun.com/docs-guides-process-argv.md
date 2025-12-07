---
url: https://bun.com/docs/guides/process/argv
title: Parse command-line arguments - Bun
source_domain: bun.com
---

# Parse command-line arguments - Bun

The *argument vector* is the list of arguments passed to the program when it is run. It is available as `Bun.argv`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)cli.ts

Copy

```
console.log(Bun.argv);
```

---

Running this file with arguments results in the following:

terminal

Copy

```
bun run cli.ts --flag1 --flag2 value
```

Copy

```
[ '/path/to/bun', '/path/to/cli.ts', '--flag1', '--flag2', 'value' ]
```

---

To parse `argv` into a more useful format, `util.parseArgs` would be helpful.
Example:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)cli.ts

Copy

```
import { parseArgs } from "util";

const { values, positionals } = parseArgs({
  args: Bun.argv,
  options: {
    flag1: {
      type: "boolean",
    },
    flag2: {
      type: "string",
    },
  },
  strict: true,
  allowPositionals: true,
});

console.log(values);
console.log(positionals);
```

---

then it outputs

terminal

Copy

```
bun run cli.ts --flag1 --flag2 value
```

Copy

```
{
  flag1: true,
  flag2: "value",
}
[ "/path/to/bun", "/path/to/cli.ts" ]
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/process/argv.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/process/argv)

⌘I