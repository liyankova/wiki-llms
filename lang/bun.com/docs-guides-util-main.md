---
url: https://bun.com/docs/guides/util/main
title: Get the absolute path to the current entrypoint - Bun
source_domain: bun.com
---

# Get the absolute path to the current entrypoint - Bun

The `Bun.main` property contains the absolute path to the current entrypoint.

Copy

```
console.log(Bun.main);
```

---

The printed path corresponds to the file that is executed with `bun run`.

terminal

Copy

```
bun run index.ts
```

Copy

```
/path/to/index.ts
```

terminal

Copy

```
bun run foo.ts
```

Copy

```
/path/to/foo.ts
```

---

See [Docs > API > Utils](https://bun.com/docs/runtime/utils) for more useful utilities.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/util/main.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/util/main)

⌘I