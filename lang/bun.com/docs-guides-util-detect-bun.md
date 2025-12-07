---
url: https://bun.com/docs/guides/util/detect-bun
title: Detect when code is executed with Bun - Bun
source_domain: bun.com
---

# Detect when code is executed with Bun - Bun

The recommended way to detect when code is being executed with Bun is to check `process.versions.bun`. This works in both JavaScript and TypeScript without requiring any additional type definitions.

Copy

```
if (process.versions.bun) {
  // this code will only run when the file is run with Bun
}
```

---

Alternatively, you can check for the existence of the `Bun` global. This is similar to how you’d check for the existence of the `window` variable to detect when code is being executed in a browser.

This approach will result in a type error in TypeScript unless `@types/bun` is installed. You can install it with `bun add -d @types/bun`.

Copy

```
if (typeof Bun !== "undefined") {
  // this code will only run when the file is run with Bun
}
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/util/detect-bun.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/util/detect-bun)

⌘I