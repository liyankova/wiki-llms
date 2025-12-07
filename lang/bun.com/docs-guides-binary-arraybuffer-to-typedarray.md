---
url: https://bun.com/docs/guides/binary/arraybuffer-to-typedarray
title: Convert an ArrayBuffer to a Uint8Array - Bun
source_domain: bun.com
---

# Convert an ArrayBuffer to a Uint8Array - Bun

A `Uint8Array` is a *typed array*, meaning it is a mechanism for viewing the data in an underlying `ArrayBuffer`.

Copy

```
const buffer = new ArrayBuffer(64);
const arr = new Uint8Array(buffer);
```

---

Instances of other typed arrays can be created similarly.

Copy

```
const buffer = new ArrayBuffer(64);

const arr1 = new Uint8Array(buffer);
const arr2 = new Uint16Array(buffer);
const arr3 = new Uint32Array(buffer);
const arr4 = new Float32Array(buffer);
const arr5 = new Float64Array(buffer);
const arr6 = new BigInt64Array(buffer);
const arr7 = new BigUint64Array(buffer);
```

---

To create a typed array that only views a portion of the underlying buffer, pass the offset and length to the constructor.

Copy

```
const buffer = new ArrayBuffer(64);
const arr = new Uint8Array(buffer, 0, 16); // view first 16 bytes
```

---

See [Docs > API > Utils](https://bun.com/docs/runtime/utils) for more useful utilities.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/binary/arraybuffer-to-typedarray.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/binary/arraybuffer-to-typedarray)

⌘I