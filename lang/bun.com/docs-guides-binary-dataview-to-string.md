---
url: https://bun.com/docs/guides/binary/dataview-to-string
title: Convert a DataView to a string - Bun
source_domain: bun.com
---

# Convert a DataView to a string - Bun

If a [`DataView`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DataView) contains ASCII-encoded text, you can convert it to a string using the [`TextDecoder`](https://developer.mozilla.org/en-US/docs/Web/API/TextDecoder) class.

Copy

```
const dv: DataView = ...;
const decoder = new TextDecoder();
const str = decoder.decode(dv);
```

---

See [Docs > API > Binary Data](https://bun.com/docs/runtime/binary-data#conversion) for complete documentation on manipulating binary data with Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/binary/dataview-to-string.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/binary/dataview-to-string)

⌘I