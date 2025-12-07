---
url: https://bun.com/docs/guides/write-file/basic
title: Write a string to a file - Bun
source_domain: bun.com
---

# Write a string to a file - Bun

This code snippet writes a string to disk at a particular *absolute path*.
It uses the fast [`Bun.write()`](https://bun.com/docs/runtime/file-io#writing-files-bun-write) API to efficiently write data to disk. The first argument is a *destination*; the second is the *data* to write.

Copy

```
const path = "/path/to/file.txt";
await Bun.write(path, "Lorem ipsum");
```

---

Any relative paths will be resolved relative to the project root (the nearest directory containing a `package.json` file).

Copy

```
const path = "./file.txt";
await Bun.write(path, "Lorem ipsum");
```

---

You can pass a `BunFile` as the destination. `Bun.write()` will write the data to its associated path.

Copy

```
const path = Bun.file("./file.txt");
await Bun.write(path, "Lorem ipsum");
```

---

`Bun.write()` returns the number of bytes written to disk.

Copy

```
const path = "./file.txt";
const bytes = await Bun.write(path, "Lorem ipsum");
// => 11
```

---

See [Docs > API > File I/O](https://bun.com/docs/runtime/file-io#writing-files-bun-write) for complete documentation of `Bun.write()`.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/write-file/basic.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/write-file/basic)

⌘I