---
url: https://bun.com/docs/guides/runtime/import-yaml
title: Import a YAML file - Bun
source_domain: bun.com
---

# Import a YAML file - Bun

Bun natively supports `.yaml` and `.yml` imports.

config.yaml

Copy

```
database:
  host: localhost
  port: 5432
  name: myapp

server:
  port: 3000
  timeout: 30

features:
  auth: true
  rateLimit: true
```

---

Import the file like any other source file.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)config.ts

Copy

```
import config from "./config.yaml";

config.database.host; // => "localhost"
config.server.port; // => 3000
config.features.auth; // => true
```

---

You can also use named imports to destructure top-level properties:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)config.ts

Copy

```
import { database, server, features } from "./config.yaml";

console.log(database.name); // => "myapp"
console.log(server.timeout); // => 30
console.log(features.rateLimit); // => true
```

---

Bun also supports [Import Attributes](https://github.com/tc39/proposal-import-attributes) syntax:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)config.ts

Copy

```
import config from "./config.yaml" with { type: "yaml" };

config.database.port; // => 5432
```

---

For parsing YAML strings at runtime, use `Bun.YAML.parse()`:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)config.ts

Copy

```
const yamlString = `
name: John Doe
age: 30
hobbies:
  - reading
  - coding
`;

const data = Bun.YAML.parse(yamlString);
console.log(data.name); // => "John Doe"
console.log(data.hobbies); // => ["reading", "coding"]
```

---

## [​](https://bun.com/docs/guides/runtime/import-yaml#typescript-support) TypeScript Support

To add TypeScript support for your YAML imports, create a declaration file with `.d.ts` appended to the YAML filename (e.g., `config.yaml` → `config.yaml.d.ts`);

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)config.yaml.d.ts

Copy

```
const contents: {
  database: {
    host: string;
    port: number;
    name: string;
  };
  server: {
    port: number;
    timeout: number;
  };
  features: {
    auth: boolean;
    rateLimit: boolean;
  };
};

export = contents;
```

---

See [Docs > API > YAML](https://bun.com/docs/runtime/yaml) for complete documentation on YAML support in Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/runtime/import-yaml.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/runtime/import-yaml)

⌘I