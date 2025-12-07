---
url: https://bun.com/docs/guides/binary/typedarray-to-dataview
title: Convert a Uint8Array to a DataView - Bun
source_domain: bun.com
---

# Convert a Uint8Array to a DataView - Bun

A [`Uint8Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array) is a *typed array* class, meaning it is a mechanism for viewing data in an underlying `ArrayBuffer`. The following snippet creates a [`DataView`] instance over the same range of data as the `Uint8Array`.

Copy

```
const arr: Uint8Array = ...
const dv = new DataView(arr.buffer, arr.byteOffset, arr.byteLength);
```

---

See [Docs > API > Binary Data](https://bun.com/docs/runtime/binary-data#conversion) for complete documentation on manipulating binary data with Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/binary/typedarray-to-dataview.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/binary/typedarray-to-dataview)

⌘I