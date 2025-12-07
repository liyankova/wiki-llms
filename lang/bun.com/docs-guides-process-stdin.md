---
url: https://bun.com/docs/guides/process/stdin
title: Read from stdin - Bun
source_domain: bun.com
---

# Read from stdin - Bun

For CLI tools, it’s often useful to read from `stdin`. In Bun, the `console` object is an `AsyncIterable` that yields lines from `stdin`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)index.ts

Copy

```
const prompt = "Type something: ";
process.stdout.write(prompt);
for await (const line of console) {
  console.log(`You typed: ${line}`);
  process.stdout.write(prompt);
}
```

---

Running this file results in a never-ending interactive prompt that echoes whatever the user types.

terminal

Copy

```
bun run index.ts
```

Copy

```
Type something: hello
You typed: hello
Type something: hello again
You typed: hello again
```

---

Bun also exposes stdin as a `BunFile` via `Bun.stdin`. This is useful for incrementally reading large inputs that are piped into the `bun` process.
There is no guarantee that the chunks will be split line-by-line.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)stdin.ts

Copy

```
for await (const chunk of Bun.stdin.stream()) {
  // chunk is Uint8Array
  // this converts it to text (assumes ASCII encoding)
  const chunkText = Buffer.from(chunk).toString();
  console.log(`Chunk: ${chunkText}`);
}
```

---

This will print the input that is piped into the `bun` process.

terminal

Copy

```
echo "hello" | bun run stdin.ts
```

Copy

```
Chunk: hello
```

---

See [Docs > API > Utils](https://bun.com/docs/runtime/utils) for more useful utilities.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/process/stdin.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/process/stdin)

⌘I