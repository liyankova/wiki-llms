---
url: https://bun.com/reference/node/string_decoder
title: Node.js string_decoder module | API Reference | Bun
source_domain: bun.com
---

# Node.js string_decoder module | API Reference | Bun

Node.js module

# [string\_decoder](https://bun.com/reference/node/string_decoder)

The `'node:string_decoder'` module provides the `StringDecoder` class, which decodes Buffer data into strings while preserving multi-byte UTF-8 and other encodings across buffer boundaries.

It ensures that decoded strings are not truncated or malformed when chunked data arrives in separate buffers.

Works in Bun

Fully implemented. 100% of Node.js's test suite passes.

* ### class [StringDecoder](https://bun.com/reference/node/string_decoder/StringDecoder)

  + [end](https://bun.com/reference/node/string_decoder/StringDecoder/end)(

    buffer?: string | ArrayBufferView<ArrayBufferLike>

    ): string;

    Returns any remaining input stored in the internal buffer as a string. Bytes representing incomplete UTF-8 and UTF-16 characters will be replaced with substitution characters appropriate for the character encoding.

    If the `buffer` argument is provided, one final call to `stringDecoder.write()` is performed before returning the remaining input. After `end()` is called, the `stringDecoder` object can be reused for new input.

    @param buffer

    The bytes to decode.
  + [write](https://bun.com/reference/node/string_decoder/StringDecoder/write)(

    buffer: string | ArrayBufferView<ArrayBufferLike>

    ): string;

    Returns a decoded string, ensuring that any incomplete multibyte characters at the end of the `Buffer`, or `TypedArray`, or `DataView` are omitted from the returned string and stored in an internal buffer for the next call to `stringDecoder.write()` or `stringDecoder.end()`.

    @param buffer

    The bytes to decode.