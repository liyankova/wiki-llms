---
url: https://bun.com/docs/guides/binary/typedarray-to-string
title: Convert a Uint8Array to a string - Bun
source_domain: bun.com
---

# Convert a Uint8Array to a string - Bun

Bun implements the Web-standard [`TextDecoder`](https://developer.mozilla.org/en-US/docs/Web/API/TextDecoder) class for converting from binary data types like `Uint8Array` and strings.

Copy

```
const arr = new Uint8Array([104, 101, 108, 108, 111]);
const decoder = new TextDecoder();
const str = decoder.decode(arr);
// => "hello"
```

---

See [Docs > API > Binary Data](https://bun.com/docs/runtime/binary-data#conversion) for complete documentation on manipulating binary data with Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/binary/typedarray-to-string.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/binary/typedarray-to-string)

⌘I