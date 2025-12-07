---
url: https://bun.com/docs/guides/read-file/string
title: Read a file as a string - Bun
source_domain: bun.com
---

# Read a file as a string - Bun

The `Bun.file()` function accepts a path and returns a `BunFile` instance. The `BunFile` class extends `Blob` and allows you to lazily read the file in a variety of formats. Use `.text()` to read the contents as a string.

Copy

```
const path = "/path/to/file.txt";
const file = Bun.file(path);

const text = await file.text();
// string
```

---

Any relative paths will be resolved relative to the project root (the nearest directory containing a `package.json` file).

Copy

```
const path = "./file.txt";
const file = Bun.file(path);
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/read-file/string.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/read-file/string)

⌘I