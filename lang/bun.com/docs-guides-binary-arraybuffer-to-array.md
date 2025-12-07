---
url: https://bun.com/docs/guides/binary/arraybuffer-to-array
title: Convert an ArrayBuffer to an array of numbers - Bun
source_domain: bun.com
---

# Convert an ArrayBuffer to an array of numbers - Bun

To retrieve the contents of an `ArrayBuffer` as an array of numbers, create a [`Uint8Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array) over of the buffer. and use the [`Array.from()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from) method to convert it to an array.

Copy

```
const buf = new ArrayBuffer(64);
const arr = new Uint8Array(buf);
arr.length; // 64
arr[0]; // 0 (instantiated with all zeros)
```

---

The `Uint8Array` class supports array indexing and iteration. However if you wish to convert the instance to a regular `Array`, use `Array.from()`. (This will likely be slower than using the `Uint8Array` directly.)

Copy

```
const buf = new ArrayBuffer(64);
const uintArr = new Uint8Array(buf);
const regularArr = Array.from(uintArr);
// number[]
```

---

See [Docs > API > Binary Data](https://bun.com/docs/runtime/binary-data#conversion) for complete documentation on manipulating binary data with Bun.

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/binary/arraybuffer-to-array.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/binary/arraybuffer-to-array)

⌘I