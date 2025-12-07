---
url: https://bun.com/docs/guides/write-file/append
title: Append content to a file - Bun
source_domain: bun.com
---

# Append content to a file - Bun

Bun implements the `node:fs` module, which includes the `fs.appendFile` and `fs.appendFileSync` functions for appending content to files.

---

You can use `fs.appendFile` to asynchronously append data to a file, creating the file if it does not yet exist. The content can be a string or a `Buffer`.

Copy

```
import { appendFile } from "node:fs/promises";

await appendFile("message.txt", "data to append");
```

---

To use the non-`Promise` API:

Copy

```
import { appendFile } from "node:fs";

appendFile("message.txt", "data to append", err => {
  if (err) throw err;
  console.log('The "data to append" was appended to file!');
});
```

---

To specify the encoding of the content:

Copy

```
import { appendFile } from "node:fs";

appendFile("message.txt", "data to append", "utf8", callback);
```

---

To append the data synchronously, use `fs.appendFileSync`:

Copy

```
import { appendFileSync } from "node:fs";

appendFileSync("message.txt", "data to append", "utf8");
```

---

See the [Node.js documentation](https://nodejs.org/api/fs.html#fspromisesappendfilepath-data-options) for more information.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/write-file/append.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/write-file/append)

⌘I