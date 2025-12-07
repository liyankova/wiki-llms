---
url: https://bun.com/docs/guides/runtime/import-json
title: Import a JSON file - Bun
source_domain: bun.com
---

# Import a JSON file - Bun

Bun natively supports `.json` imports.

package.json

Copy

```
{
  "name": "bun",
  "version": "1.0.0",
  "author": {
    "name": "John Dough",
    "email": "[email protected]"
  }
}
```

---

Import the file like any other source file.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)data.ts

Copy

```
import data from "./package.json";

data.name; // => "bun"
data.version; // => "1.0.0"
data.author.name; // => "John Dough"
```

---

Bun also supports [Import Attributes](https://github.com/tc39/proposal-import-attributes/) and [JSON modules](https://github.com/tc39/proposal-json-modules) syntax.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)data.ts

Copy

```
import data from "./package.json" with { type: "json" };

data.name; // => "bun"
data.version; // => "1.0.0"
data.author.name; // => "John Dough"
```

---

See [Docs > Runtime > TypeScript](https://bun.com/docs/runtime/typescript) for more information on using TypeScript with Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/runtime/import-json.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/runtime/import-json)

⌘I