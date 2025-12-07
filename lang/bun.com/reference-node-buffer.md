---
url: https://bun.com/reference/node/buffer
title: Node.js buffer module | API Reference | Bun
source_domain: bun.com
---

# Node.js buffer module | API Reference | Bun

Node.js module

# [buffer](https://bun.com/reference/node/buffer)

The `'node:buffer'` module provides a way to handle raw binary data directly in memory. Buffers are instances of the `Buffer` class, which is a fixed-length sequence of bytes.

The module includes methods to create, read, write, concatenate, and compare buffers. It is fundamental for I/O operations, such as reading files, handling network streams, and interfacing with C++ addons.

Works in Bun

Fully implemented.

* ### class [Blob](https://bun.com/reference/node/buffer/Blob)

  A `Blob` encapsulates immutable, raw data that can be safely shared across multiple worker threads.

  + readonly [size](https://bun.com/reference/node/buffer/Blob/size): number

    The total size of the `Blob` in bytes.
  + readonly [type](https://bun.com/reference/node/buffer/Blob/type): string

    The content-type of the `Blob`.
  + [arrayBuffer](https://bun.com/reference/node/buffer/Blob/arrayBuffer)(): Promise<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Consume the blob as an ArrayBuffer
  + [bytes](https://bun.com/reference/node/buffer/Blob/bytes)(): Promise<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>>;

    The `blob.bytes()` method returns the byte of the `Blob` object as a `Promise<Uint8Array>`.

    ```
    const blob = new Blob(['hello']);
    blob.bytes().then((bytes) => {
      console.log(bytes); // Outputs: Uint8Array(5) [ 104, 101, 108, 108, 111 ]
    });
    ```

    [bytes](https://bun.com/reference/node/buffer/Blob/bytes)(): Promise<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>>;

    Consume as a Uint8Array, backed by an ArrayBuffer
  + [formData](https://bun.com/reference/node/buffer/Blob/formData)(): Promise<[FormData](https://bun.com/reference/globals/FormData)>;

    Consume the blob as a FormData instance
  + [json](https://bun.com/reference/node/buffer/Blob/json)(): Promise<any>;

    Consume as JSON
  + [slice](https://bun.com/reference/node/buffer/Blob/slice)(

    start?: number,

    end?: number,

    type?: string

    ): [Blob](https://bun.com/reference/node/buffer/Blob);

    Creates and returns a new `Blob` containing a subset of this `Blob` objects data. The original `Blob` is not altered.

    @param start

    The starting index.

    @param end

    The ending index.

    @param type

    The content-type for the new `Blob`
  + [stream](https://bun.com/reference/node/buffer/Blob/stream)(): [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream);

    Returns a new `ReadableStream` that allows the content of the `Blob` to be read.

    [stream](https://bun.com/reference/node/buffer/Blob/stream)(): [ReadableStream](https://bun.com/reference/globals/ReadableStream)<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>>;

    Returns a readable stream of the blob's contents
  + [text](https://bun.com/reference/node/buffer/Blob/text)(): Promise<string>;

    Returns a promise that fulfills with the contents of the `Blob` decoded as a UTF-8 string.
* ### class [File](https://bun.com/reference/node/buffer/File)

  A [`File`](https://developer.mozilla.org/en-US/docs/Web/API/File) provides information about files.

  + readonly [lastModified](https://bun.com/reference/node/buffer/File/lastModified): number

    The last modified date of the `File`.
  + readonly [name](https://bun.com/reference/node/buffer/File/name): string

    The name of the `File`.
  + readonly [size](https://bun.com/reference/node/buffer/File/size): number

    The total size of the `Blob` in bytes.
  + readonly [type](https://bun.com/reference/node/buffer/File/type): string

    The content-type of the `Blob`.
  + [arrayBuffer](https://bun.com/reference/node/buffer/File/arrayBuffer)(): Promise<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Consume the blob as an ArrayBuffer
  + [bytes](https://bun.com/reference/node/buffer/File/bytes)(): Promise<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>>;

    The `blob.bytes()` method returns the byte of the `Blob` object as a `Promise<Uint8Array>`.

    ```
    const blob = new Blob(['hello']);
    blob.bytes().then((bytes) => {
      console.log(bytes); // Outputs: Uint8Array(5) [ 104, 101, 108, 108, 111 ]
    });
    ```

    [bytes](https://bun.com/reference/node/buffer/File/bytes)(): Promise<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>>;

    Consume as a Uint8Array, backed by an ArrayBuffer
  + [formData](https://bun.com/reference/node/buffer/File/formData)(): Promise<[FormData](https://bun.com/reference/globals/FormData)>;

    Consume the blob as a FormData instance
  + [json](https://bun.com/reference/node/buffer/File/json)(): Promise<any>;

    Consume as JSON
  + [slice](https://bun.com/reference/node/buffer/File/slice)(

    start?: number,

    end?: number,

    type?: string

    ): [Blob](https://bun.com/reference/node/buffer/Blob);

    Creates and returns a new `Blob` containing a subset of this `Blob` objects data. The original `Blob` is not altered.

    @param start

    The starting index.

    @param end

    The ending index.

    @param type

    The content-type for the new `Blob`
  + [stream](https://bun.com/reference/node/buffer/File/stream)(): [ReadableStream](https://bun.com/reference/node/stream/web/ReadableStream);

    Returns a new `ReadableStream` that allows the content of the `Blob` to be read.

    [stream](https://bun.com/reference/node/buffer/File/stream)(): [ReadableStream](https://bun.com/reference/globals/ReadableStream)<[Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>>;

    Returns a readable stream of the blob's contents
  + [text](https://bun.com/reference/node/buffer/File/text)(): Promise<string>;

    Returns a promise that fulfills with the contents of the `Blob` decoded as a UTF-8 string.
* const [Buffer](https://bun.com/reference/node/buffer/Buffer): BufferConstructor
* const [constants](https://bun.com/reference/node/buffer/constants): { MAX\_LENGTH: number; MAX\_STRING\_LENGTH: number }
* const [INSPECT\_MAX\_BYTES](https://bun.com/reference/node/buffer/INSPECT_MAX_BYTES): number
* const [kMaxLength](https://bun.com/reference/node/buffer/kMaxLength): number
* const [kStringMaxLength](https://bun.com/reference/node/buffer/kStringMaxLength): number
* function [atob](https://bun.com/reference/node/buffer/atob)(

  data: string

  ): string;

  Decodes a string of Base64-encoded data into bytes, and encodes those bytes into a string using Latin-1 (ISO-8859-1).

  The `data` may be any JavaScript-value that can be coerced into a string.

  **This function is only provided for compatibility with legacy web platform APIs** **and should never be used in new code, because they use strings to represent** **binary data and predate the introduction of typed arrays in JavaScript.** **For code running using Node.js APIs, converting between base64-encoded strings** **and binary data should be performed using `Buffer.from(str, 'base64')` and `buf.toString('base64')`.**

  @param data

  The Base64-encoded input string.
* function [btoa](https://bun.com/reference/node/buffer/btoa)(

  data: string

  ): string;

  Decodes a string into bytes using Latin-1 (ISO-8859), and encodes those bytes into a string using Base64.

  The `data` may be any JavaScript-value that can be coerced into a string.

  **This function is only provided for compatibility with legacy web platform APIs** **and should never be used in new code, because they use strings to represent** **binary data and predate the introduction of typed arrays in JavaScript.** **For code running using Node.js APIs, converting between base64-encoded strings** **and binary data should be performed using `Buffer.from(str, 'base64')` and `buf.toString('base64')`.**

  @param data

  An ASCII (Latin1) string.
* function [isAscii](https://bun.com/reference/node/buffer/isAscii)(

  input: [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer) | TypedArray<ArrayBufferLike>

  ): boolean;

  This function returns `true` if `input` contains only valid ASCII-encoded data, including the case in which `input` is empty.

  Throws if the `input` is a detached array buffer.

  @param input

  The input to validate.
* function [isUtf8](https://bun.com/reference/node/buffer/isUtf8)(

  input: [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer) | TypedArray<ArrayBufferLike>

  ): boolean;

  This function returns `true` if `input` contains only valid UTF-8-encoded data, including the case in which `input` is empty.

  Throws if the `input` is a detached array buffer.

  @param input

  The input to validate.
* function [resolveObjectURL](https://bun.com/reference/node/buffer/resolveObjectURL)(

  id: string

  ): undefined | [Blob](https://bun.com/reference/node/buffer/Blob);

  Resolves a `'blob:nodedata:...'` an associated `Blob` object registered using a prior call to `URL.createObjectURL()`.

  @param id

  A `'blob:nodedata:...` URL string returned by a prior call to `URL.createObjectURL()`.
* function [transcode](https://bun.com/reference/node/buffer/transcode)(

  source: [Uint8Array](https://bun.com/reference/globals/Uint8Array),

  fromEnc: [TranscodeEncoding](https://bun.com/reference/node/buffer/TranscodeEncoding),

  toEnc: [TranscodeEncoding](https://bun.com/reference/node/buffer/TranscodeEncoding)

  ): NonSharedBuffer;

  Re-encodes the given `Buffer` or `Uint8Array` instance from one character encoding to another. Returns a new `Buffer` instance.

  Throws if the `fromEnc` or `toEnc` specify invalid character encodings or if conversion from `fromEnc` to `toEnc` is not permitted.

  Encodings supported by `buffer.transcode()` are: `'ascii'`, `'utf8'`, `'utf16le'`, `'ucs2'`, `'latin1'`, and `'binary'`.

  The transcoding process will use substitution characters if a given byte sequence cannot be adequately represented in the target encoding. For instance:

  ```
  import { Buffer, transcode } from 'node:buffer';

  const newBuf = transcode(Buffer.from('€'), 'utf8', 'ascii');
  console.log(newBuf.toString('ascii'));
  // Prints: '?'
  ```

  Because the Euro (`€`) sign is not representable in US-ASCII, it is replaced with `?` in the transcoded `Buffer`.

  @param source

  A `Buffer` or `Uint8Array` instance.

  @param fromEnc

  The current encoding.

  @param toEnc

  To target encoding.

## Type definitions

* ### interface [BlobOptions](https://bun.com/reference/node/buffer/BlobOptions)

  + [endings](https://bun.com/reference/node/buffer/BlobOptions/endings)?: 'transparent' | 'native'

    One of either `'transparent'` or `'native'`. When set to `'native'`, line endings in string source parts will be converted to the platform native line-ending as specified by `import { EOL } from 'node:os'`.
  + [type](https://bun.com/reference/node/buffer/BlobOptions/type)?: string

    The Blob content-type. The intent is for `type` to convey the MIME media type of the data, however no validation of the type format is performed.
* ### interface [Buffer](https://bun.com/reference/node/buffer/Buffer)<TArrayBuffer extends ArrayBufferLike = ArrayBufferLike>

  A typed array of 8-bit unsigned integer values. The contents are initialized to 0. If the requested number of bytes could not be allocated an exception is raised.

  + readonly [[Symbol.toStringTag]](https://bun.com/reference/node/buffer/Buffer/[toStringTag]): 'Uint8Array'
  + readonly [buffer](https://bun.com/reference/node/buffer/Buffer/buffer): TArrayBuffer

    The ArrayBuffer instance referenced by the array.
  + readonly [byteLength](https://bun.com/reference/node/buffer/Buffer/byteLength): number

    The length in bytes of the array.
  + readonly [byteOffset](https://bun.com/reference/node/buffer/Buffer/byteOffset): number

    The offset in bytes of the array.
  + readonly [BYTES\_PER\_ELEMENT](https://bun.com/reference/node/buffer/Buffer/BYTES_PER_ELEMENT): number

    The size in bytes of each element in the array.
  + readonly [length](https://bun.com/reference/node/buffer/Buffer/length): number

    The length of the array.
  + [[Symbol.iterator]](https://bun.com/reference/node/buffer/Buffer/[iterator])(): ArrayIterator<number>;
  + [at](https://bun.com/reference/node/buffer/Buffer/at)(

    index: number

    ): undefined | number;

    Returns the item located at the specified index.

    @param index

    The zero-based index of the desired code unit. A negative index will count back from the last item.
  + [compare](https://bun.com/reference/node/buffer/Buffer/compare)(

    target: [Uint8Array](https://bun.com/reference/globals/Uint8Array),

    targetStart?: number,

    targetEnd?: number,

    sourceStart?: number,

    sourceEnd?: number

    ): -1 | 0 | 1;

    Compares `buf` with `target` and returns a number indicating whether `buf`comes before, after, or is the same as `target` in sort order. Comparison is based on the actual sequence of bytes in each `Buffer`.

    - `0` is returned if `target` is the same as `buf`
    - `1` is returned if `target` should come *before*`buf` when sorted.
    - `-1` is returned if `target` should come *after*`buf` when sorted.

    ```
    import { Buffer } from 'node:buffer';

    const buf1 = Buffer.from('ABC');
    const buf2 = Buffer.from('BCD');
    const buf3 = Buffer.from('ABCD');

    console.log(buf1.compare(buf1));
    // Prints: 0
    console.log(buf1.compare(buf2));
    // Prints: -1
    console.log(buf1.compare(buf3));
    // Prints: -1
    console.log(buf2.compare(buf1));
    // Prints: 1
    console.log(buf2.compare(buf3));
    // Prints: 1
    console.log([buf1, buf2, buf3].sort(Buffer.compare));
    // Prints: [ <Buffer 41 42 43>, <Buffer 41 42 43 44>, <Buffer 42 43 44> ]
    // (This result is equal to: [buf1, buf3, buf2].)
    ```

    The optional `targetStart`, `targetEnd`, `sourceStart`, and `sourceEnd` arguments can be used to limit the comparison to specific ranges within `target` and `buf` respectively.

    ```
    import { Buffer } from 'node:buffer';

    const buf1 = Buffer.from([1, 2, 3, 4, 5, 6, 7, 8, 9]);
    const buf2 = Buffer.from([5, 6, 7, 8, 9, 1, 2, 3, 4]);

    console.log(buf1.compare(buf2, 5, 9, 0, 4));
    // Prints: 0
    console.log(buf1.compare(buf2, 0, 6, 4));
    // Prints: -1
    console.log(buf1.compare(buf2, 5, 6, 5));
    // Prints: 1
    ```

    `ERR_OUT_OF_RANGE` is thrown if `targetStart < 0`, `sourceStart < 0`, `targetEnd > target.byteLength`, or `sourceEnd > source.byteLength`.

    @param target

    A `Buffer` or Uint8Array with which to compare `buf`.

    @param targetStart

    The offset within `target` at which to begin comparison.

    @param targetEnd

    The offset within `target` at which to end comparison (not inclusive).

    @param sourceStart

    The offset within `buf` at which to begin comparison.

    @param sourceEnd

    The offset within `buf` at which to end comparison (not inclusive).
  + [copy](https://bun.com/reference/node/buffer/Buffer/copy)(

    target: [Uint8Array](https://bun.com/reference/globals/Uint8Array),

    targetStart?: number,

    sourceStart?: number,

    sourceEnd?: number

    ): number;

    Copies data from a region of `buf` to a region in `target`, even if the `target`memory region overlaps with `buf`.

    [`TypedArray.prototype.set()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray/set) performs the same operation, and is available for all TypedArrays, including Node.js `Buffer`s, although it takes different function arguments.

    ```
    import { Buffer } from 'node:buffer';

    // Create two `Buffer` instances.
    const buf1 = Buffer.allocUnsafe(26);
    const buf2 = Buffer.allocUnsafe(26).fill('!');

    for (let i = 0; i < 26; i++) {
      // 97 is the decimal ASCII value for 'a'.
      buf1[i] = i + 97;
    }

    // Copy `buf1` bytes 16 through 19 into `buf2` starting at byte 8 of `buf2`.
    buf1.copy(buf2, 8, 16, 20);
    // This is equivalent to:
    // buf2.set(buf1.subarray(16, 20), 8);

    console.log(buf2.toString('ascii', 0, 25));
    // Prints: !!!!!!!!qrst!!!!!!!!!!!!!
    ```

    ```
    import { Buffer } from 'node:buffer';

    // Create a `Buffer` and copy data from one region to an overlapping region
    // within the same `Buffer`.

    const buf = Buffer.allocUnsafe(26);

    for (let i = 0; i < 26; i++) {
      // 97 is the decimal ASCII value for 'a'.
      buf[i] = i + 97;
    }

    buf.copy(buf, 0, 4, 10);

    console.log(buf.toString());
    // Prints: efghijghijklmnopqrstuvwxyz
    ```

    @param target

    A `Buffer` or Uint8Array to copy into.

    @param targetStart

    The offset within `target` at which to begin writing.

    @param sourceStart

    The offset within `buf` from which to begin copying.

    @param sourceEnd

    The offset within `buf` at which to stop copying (not inclusive).

    @returns

    The number of bytes copied.
  + [copyWithin](https://bun.com/reference/node/buffer/Buffer/copyWithin)(

    target: number,

    start: number,

    end?: number

    ): this;

    Returns the this object after copying a section of the array identified by start and end to the same array starting at position target

    @param target

    If target is negative, it is treated as length+target where length is the length of the array.

    @param start

    If start is negative, it is treated as length+start. If end is negative, it is treated as length+end.

    @param end

    If not specified, length of the this object is used as its default value.
  + [entries](https://bun.com/reference/node/buffer/Buffer/entries)(): ArrayIterator<[number, number]>;

    Returns an array of key, value pairs for every entry in the array
  + [equals](https://bun.com/reference/node/buffer/Buffer/equals)(

    otherBuffer: [Uint8Array](https://bun.com/reference/globals/Uint8Array)

    ): boolean;

    Returns `true` if both `buf` and `otherBuffer` have exactly the same bytes,`false` otherwise. Equivalent to `buf.compare(otherBuffer) === 0`.

    ```
    import { Buffer } from 'node:buffer';

    const buf1 = Buffer.from('ABC');
    const buf2 = Buffer.from('414243', 'hex');
    const buf3 = Buffer.from('ABCD');

    console.log(buf1.equals(buf2));
    // Prints: true
    console.log(buf1.equals(buf3));
    // Prints: false
    ```

    @param otherBuffer

    A `Buffer` or Uint8Array with which to compare `buf`.
  + [every](https://bun.com/reference/node/buffer/Buffer/every)(

    predicate: (value: number, index: number, array: this) => unknown,

    thisArg?: any

    ): boolean;

    Determines whether all the members of an array satisfy the specified test.

    @param predicate

    A function that accepts up to three arguments. The every method calls the predicate function for each element in the array until the predicate returns a value which is coercible to the Boolean value false, or until the end of the array.

    @param thisArg

    An object to which the this keyword can refer in the predicate function. If thisArg is omitted, undefined is used as the this value.
  + [fill](https://bun.com/reference/node/buffer/Buffer/fill)(

    value: string | number | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

    offset?: number,

    end?: number,

    encoding?: BufferEncoding

    ): this;

    Fills `buf` with the specified `value`. If the `offset` and `end` are not given, the entire `buf` will be filled:

    ```
    import { Buffer } from 'node:buffer';

    // Fill a `Buffer` with the ASCII character 'h'.

    const b = Buffer.allocUnsafe(50).fill('h');

    console.log(b.toString());
    // Prints: hhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhh

    // Fill a buffer with empty string
    const c = Buffer.allocUnsafe(5).fill('');

    console.log(c.fill(''));
    // Prints: <Buffer 00 00 00 00 00>
    ```

    `value` is coerced to a `uint32` value if it is not a string, `Buffer`, or integer. If the resulting integer is greater than `255` (decimal), `buf` will be filled with `value &#x26; 255`.

    If the final write of a `fill()` operation falls on a multi-byte character, then only the bytes of that character that fit into `buf` are written:

    ```
    import { Buffer } from 'node:buffer';

    // Fill a `Buffer` with character that takes up two bytes in UTF-8.

    console.log(Buffer.allocUnsafe(5).fill('\u0222'));
    // Prints: <Buffer c8 a2 c8 a2 c8>
    ```

    If `value` contains invalid characters, it is truncated; if no valid fill data remains, an exception is thrown:

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(5);

    console.log(buf.fill('a'));
    // Prints: <Buffer 61 61 61 61 61>
    console.log(buf.fill('aazz', 'hex'));
    // Prints: <Buffer aa aa aa aa aa>
    console.log(buf.fill('zz', 'hex'));
    // Throws an exception.
    ```

    @param value

    The value with which to fill `buf`. Empty value (string, Uint8Array, Buffer) is coerced to `0`.

    @param offset

    Number of bytes to skip before starting to fill `buf`.

    @param end

    Where to stop filling `buf` (not inclusive).

    @param encoding

    The encoding for `value` if `value` is a string.

    @returns

    A reference to `buf`.

    [fill](https://bun.com/reference/node/buffer/Buffer/fill)(

    value: string | number | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

    offset: number,

    encoding: BufferEncoding

    ): this;

    [fill](https://bun.com/reference/node/buffer/Buffer/fill)(

    value: string | number | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

    encoding: BufferEncoding

    ): this;
  + [filter](https://bun.com/reference/node/buffer/Buffer/filter)(

    predicate: (value: number, index: number, array: this) => any,

    thisArg?: any

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Returns the elements of an array that meet the condition specified in a callback function.

    @param predicate

    A function that accepts up to three arguments. The filter method calls the predicate function one time for each element in the array.

    @param thisArg

    An object to which the this keyword can refer in the predicate function. If thisArg is omitted, undefined is used as the this value.
  + [find](https://bun.com/reference/node/buffer/Buffer/find)(

    predicate: (value: number, index: number, obj: this) => boolean,

    thisArg?: any

    ): undefined | number;

    Returns the value of the first element in the array where predicate is true, and undefined otherwise.

    @param predicate

    find calls predicate once for each element of the array, in ascending order, until it finds one where predicate returns true. If such an element is found, find immediately returns that element value. Otherwise, find returns undefined.

    @param thisArg

    If provided, it will be used as the this value for each invocation of predicate. If it is not provided, undefined is used instead.
  + [findIndex](https://bun.com/reference/node/buffer/Buffer/findIndex)(

    predicate: (value: number, index: number, obj: this) => boolean,

    thisArg?: any

    ): number;

    Returns the index of the first element in the array where predicate is true, and -1 otherwise.

    @param predicate

    find calls predicate once for each element of the array, in ascending order, until it finds one where predicate returns true. If such an element is found, findIndex immediately returns that element index. Otherwise, findIndex returns -1.

    @param thisArg

    If provided, it will be used as the this value for each invocation of predicate. If it is not provided, undefined is used instead.
  + [findLast](https://bun.com/reference/node/buffer/Buffer/findLast)<S extends number>(

    predicate: (value: number, index: number, array: this) => value is S,

    thisArg?: any

    ): undefined | S;

    Returns the value of the last element in the array where predicate is true, and undefined otherwise.

    @param predicate

    findLast calls predicate once for each element of the array, in descending order, until it finds one where predicate returns true. If such an element is found, findLast immediately returns that element value. Otherwise, findLast returns undefined.

    @param thisArg

    If provided, it will be used as the this value for each invocation of predicate. If it is not provided, undefined is used instead.

    [findLast](https://bun.com/reference/node/buffer/Buffer/findLast)(

    predicate: (value: number, index: number, array: this) => unknown,

    thisArg?: any

    ): undefined | number;
  + [findLastIndex](https://bun.com/reference/node/buffer/Buffer/findLastIndex)(

    predicate: (value: number, index: number, array: this) => unknown,

    thisArg?: any

    ): number;

    Returns the index of the last element in the array where predicate is true, and -1 otherwise.

    @param predicate

    findLastIndex calls predicate once for each element of the array, in descending order, until it finds one where predicate returns true. If such an element is found, findLastIndex immediately returns that element index. Otherwise, findLastIndex returns -1.

    @param thisArg

    If provided, it will be used as the this value for each invocation of predicate. If it is not provided, undefined is used instead.
  + [forEach](https://bun.com/reference/node/buffer/Buffer/forEach)(

    callbackfn: (value: number, index: number, array: this) => void,

    thisArg?: any

    ): void;

    Performs the specified action for each element in an array.

    @param callbackfn

    A function that accepts up to three arguments. forEach calls the callbackfn function one time for each element in the array.

    @param thisArg

    An object to which the this keyword can refer in the callbackfn function. If thisArg is omitted, undefined is used as the this value.
  + [includes](https://bun.com/reference/node/buffer/Buffer/includes)(

    value: string | number | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>,

    byteOffset?: number,

    encoding?: BufferEncoding

    ): boolean;

    Equivalent to `buf.indexOf() !== -1`.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from('this is a buffer');

    console.log(buf.includes('this'));
    // Prints: true
    console.log(buf.includes('is'));
    // Prints: true
    console.log(buf.includes(Buffer.from('a buffer')));
    // Prints: true
    console.log(buf.includes(97));
    // Prints: true (97 is the decimal ASCII value for 'a')
    console.log(buf.includes(Buffer.from('a buffer example')));
    // Prints: false
    console.log(buf.includes(Buffer.from('a buffer example').slice(0, 8)));
    // Prints: true
    console.log(buf.includes('this', 4));
    // Prints: false
    ```

    @param value

    What to search for.

    @param byteOffset

    Where to begin searching in `buf`. If negative, then offset is calculated from the end of `buf`.

    @param encoding

    If `value` is a string, this is its encoding.

    @returns

    `true` if `value` was found in `buf`, `false` otherwise.

    [includes](https://bun.com/reference/node/buffer/Buffer/includes)(

    value: string | number | [Buffer](https://bun.com/reference/node/buffer/Buffer)<ArrayBufferLike>,

    encoding: BufferEncoding

    ): boolean;
  + [indexOf](https://bun.com/reference/node/buffer/Buffer/indexOf)(

    value: string | number | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

    byteOffset?: number,

    encoding?: BufferEncoding

    ): number;

    If `value` is:

    - a string, `value` is interpreted according to the character encoding in `encoding`.
    - a `Buffer` or [`Uint8Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array), `value` will be used in its entirety. To compare a partial `Buffer`, use `buf.subarray`.
    - a number, `value` will be interpreted as an unsigned 8-bit integer value between `0` and `255`.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from('this is a buffer');

    console.log(buf.indexOf('this'));
    // Prints: 0
    console.log(buf.indexOf('is'));
    // Prints: 2
    console.log(buf.indexOf(Buffer.from('a buffer')));
    // Prints: 8
    console.log(buf.indexOf(97));
    // Prints: 8 (97 is the decimal ASCII value for 'a')
    console.log(buf.indexOf(Buffer.from('a buffer example')));
    // Prints: -1
    console.log(buf.indexOf(Buffer.from('a buffer example').slice(0, 8)));
    // Prints: 8

    const utf16Buffer = Buffer.from('\u039a\u0391\u03a3\u03a3\u0395', 'utf16le');

    console.log(utf16Buffer.indexOf('\u03a3', 0, 'utf16le'));
    // Prints: 4
    console.log(utf16Buffer.indexOf('\u03a3', -4, 'utf16le'));
    // Prints: 6
    ```

    If `value` is not a string, number, or `Buffer`, this method will throw a `TypeError`. If `value` is a number, it will be coerced to a valid byte value, an integer between 0 and 255.

    If `byteOffset` is not a number, it will be coerced to a number. If the result of coercion is `NaN` or `0`, then the entire buffer will be searched. This behavior matches [`String.prototype.indexOf()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/indexOf).

    ```
    import { Buffer } from 'node:buffer';

    const b = Buffer.from('abcdef');

    // Passing a value that's a number, but not a valid byte.
    // Prints: 2, equivalent to searching for 99 or 'c'.
    console.log(b.indexOf(99.9));
    console.log(b.indexOf(256 + 99));

    // Passing a byteOffset that coerces to NaN or 0.
    // Prints: 1, searching the whole buffer.
    console.log(b.indexOf('b', undefined));
    console.log(b.indexOf('b', {}));
    console.log(b.indexOf('b', null));
    console.log(b.indexOf('b', []));
    ```

    If `value` is an empty string or empty `Buffer` and `byteOffset` is less than `buf.length`, `byteOffset` will be returned. If `value` is empty and`byteOffset` is at least `buf.length`, `buf.length` will be returned.

    @param value

    What to search for.

    @param byteOffset

    Where to begin searching in `buf`. If negative, then offset is calculated from the end of `buf`.

    @param encoding

    If `value` is a string, this is the encoding used to determine the binary representation of the string that will be searched for in `buf`.

    @returns

    The index of the first occurrence of `value` in `buf`, or `-1` if `buf` does not contain `value`.

    [indexOf](https://bun.com/reference/node/buffer/Buffer/indexOf)(

    value: string | number | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

    encoding: BufferEncoding

    ): number;
  + [join](https://bun.com/reference/node/buffer/Buffer/join)(

    separator?: string

    ): string;

    Adds all the elements of an array separated by the specified separator string.

    @param separator

    A string used to separate one element of an array from the next in the resulting String. If omitted, the array elements are separated with a comma.
  + [keys](https://bun.com/reference/node/buffer/Buffer/keys)(): ArrayIterator<number>;

    Returns an list of keys in the array
  + [lastIndexOf](https://bun.com/reference/node/buffer/Buffer/lastIndexOf)(

    value: string | number | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

    byteOffset?: number,

    encoding?: BufferEncoding

    ): number;

    Identical to `buf.indexOf()`, except the last occurrence of `value` is found rather than the first occurrence.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from('this buffer is a buffer');

    console.log(buf.lastIndexOf('this'));
    // Prints: 0
    console.log(buf.lastIndexOf('buffer'));
    // Prints: 17
    console.log(buf.lastIndexOf(Buffer.from('buffer')));
    // Prints: 17
    console.log(buf.lastIndexOf(97));
    // Prints: 15 (97 is the decimal ASCII value for 'a')
    console.log(buf.lastIndexOf(Buffer.from('yolo')));
    // Prints: -1
    console.log(buf.lastIndexOf('buffer', 5));
    // Prints: 5
    console.log(buf.lastIndexOf('buffer', 4));
    // Prints: -1

    const utf16Buffer = Buffer.from('\u039a\u0391\u03a3\u03a3\u0395', 'utf16le');

    console.log(utf16Buffer.lastIndexOf('\u03a3', undefined, 'utf16le'));
    // Prints: 6
    console.log(utf16Buffer.lastIndexOf('\u03a3', -5, 'utf16le'));
    // Prints: 4
    ```

    If `value` is not a string, number, or `Buffer`, this method will throw a `TypeError`. If `value` is a number, it will be coerced to a valid byte value, an integer between 0 and 255.

    If `byteOffset` is not a number, it will be coerced to a number. Any arguments that coerce to `NaN`, like `{}` or `undefined`, will search the whole buffer. This behavior matches [`String.prototype.lastIndexOf()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/lastIndexOf).

    ```
    import { Buffer } from 'node:buffer';

    const b = Buffer.from('abcdef');

    // Passing a value that's a number, but not a valid byte.
    // Prints: 2, equivalent to searching for 99 or 'c'.
    console.log(b.lastIndexOf(99.9));
    console.log(b.lastIndexOf(256 + 99));

    // Passing a byteOffset that coerces to NaN.
    // Prints: 1, searching the whole buffer.
    console.log(b.lastIndexOf('b', undefined));
    console.log(b.lastIndexOf('b', {}));

    // Passing a byteOffset that coerces to 0.
    // Prints: -1, equivalent to passing 0.
    console.log(b.lastIndexOf('b', null));
    console.log(b.lastIndexOf('b', []));
    ```

    If `value` is an empty string or empty `Buffer`, `byteOffset` will be returned.

    @param value

    What to search for.

    @param byteOffset

    Where to begin searching in `buf`. If negative, then offset is calculated from the end of `buf`.

    @param encoding

    If `value` is a string, this is the encoding used to determine the binary representation of the string that will be searched for in `buf`.

    @returns

    The index of the last occurrence of `value` in `buf`, or `-1` if `buf` does not contain `value`.

    [lastIndexOf](https://bun.com/reference/node/buffer/Buffer/lastIndexOf)(

    value: string | number | [Uint8Array](https://bun.com/reference/globals/Uint8Array)<ArrayBufferLike>,

    encoding: BufferEncoding

    ): number;
  + [map](https://bun.com/reference/node/buffer/Buffer/map)(

    callbackfn: (value: number, index: number, array: this) => number,

    thisArg?: any

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Calls a defined callback function on each element of an array, and returns an array that contains the results.

    @param callbackfn

    A function that accepts up to three arguments. The map method calls the callbackfn function one time for each element in the array.

    @param thisArg

    An object to which the this keyword can refer in the callbackfn function. If thisArg is omitted, undefined is used as the this value.
  + [readBigInt64BE](https://bun.com/reference/node/buffer/Buffer/readBigInt64BE)(

    offset?: number

    ): bigint;

    Reads a signed, big-endian 64-bit integer from `buf` at the specified `offset`.

    Integers read from a `Buffer` are interpreted as two's complement signed values.

    @param offset

    Number of bytes to skip before starting to read. Must satisfy: `0 <= offset <= buf.length - 8`.
  + [readBigInt64LE](https://bun.com/reference/node/buffer/Buffer/readBigInt64LE)(

    offset?: number

    ): bigint;

    Reads a signed, little-endian 64-bit integer from `buf` at the specified`offset`.

    Integers read from a `Buffer` are interpreted as two's complement signed values.

    @param offset

    Number of bytes to skip before starting to read. Must satisfy: `0 <= offset <= buf.length - 8`.
  + [readBigUint64BE](https://bun.com/reference/node/buffer/Buffer/readBigUint64BE)(

    offset?: number

    ): bigint;
  + [readBigUInt64BE](https://bun.com/reference/node/buffer/Buffer/readBigUInt64BE)(

    offset?: number

    ): bigint;

    Reads an unsigned, big-endian 64-bit integer from `buf` at the specified`offset`.

    This function is also available under the `readBigUint64BE` alias.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from([0x00, 0x00, 0x00, 0x00, 0xff, 0xff, 0xff, 0xff]);

    console.log(buf.readBigUInt64BE(0));
    // Prints: 4294967295n
    ```

    @param offset

    Number of bytes to skip before starting to read. Must satisfy: `0 <= offset <= buf.length - 8`.
  + [readBigUint64LE](https://bun.com/reference/node/buffer/Buffer/readBigUint64LE)(

    offset?: number

    ): bigint;
  + [readBigUInt64LE](https://bun.com/reference/node/buffer/Buffer/readBigUInt64LE)(

    offset?: number

    ): bigint;

    Reads an unsigned, little-endian 64-bit integer from `buf` at the specified`offset`.

    This function is also available under the `readBigUint64LE` alias.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from([0x00, 0x00, 0x00, 0x00, 0xff, 0xff, 0xff, 0xff]);

    console.log(buf.readBigUInt64LE(0));
    // Prints: 18446744069414584320n
    ```

    @param offset

    Number of bytes to skip before starting to read. Must satisfy: `0 <= offset <= buf.length - 8`.
  + [readDoubleBE](https://bun.com/reference/node/buffer/Buffer/readDoubleBE)(

    offset?: number

    ): number;

    Reads a 64-bit, big-endian double from `buf` at the specified `offset`.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from([1, 2, 3, 4, 5, 6, 7, 8]);

    console.log(buf.readDoubleBE(0));
    // Prints: 8.20788039913184e-304
    ```

    @param offset

    Number of bytes to skip before starting to read. Must satisfy `0 <= offset <= buf.length - 8`.
  + [readDoubleLE](https://bun.com/reference/node/buffer/Buffer/readDoubleLE)(

    offset?: number

    ): number;

    Reads a 64-bit, little-endian double from `buf` at the specified `offset`.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from([1, 2, 3, 4, 5, 6, 7, 8]);

    console.log(buf.readDoubleLE(0));
    // Prints: 5.447603722011605e-270
    console.log(buf.readDoubleLE(1));
    // Throws ERR_OUT_OF_RANGE.
    ```

    @param offset

    Number of bytes to skip before starting to read. Must satisfy `0 <= offset <= buf.length - 8`.
  + [readFloatBE](https://bun.com/reference/node/buffer/Buffer/readFloatBE)(

    offset?: number

    ): number;

    Reads a 32-bit, big-endian float from `buf` at the specified `offset`.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from([1, 2, 3, 4]);

    console.log(buf.readFloatBE(0));
    // Prints: 2.387939260590663e-38
    ```

    @param offset

    Number of bytes to skip before starting to read. Must satisfy `0 <= offset <= buf.length - 4`.
  + [readFloatLE](https://bun.com/reference/node/buffer/Buffer/readFloatLE)(

    offset?: number

    ): number;

    Reads a 32-bit, little-endian float from `buf` at the specified `offset`.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from([1, 2, 3, 4]);

    console.log(buf.readFloatLE(0));
    // Prints: 1.539989614439558e-36
    console.log(buf.readFloatLE(1));
    // Throws ERR_OUT_OF_RANGE.
    ```

    @param offset

    Number of bytes to skip before starting to read. Must satisfy `0 <= offset <= buf.length - 4`.
  + [readInt16BE](https://bun.com/reference/node/buffer/Buffer/readInt16BE)(

    offset?: number

    ): number;

    Reads a signed, big-endian 16-bit integer from `buf` at the specified `offset`.

    Integers read from a `Buffer` are interpreted as two's complement signed values.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from([0, 5]);

    console.log(buf.readInt16BE(0));
    // Prints: 5
    ```

    @param offset

    Number of bytes to skip before starting to read. Must satisfy `0 <= offset <= buf.length - 2`.
  + [readInt16LE](https://bun.com/reference/node/buffer/Buffer/readInt16LE)(

    offset?: number

    ): number;

    Reads a signed, little-endian 16-bit integer from `buf` at the specified`offset`.

    Integers read from a `Buffer` are interpreted as two's complement signed values.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from([0, 5]);

    console.log(buf.readInt16LE(0));
    // Prints: 1280
    console.log(buf.readInt16LE(1));
    // Throws ERR_OUT_OF_RANGE.
    ```

    @param offset

    Number of bytes to skip before starting to read. Must satisfy `0 <= offset <= buf.length - 2`.
  + [readInt32BE](https://bun.com/reference/node/buffer/Buffer/readInt32BE)(

    offset?: number

    ): number;

    Reads a signed, big-endian 32-bit integer from `buf` at the specified `offset`.

    Integers read from a `Buffer` are interpreted as two's complement signed values.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from([0, 0, 0, 5]);

    console.log(buf.readInt32BE(0));
    // Prints: 5
    ```

    @param offset

    Number of bytes to skip before starting to read. Must satisfy `0 <= offset <= buf.length - 4`.
  + [readInt32LE](https://bun.com/reference/node/buffer/Buffer/readInt32LE)(

    offset?: number

    ): number;

    Reads a signed, little-endian 32-bit integer from `buf` at the specified`offset`.

    Integers read from a `Buffer` are interpreted as two's complement signed values.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from([0, 0, 0, 5]);

    console.log(buf.readInt32LE(0));
    // Prints: 83886080
    console.log(buf.readInt32LE(1));
    // Throws ERR_OUT_OF_RANGE.
    ```

    @param offset

    Number of bytes to skip before starting to read. Must satisfy `0 <= offset <= buf.length - 4`.
  + [readInt8](https://bun.com/reference/node/buffer/Buffer/readInt8)(

    offset?: number

    ): number;

    Reads a signed 8-bit integer from `buf` at the specified `offset`.

    Integers read from a `Buffer` are interpreted as two's complement signed values.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from([-1, 5]);

    console.log(buf.readInt8(0));
    // Prints: -1
    console.log(buf.readInt8(1));
    // Prints: 5
    console.log(buf.readInt8(2));
    // Throws ERR_OUT_OF_RANGE.
    ```

    @param offset

    Number of bytes to skip before starting to read. Must satisfy `0 <= offset <= buf.length - 1`.
  + [readIntBE](https://bun.com/reference/node/buffer/Buffer/readIntBE)(

    offset: number,

    byteLength: number

    ): number;

    Reads `byteLength` number of bytes from `buf` at the specified `offset` and interprets the result as a big-endian, two's complement signed value supporting up to 48 bits of accuracy.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from([0x12, 0x34, 0x56, 0x78, 0x90, 0xab]);

    console.log(buf.readIntBE(0, 6).toString(16));
    // Prints: 1234567890ab
    console.log(buf.readIntBE(1, 6).toString(16));
    // Throws ERR_OUT_OF_RANGE.
    console.log(buf.readIntBE(1, 0).toString(16));
    // Throws ERR_OUT_OF_RANGE.
    ```

    @param offset

    Number of bytes to skip before starting to read. Must satisfy `0 <= offset <= buf.length - byteLength`.

    @param byteLength

    Number of bytes to read. Must satisfy `0 < byteLength <= 6`.
  + [readIntLE](https://bun.com/reference/node/buffer/Buffer/readIntLE)(

    offset: number,

    byteLength: number

    ): number;

    Reads `byteLength` number of bytes from `buf` at the specified `offset` and interprets the result as a little-endian, two's complement signed value supporting up to 48 bits of accuracy.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from([0x12, 0x34, 0x56, 0x78, 0x90, 0xab]);

    console.log(buf.readIntLE(0, 6).toString(16));
    // Prints: -546f87a9cbee
    ```

    @param offset

    Number of bytes to skip before starting to read. Must satisfy `0 <= offset <= buf.length - byteLength`.

    @param byteLength

    Number of bytes to read. Must satisfy `0 < byteLength <= 6`.
  + [readUint16BE](https://bun.com/reference/node/buffer/Buffer/readUint16BE)(

    offset?: number

    ): number;
  + [readUInt16BE](https://bun.com/reference/node/buffer/Buffer/readUInt16BE)(

    offset?: number

    ): number;

    Reads an unsigned, big-endian 16-bit integer from `buf` at the specified`offset`.

    This function is also available under the `readUint16BE` alias.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from([0x12, 0x34, 0x56]);

    console.log(buf.readUInt16BE(0).toString(16));
    // Prints: 1234
    console.log(buf.readUInt16BE(1).toString(16));
    // Prints: 3456
    ```

    @param offset

    Number of bytes to skip before starting to read. Must satisfy `0 <= offset <= buf.length - 2`.
  + [readUint16LE](https://bun.com/reference/node/buffer/Buffer/readUint16LE)(

    offset?: number

    ): number;
  + [readUInt16LE](https://bun.com/reference/node/buffer/Buffer/readUInt16LE)(

    offset?: number

    ): number;

    Reads an unsigned, little-endian 16-bit integer from `buf` at the specified `offset`.

    This function is also available under the `readUint16LE` alias.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from([0x12, 0x34, 0x56]);

    console.log(buf.readUInt16LE(0).toString(16));
    // Prints: 3412
    console.log(buf.readUInt16LE(1).toString(16));
    // Prints: 5634
    console.log(buf.readUInt16LE(2).toString(16));
    // Throws ERR_OUT_OF_RANGE.
    ```

    @param offset

    Number of bytes to skip before starting to read. Must satisfy `0 <= offset <= buf.length - 2`.
  + [readUint32BE](https://bun.com/reference/node/buffer/Buffer/readUint32BE)(

    offset?: number

    ): number;
  + [readUInt32BE](https://bun.com/reference/node/buffer/Buffer/readUInt32BE)(

    offset?: number

    ): number;

    Reads an unsigned, big-endian 32-bit integer from `buf` at the specified`offset`.

    This function is also available under the `readUint32BE` alias.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from([0x12, 0x34, 0x56, 0x78]);

    console.log(buf.readUInt32BE(0).toString(16));
    // Prints: 12345678
    ```

    @param offset

    Number of bytes to skip before starting to read. Must satisfy `0 <= offset <= buf.length - 4`.
  + [readUint32LE](https://bun.com/reference/node/buffer/Buffer/readUint32LE)(

    offset?: number

    ): number;
  + [readUInt32LE](https://bun.com/reference/node/buffer/Buffer/readUInt32LE)(

    offset?: number

    ): number;

    Reads an unsigned, little-endian 32-bit integer from `buf` at the specified`offset`.

    This function is also available under the `readUint32LE` alias.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from([0x12, 0x34, 0x56, 0x78]);

    console.log(buf.readUInt32LE(0).toString(16));
    // Prints: 78563412
    console.log(buf.readUInt32LE(1).toString(16));
    // Throws ERR_OUT_OF_RANGE.
    ```

    @param offset

    Number of bytes to skip before starting to read. Must satisfy `0 <= offset <= buf.length - 4`.
  + [readUint8](https://bun.com/reference/node/buffer/Buffer/readUint8)(

    offset?: number

    ): number;
  + [readUInt8](https://bun.com/reference/node/buffer/Buffer/readUInt8)(

    offset?: number

    ): number;

    Reads an unsigned 8-bit integer from `buf` at the specified `offset`.

    This function is also available under the `readUint8` alias.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from([1, -2]);

    console.log(buf.readUInt8(0));
    // Prints: 1
    console.log(buf.readUInt8(1));
    // Prints: 254
    console.log(buf.readUInt8(2));
    // Throws ERR_OUT_OF_RANGE.
    ```

    @param offset

    Number of bytes to skip before starting to read. Must satisfy `0 <= offset <= buf.length - 1`.
  + [readUintBE](https://bun.com/reference/node/buffer/Buffer/readUintBE)(

    offset: number,

    byteLength: number

    ): number;
  + [readUIntBE](https://bun.com/reference/node/buffer/Buffer/readUIntBE)(

    offset: number,

    byteLength: number

    ): number;

    Reads `byteLength` number of bytes from `buf` at the specified `offset` and interprets the result as an unsigned big-endian integer supporting up to 48 bits of accuracy.

    This function is also available under the `readUintBE` alias.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from([0x12, 0x34, 0x56, 0x78, 0x90, 0xab]);

    console.log(buf.readUIntBE(0, 6).toString(16));
    // Prints: 1234567890ab
    console.log(buf.readUIntBE(1, 6).toString(16));
    // Throws ERR_OUT_OF_RANGE.
    ```

    @param offset

    Number of bytes to skip before starting to read. Must satisfy `0 <= offset <= buf.length - byteLength`.

    @param byteLength

    Number of bytes to read. Must satisfy `0 < byteLength <= 6`.
  + [readUintLE](https://bun.com/reference/node/buffer/Buffer/readUintLE)(

    offset: number,

    byteLength: number

    ): number;
  + [readUIntLE](https://bun.com/reference/node/buffer/Buffer/readUIntLE)(

    offset: number,

    byteLength: number

    ): number;

    Reads `byteLength` number of bytes from `buf` at the specified `offset` and interprets the result as an unsigned, little-endian integer supporting up to 48 bits of accuracy.

    This function is also available under the `readUintLE` alias.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from([0x12, 0x34, 0x56, 0x78, 0x90, 0xab]);

    console.log(buf.readUIntLE(0, 6).toString(16));
    // Prints: ab9078563412
    ```

    @param offset

    Number of bytes to skip before starting to read. Must satisfy `0 <= offset <= buf.length - byteLength`.

    @param byteLength

    Number of bytes to read. Must satisfy `0 < byteLength <= 6`.
  + [reduce](https://bun.com/reference/node/buffer/Buffer/reduce)(

    callbackfn: (previousValue: number, currentValue: number, currentIndex: number, array: this) => number

    ): number;

    Calls the specified callback function for all the elements in an array. The return value of the callback function is the accumulated result, and is provided as an argument in the next call to the callback function.

    @param callbackfn

    A function that accepts up to four arguments. The reduce method calls the callbackfn function one time for each element in the array.

    [reduce](https://bun.com/reference/node/buffer/Buffer/reduce)(

    callbackfn: (previousValue: number, currentValue: number, currentIndex: number, array: this) => number,

    initialValue: number

    ): number;

    [reduce](https://bun.com/reference/node/buffer/Buffer/reduce)<U>(

    callbackfn: (previousValue: U, currentValue: number, currentIndex: number, array: this) => U,

    initialValue: U

    ): U;

    Calls the specified callback function for all the elements in an array. The return value of the callback function is the accumulated result, and is provided as an argument in the next call to the callback function.

    @param callbackfn

    A function that accepts up to four arguments. The reduce method calls the callbackfn function one time for each element in the array.

    @param initialValue

    If initialValue is specified, it is used as the initial value to start the accumulation. The first call to the callbackfn function provides this value as an argument instead of an array value.
  + [reduceRight](https://bun.com/reference/node/buffer/Buffer/reduceRight)(

    callbackfn: (previousValue: number, currentValue: number, currentIndex: number, array: this) => number

    ): number;

    Calls the specified callback function for all the elements in an array, in descending order. The return value of the callback function is the accumulated result, and is provided as an argument in the next call to the callback function.

    @param callbackfn

    A function that accepts up to four arguments. The reduceRight method calls the callbackfn function one time for each element in the array.

    [reduceRight](https://bun.com/reference/node/buffer/Buffer/reduceRight)(

    callbackfn: (previousValue: number, currentValue: number, currentIndex: number, array: this) => number,

    initialValue: number

    ): number;

    [reduceRight](https://bun.com/reference/node/buffer/Buffer/reduceRight)<U>(

    callbackfn: (previousValue: U, currentValue: number, currentIndex: number, array: this) => U,

    initialValue: U

    ): U;

    Calls the specified callback function for all the elements in an array, in descending order. The return value of the callback function is the accumulated result, and is provided as an argument in the next call to the callback function.

    @param callbackfn

    A function that accepts up to four arguments. The reduceRight method calls the callbackfn function one time for each element in the array.

    @param initialValue

    If initialValue is specified, it is used as the initial value to start the accumulation. The first call to the callbackfn function provides this value as an argument instead of an array value.
  + [reverse](https://bun.com/reference/node/buffer/Buffer/reverse)(): this;

    Reverses the elements in an Array.
  + [set](https://bun.com/reference/node/buffer/Buffer/set)(

    array: ArrayLike<number>,

    offset?: number

    ): void;

    Sets a value or an array of values.

    @param array

    A typed or untyped array of values to set.

    @param offset

    The index in the current array at which the values are to be written.
  + [setFromBase64](https://bun.com/reference/node/buffer/Buffer/setFromBase64)(

    base64: string,

    offset?: number

    ): { read: number; written: number };

    Set the contents of the Uint8Array from a base64 encoded string

    @param base64

    The base64 encoded string to decode into the array

    @param offset

    Optional starting index to begin setting the decoded bytes (default: 0)
  + [setFromHex](https://bun.com/reference/node/buffer/Buffer/setFromHex)(

    hex: string

    ): { read: number; written: number };

    Set the contents of the Uint8Array from a hex encoded string

    @param hex

    The hex encoded string to decode into the array. The string must have an even number of characters, be valid hexadecimal characters and contain no whitespace.
  + [some](https://bun.com/reference/node/buffer/Buffer/some)(

    predicate: (value: number, index: number, array: this) => unknown,

    thisArg?: any

    ): boolean;

    Determines whether the specified callback function returns true for any element of an array.

    @param predicate

    A function that accepts up to three arguments. The some method calls the predicate function for each element in the array until the predicate returns a value which is coercible to the Boolean value true, or until the end of the array.

    @param thisArg

    An object to which the this keyword can refer in the predicate function. If thisArg is omitted, undefined is used as the this value.
  + [sort](https://bun.com/reference/node/buffer/Buffer/sort)(

    compareFn?: (a: number, b: number) => number

    ): this;

    Sorts an array.

    @param compareFn

    Function used to determine the order of the elements. It is expected to return a negative value if first argument is less than second argument, zero if they're equal and a positive value otherwise. If omitted, the elements are sorted in ascending order.

    ```
    [11,2,22,1].sort((a, b) => a - b)
    ```
  + [subarray](https://bun.com/reference/node/buffer/Buffer/subarray)(

    start?: number,

    end?: number

    ): [Buffer](https://bun.com/reference/node/buffer/Buffer)<TArrayBuffer>;

    Returns a new `Buffer` that references the same memory as the original, but offset and cropped by the `start` and `end` indices.

    Specifying `end` greater than `buf.length` will return the same result as that of `end` equal to `buf.length`.

    This method is inherited from [`TypedArray.prototype.subarray()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray/subarray).

    Modifying the new `Buffer` slice will modify the memory in the original `Buffer`because the allocated memory of the two objects overlap.

    ```
    import { Buffer } from 'node:buffer';

    // Create a `Buffer` with the ASCII alphabet, take a slice, and modify one byte
    // from the original `Buffer`.

    const buf1 = Buffer.allocUnsafe(26);

    for (let i = 0; i < 26; i++) {
      // 97 is the decimal ASCII value for 'a'.
      buf1[i] = i + 97;
    }

    const buf2 = buf1.subarray(0, 3);

    console.log(buf2.toString('ascii', 0, buf2.length));
    // Prints: abc

    buf1[0] = 33;

    console.log(buf2.toString('ascii', 0, buf2.length));
    // Prints: !bc
    ```

    Specifying negative indexes causes the slice to be generated relative to the end of `buf` rather than the beginning.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from('buffer');

    console.log(buf.subarray(-6, -1).toString());
    // Prints: buffe
    // (Equivalent to buf.subarray(0, 5).)

    console.log(buf.subarray(-6, -2).toString());
    // Prints: buff
    // (Equivalent to buf.subarray(0, 4).)

    console.log(buf.subarray(-5, -2).toString());
    // Prints: uff
    // (Equivalent to buf.subarray(1, 4).)
    ```

    @param start

    Where the new `Buffer` will start.

    @param end

    Where the new `Buffer` will end (not inclusive).
  + [swap16](https://bun.com/reference/node/buffer/Buffer/swap16)(): this;

    Interprets `buf` as an array of unsigned 16-bit integers and swaps the byte order *in-place*. Throws `ERR_INVALID_BUFFER_SIZE` if `buf.length` is not a multiple of 2.

    ```
    import { Buffer } from 'node:buffer';

    const buf1 = Buffer.from([0x1, 0x2, 0x3, 0x4, 0x5, 0x6, 0x7, 0x8]);

    console.log(buf1);
    // Prints: <Buffer 01 02 03 04 05 06 07 08>

    buf1.swap16();

    console.log(buf1);
    // Prints: <Buffer 02 01 04 03 06 05 08 07>

    const buf2 = Buffer.from([0x1, 0x2, 0x3]);

    buf2.swap16();
    // Throws ERR_INVALID_BUFFER_SIZE.
    ```

    One convenient use of `buf.swap16()` is to perform a fast in-place conversion between UTF-16 little-endian and UTF-16 big-endian:

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from('This is little-endian UTF-16', 'utf16le');
    buf.swap16(); // Convert to big-endian UTF-16 text.
    ```

    @returns

    A reference to `buf`.
  + [swap32](https://bun.com/reference/node/buffer/Buffer/swap32)(): this;

    Interprets `buf` as an array of unsigned 32-bit integers and swaps the byte order *in-place*. Throws `ERR_INVALID_BUFFER_SIZE` if `buf.length` is not a multiple of 4.

    ```
    import { Buffer } from 'node:buffer';

    const buf1 = Buffer.from([0x1, 0x2, 0x3, 0x4, 0x5, 0x6, 0x7, 0x8]);

    console.log(buf1);
    // Prints: <Buffer 01 02 03 04 05 06 07 08>

    buf1.swap32();

    console.log(buf1);
    // Prints: <Buffer 04 03 02 01 08 07 06 05>

    const buf2 = Buffer.from([0x1, 0x2, 0x3]);

    buf2.swap32();
    // Throws ERR_INVALID_BUFFER_SIZE.
    ```

    @returns

    A reference to `buf`.
  + [swap64](https://bun.com/reference/node/buffer/Buffer/swap64)(): this;

    Interprets `buf` as an array of 64-bit numbers and swaps byte order *in-place*. Throws `ERR_INVALID_BUFFER_SIZE` if `buf.length` is not a multiple of 8.

    ```
    import { Buffer } from 'node:buffer';

    const buf1 = Buffer.from([0x1, 0x2, 0x3, 0x4, 0x5, 0x6, 0x7, 0x8]);

    console.log(buf1);
    // Prints: <Buffer 01 02 03 04 05 06 07 08>

    buf1.swap64();

    console.log(buf1);
    // Prints: <Buffer 08 07 06 05 04 03 02 01>

    const buf2 = Buffer.from([0x1, 0x2, 0x3]);

    buf2.swap64();
    // Throws ERR_INVALID_BUFFER_SIZE.
    ```

    @returns

    A reference to `buf`.
  + [toBase64](https://bun.com/reference/node/buffer/Buffer/toBase64)(

    options?: { alphabet: 'base64' | 'base64url'; omitPadding: boolean }

    ): string;

    Convert the Uint8Array to a base64 encoded string

    @returns

    The base64 encoded string representation of the Uint8Array
  + [toHex](https://bun.com/reference/node/buffer/Buffer/toHex)(): string;

    Convert the Uint8Array to a hex encoded string

    @returns

    The hex encoded string representation of the Uint8Array
  + [toJSON](https://bun.com/reference/node/buffer/Buffer/toJSON)(): { data: number[]; type: 'Buffer' };

    Returns a JSON representation of `buf`. [`JSON.stringify()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify) implicitly calls this function when stringifying a `Buffer` instance.

    `Buffer.from()` accepts objects in the format returned from this method. In particular, `Buffer.from(buf.toJSON())` works like `Buffer.from(buf)`.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.from([0x1, 0x2, 0x3, 0x4, 0x5]);
    const json = JSON.stringify(buf);

    console.log(json);
    // Prints: {"type":"Buffer","data":[1,2,3,4,5]}

    const copy = JSON.parse(json, (key, value) => {
      return value &#x26;&#x26; value.type === 'Buffer' ?
        Buffer.from(value) :
        value;
    });

    console.log(copy);
    // Prints: <Buffer 01 02 03 04 05>
    ```
  + [toLocaleString](https://bun.com/reference/node/buffer/Buffer/toLocaleString)(): string;

    Converts a number to a string by using the current locale.

    [toLocaleString](https://bun.com/reference/node/buffer/Buffer/toLocaleString)(

    locales: string | string[],

    options?: NumberFormatOptions

    ): string;
  + [toReversed](https://bun.com/reference/node/buffer/Buffer/toReversed)(): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Copies the array and returns the copy with the elements in reverse order.
  + [toSorted](https://bun.com/reference/node/buffer/Buffer/toSorted)(

    compareFn?: (a: number, b: number) => number

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Copies and sorts the array.

    @param compareFn

    Function used to determine the order of the elements. It is expected to return a negative value if the first argument is less than the second argument, zero if they're equal, and a positive value otherwise. If omitted, the elements are sorted in ascending order.

    ```
    const myNums = Uint8Array.from([11, 2, 22, 1]);
    myNums.toSorted((a, b) => a - b) // Uint8Array(4) [1, 2, 11, 22]
    ```
  + [toString](https://bun.com/reference/node/buffer/Buffer/toString)(

    encoding?: BufferEncoding,

    start?: number,

    end?: number

    ): string;

    Decodes `buf` to a string according to the specified character encoding in`encoding`. `start` and `end` may be passed to decode only a subset of `buf`.

    If `encoding` is `'utf8'` and a byte sequence in the input is not valid UTF-8, then each invalid byte is replaced with the replacement character `U+FFFD`.

    The maximum length of a string instance (in UTF-16 code units) is available as constants.MAX\_STRING\_LENGTH.

    ```
    import { Buffer } from 'node:buffer';

    const buf1 = Buffer.allocUnsafe(26);

    for (let i = 0; i < 26; i++) {
      // 97 is the decimal ASCII value for 'a'.
      buf1[i] = i + 97;
    }

    console.log(buf1.toString('utf8'));
    // Prints: abcdefghijklmnopqrstuvwxyz
    console.log(buf1.toString('utf8', 0, 5));
    // Prints: abcde

    const buf2 = Buffer.from('tést');

    console.log(buf2.toString('hex'));
    // Prints: 74c3a97374
    console.log(buf2.toString('utf8', 0, 3));
    // Prints: té
    console.log(buf2.toString(undefined, 0, 3));
    // Prints: té
    ```

    @param encoding

    The character encoding to use.

    @param start

    The byte offset to start decoding at.

    @param end

    The byte offset to stop decoding at (not inclusive).
  + [valueOf](https://bun.com/reference/node/buffer/Buffer/valueOf)(): this;

    Returns the primitive value of the specified object.
  + [values](https://bun.com/reference/node/buffer/Buffer/values)(): ArrayIterator<number>;

    Returns an list of values in the array
  + [with](https://bun.com/reference/node/buffer/Buffer/with)(

    index: number,

    value: number

    ): [Uint8Array](https://bun.com/reference/globals/Uint8Array)<[ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer)>;

    Copies the array and inserts the given number at the provided index.

    @param index

    The index of the value to overwrite. If the index is negative, then it replaces from the end of the array.

    @param value

    The value to insert into the copied array.

    @returns

    A copy of the original array with the inserted value.
  + [write](https://bun.com/reference/node/buffer/Buffer/write)(

    string: string,

    encoding?: BufferEncoding

    ): number;

    Writes `string` to `buf` at `offset` according to the character encoding in`encoding`. The `length` parameter is the number of bytes to write. If `buf` did not contain enough space to fit the entire string, only part of `string` will be written. However, partially encoded characters will not be written.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.alloc(256);

    const len = buf.write('\u00bd + \u00bc = \u00be', 0);

    console.log(`${len} bytes: ${buf.toString('utf8', 0, len)}`);
    // Prints: 12 bytes: ½ + ¼ = ¾

    const buffer = Buffer.alloc(10);

    const length = buffer.write('abcd', 8);

    console.log(`${length} bytes: ${buffer.toString('utf8', 8, 10)}`);
    // Prints: 2 bytes : ab
    ```

    @param string

    String to write to `buf`.

    @param encoding

    The character encoding of `string`.

    @returns

    Number of bytes written.

    [write](https://bun.com/reference/node/buffer/Buffer/write)(

    string: string,

    offset: number,

    encoding?: BufferEncoding

    ): number;

    [write](https://bun.com/reference/node/buffer/Buffer/write)(

    string: string,

    offset: number,

    length: number,

    encoding?: BufferEncoding

    ): number;
  + [writeBigInt64BE](https://bun.com/reference/node/buffer/Buffer/writeBigInt64BE)(

    value: bigint,

    offset?: number

    ): number;

    Writes `value` to `buf` at the specified `offset` as big-endian.

    `value` is interpreted and written as a two's complement signed integer.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(8);

    buf.writeBigInt64BE(0x0102030405060708n, 0);

    console.log(buf);
    // Prints: <Buffer 01 02 03 04 05 06 07 08>
    ```

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy: `0 <= offset <= buf.length - 8`.

    @returns

    `offset` plus the number of bytes written.
  + [writeBigInt64LE](https://bun.com/reference/node/buffer/Buffer/writeBigInt64LE)(

    value: bigint,

    offset?: number

    ): number;

    Writes `value` to `buf` at the specified `offset` as little-endian.

    `value` is interpreted and written as a two's complement signed integer.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(8);

    buf.writeBigInt64LE(0x0102030405060708n, 0);

    console.log(buf);
    // Prints: <Buffer 08 07 06 05 04 03 02 01>
    ```

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy: `0 <= offset <= buf.length - 8`.

    @returns

    `offset` plus the number of bytes written.
  + [writeBigUint64BE](https://bun.com/reference/node/buffer/Buffer/writeBigUint64BE)(

    value: bigint,

    offset?: number

    ): number;
  + [writeBigUInt64BE](https://bun.com/reference/node/buffer/Buffer/writeBigUInt64BE)(

    value: bigint,

    offset?: number

    ): number;

    Writes `value` to `buf` at the specified `offset` as big-endian.

    This function is also available under the `writeBigUint64BE` alias.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(8);

    buf.writeBigUInt64BE(0xdecafafecacefaden, 0);

    console.log(buf);
    // Prints: <Buffer de ca fa fe ca ce fa de>
    ```

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy: `0 <= offset <= buf.length - 8`.

    @returns

    `offset` plus the number of bytes written.
  + [writeBigUint64LE](https://bun.com/reference/node/buffer/Buffer/writeBigUint64LE)(

    value: bigint,

    offset?: number

    ): number;
  + [writeBigUInt64LE](https://bun.com/reference/node/buffer/Buffer/writeBigUInt64LE)(

    value: bigint,

    offset?: number

    ): number;

    Writes `value` to `buf` at the specified `offset` as little-endian

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(8);

    buf.writeBigUInt64LE(0xdecafafecacefaden, 0);

    console.log(buf);
    // Prints: <Buffer de fa ce ca fe fa ca de>
    ```

    This function is also available under the `writeBigUint64LE` alias.

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy: `0 <= offset <= buf.length - 8`.

    @returns

    `offset` plus the number of bytes written.
  + [writeDoubleBE](https://bun.com/reference/node/buffer/Buffer/writeDoubleBE)(

    value: number,

    offset?: number

    ): number;

    Writes `value` to `buf` at the specified `offset` as big-endian. The `value` must be a JavaScript number. Behavior is undefined when `value` is anything other than a JavaScript number.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(8);

    buf.writeDoubleBE(123.456, 0);

    console.log(buf);
    // Prints: <Buffer 40 5e dd 2f 1a 9f be 77>
    ```

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy `0 <= offset <= buf.length - 8`.

    @returns

    `offset` plus the number of bytes written.
  + [writeDoubleLE](https://bun.com/reference/node/buffer/Buffer/writeDoubleLE)(

    value: number,

    offset?: number

    ): number;

    Writes `value` to `buf` at the specified `offset` as little-endian. The `value` must be a JavaScript number. Behavior is undefined when `value` is anything other than a JavaScript number.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(8);

    buf.writeDoubleLE(123.456, 0);

    console.log(buf);
    // Prints: <Buffer 77 be 9f 1a 2f dd 5e 40>
    ```

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy `0 <= offset <= buf.length - 8`.

    @returns

    `offset` plus the number of bytes written.
  + [writeFloatBE](https://bun.com/reference/node/buffer/Buffer/writeFloatBE)(

    value: number,

    offset?: number

    ): number;

    Writes `value` to `buf` at the specified `offset` as big-endian. Behavior is undefined when `value` is anything other than a JavaScript number.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(4);

    buf.writeFloatBE(0xcafebabe, 0);

    console.log(buf);
    // Prints: <Buffer 4f 4a fe bb>
    ```

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy `0 <= offset <= buf.length - 4`.

    @returns

    `offset` plus the number of bytes written.
  + [writeFloatLE](https://bun.com/reference/node/buffer/Buffer/writeFloatLE)(

    value: number,

    offset?: number

    ): number;

    Writes `value` to `buf` at the specified `offset` as little-endian. Behavior is undefined when `value` is anything other than a JavaScript number.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(4);

    buf.writeFloatLE(0xcafebabe, 0);

    console.log(buf);
    // Prints: <Buffer bb fe 4a 4f>
    ```

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy `0 <= offset <= buf.length - 4`.

    @returns

    `offset` plus the number of bytes written.
  + [writeInt16BE](https://bun.com/reference/node/buffer/Buffer/writeInt16BE)(

    value: number,

    offset?: number

    ): number;

    Writes `value` to `buf` at the specified `offset` as big-endian. The `value` must be a valid signed 16-bit integer. Behavior is undefined when `value` is anything other than a signed 16-bit integer.

    The `value` is interpreted and written as a two's complement signed integer.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(2);

    buf.writeInt16BE(0x0102, 0);

    console.log(buf);
    // Prints: <Buffer 01 02>
    ```

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy `0 <= offset <= buf.length - 2`.

    @returns

    `offset` plus the number of bytes written.
  + [writeInt16LE](https://bun.com/reference/node/buffer/Buffer/writeInt16LE)(

    value: number,

    offset?: number

    ): number;

    Writes `value` to `buf` at the specified `offset` as little-endian. The `value` must be a valid signed 16-bit integer. Behavior is undefined when `value` is anything other than a signed 16-bit integer.

    The `value` is interpreted and written as a two's complement signed integer.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(2);

    buf.writeInt16LE(0x0304, 0);

    console.log(buf);
    // Prints: <Buffer 04 03>
    ```

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy `0 <= offset <= buf.length - 2`.

    @returns

    `offset` plus the number of bytes written.
  + [writeInt32BE](https://bun.com/reference/node/buffer/Buffer/writeInt32BE)(

    value: number,

    offset?: number

    ): number;

    Writes `value` to `buf` at the specified `offset` as big-endian. The `value` must be a valid signed 32-bit integer. Behavior is undefined when `value` is anything other than a signed 32-bit integer.

    The `value` is interpreted and written as a two's complement signed integer.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(4);

    buf.writeInt32BE(0x01020304, 0);

    console.log(buf);
    // Prints: <Buffer 01 02 03 04>
    ```

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy `0 <= offset <= buf.length - 4`.

    @returns

    `offset` plus the number of bytes written.
  + [writeInt32LE](https://bun.com/reference/node/buffer/Buffer/writeInt32LE)(

    value: number,

    offset?: number

    ): number;

    Writes `value` to `buf` at the specified `offset` as little-endian. The `value` must be a valid signed 32-bit integer. Behavior is undefined when `value` is anything other than a signed 32-bit integer.

    The `value` is interpreted and written as a two's complement signed integer.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(4);

    buf.writeInt32LE(0x05060708, 0);

    console.log(buf);
    // Prints: <Buffer 08 07 06 05>
    ```

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy `0 <= offset <= buf.length - 4`.

    @returns

    `offset` plus the number of bytes written.
  + [writeInt8](https://bun.com/reference/node/buffer/Buffer/writeInt8)(

    value: number,

    offset?: number

    ): number;

    Writes `value` to `buf` at the specified `offset`. `value` must be a valid signed 8-bit integer. Behavior is undefined when `value` is anything other than a signed 8-bit integer.

    `value` is interpreted and written as a two's complement signed integer.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(2);

    buf.writeInt8(2, 0);
    buf.writeInt8(-2, 1);

    console.log(buf);
    // Prints: <Buffer 02 fe>
    ```

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy `0 <= offset <= buf.length - 1`.

    @returns

    `offset` plus the number of bytes written.
  + [writeIntBE](https://bun.com/reference/node/buffer/Buffer/writeIntBE)(

    value: number,

    offset: number,

    byteLength: number

    ): number;

    Writes `byteLength` bytes of `value` to `buf` at the specified `offset`as big-endian. Supports up to 48 bits of accuracy. Behavior is undefined when`value` is anything other than a signed integer.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(6);

    buf.writeIntBE(0x1234567890ab, 0, 6);

    console.log(buf);
    // Prints: <Buffer 12 34 56 78 90 ab>
    ```

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy `0 <= offset <= buf.length - byteLength`.

    @param byteLength

    Number of bytes to write. Must satisfy `0 < byteLength <= 6`.

    @returns

    `offset` plus the number of bytes written.
  + [writeIntLE](https://bun.com/reference/node/buffer/Buffer/writeIntLE)(

    value: number,

    offset: number,

    byteLength: number

    ): number;

    Writes `byteLength` bytes of `value` to `buf` at the specified `offset`as little-endian. Supports up to 48 bits of accuracy. Behavior is undefined when `value` is anything other than a signed integer.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(6);

    buf.writeIntLE(0x1234567890ab, 0, 6);

    console.log(buf);
    // Prints: <Buffer ab 90 78 56 34 12>
    ```

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy `0 <= offset <= buf.length - byteLength`.

    @param byteLength

    Number of bytes to write. Must satisfy `0 < byteLength <= 6`.

    @returns

    `offset` plus the number of bytes written.
  + [writeUint16BE](https://bun.com/reference/node/buffer/Buffer/writeUint16BE)(

    value: number,

    offset?: number

    ): number;
  + [writeUInt16BE](https://bun.com/reference/node/buffer/Buffer/writeUInt16BE)(

    value: number,

    offset?: number

    ): number;

    Writes `value` to `buf` at the specified `offset` as big-endian. The `value` must be a valid unsigned 16-bit integer. Behavior is undefined when `value`is anything other than an unsigned 16-bit integer.

    This function is also available under the `writeUint16BE` alias.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(4);

    buf.writeUInt16BE(0xdead, 0);
    buf.writeUInt16BE(0xbeef, 2);

    console.log(buf);
    // Prints: <Buffer de ad be ef>
    ```

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy `0 <= offset <= buf.length - 2`.

    @returns

    `offset` plus the number of bytes written.
  + [writeUint16LE](https://bun.com/reference/node/buffer/Buffer/writeUint16LE)(

    value: number,

    offset?: number

    ): number;
  + [writeUInt16LE](https://bun.com/reference/node/buffer/Buffer/writeUInt16LE)(

    value: number,

    offset?: number

    ): number;

    Writes `value` to `buf` at the specified `offset` as little-endian. The `value` must be a valid unsigned 16-bit integer. Behavior is undefined when `value` is anything other than an unsigned 16-bit integer.

    This function is also available under the `writeUint16LE` alias.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(4);

    buf.writeUInt16LE(0xdead, 0);
    buf.writeUInt16LE(0xbeef, 2);

    console.log(buf);
    // Prints: <Buffer ad de ef be>
    ```

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy `0 <= offset <= buf.length - 2`.

    @returns

    `offset` plus the number of bytes written.
  + [writeUint32BE](https://bun.com/reference/node/buffer/Buffer/writeUint32BE)(

    value: number,

    offset?: number

    ): number;
  + [writeUInt32BE](https://bun.com/reference/node/buffer/Buffer/writeUInt32BE)(

    value: number,

    offset?: number

    ): number;

    Writes `value` to `buf` at the specified `offset` as big-endian. The `value` must be a valid unsigned 32-bit integer. Behavior is undefined when `value`is anything other than an unsigned 32-bit integer.

    This function is also available under the `writeUint32BE` alias.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(4);

    buf.writeUInt32BE(0xfeedface, 0);

    console.log(buf);
    // Prints: <Buffer fe ed fa ce>
    ```

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy `0 <= offset <= buf.length - 4`.

    @returns

    `offset` plus the number of bytes written.
  + [writeUint32LE](https://bun.com/reference/node/buffer/Buffer/writeUint32LE)(

    value: number,

    offset?: number

    ): number;
  + [writeUInt32LE](https://bun.com/reference/node/buffer/Buffer/writeUInt32LE)(

    value: number,

    offset?: number

    ): number;

    Writes `value` to `buf` at the specified `offset` as little-endian. The `value` must be a valid unsigned 32-bit integer. Behavior is undefined when `value` is anything other than an unsigned 32-bit integer.

    This function is also available under the `writeUint32LE` alias.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(4);

    buf.writeUInt32LE(0xfeedface, 0);

    console.log(buf);
    // Prints: <Buffer ce fa ed fe>
    ```

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy `0 <= offset <= buf.length - 4`.

    @returns

    `offset` plus the number of bytes written.
  + [writeUint8](https://bun.com/reference/node/buffer/Buffer/writeUint8)(

    value: number,

    offset?: number

    ): number;
  + [writeUInt8](https://bun.com/reference/node/buffer/Buffer/writeUInt8)(

    value: number,

    offset?: number

    ): number;

    Writes `value` to `buf` at the specified `offset`. `value` must be a valid unsigned 8-bit integer. Behavior is undefined when `value` is anything other than an unsigned 8-bit integer.

    This function is also available under the `writeUint8` alias.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(4);

    buf.writeUInt8(0x3, 0);
    buf.writeUInt8(0x4, 1);
    buf.writeUInt8(0x23, 2);
    buf.writeUInt8(0x42, 3);

    console.log(buf);
    // Prints: <Buffer 03 04 23 42>
    ```

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy `0 <= offset <= buf.length - 1`.

    @returns

    `offset` plus the number of bytes written.
  + [writeUintBE](https://bun.com/reference/node/buffer/Buffer/writeUintBE)(

    value: number,

    offset: number,

    byteLength: number

    ): number;
  + [writeUIntBE](https://bun.com/reference/node/buffer/Buffer/writeUIntBE)(

    value: number,

    offset: number,

    byteLength: number

    ): number;

    Writes `byteLength` bytes of `value` to `buf` at the specified `offset`as big-endian. Supports up to 48 bits of accuracy. Behavior is undefined when `value` is anything other than an unsigned integer.

    This function is also available under the `writeUintBE` alias.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(6);

    buf.writeUIntBE(0x1234567890ab, 0, 6);

    console.log(buf);
    // Prints: <Buffer 12 34 56 78 90 ab>
    ```

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy `0 <= offset <= buf.length - byteLength`.

    @param byteLength

    Number of bytes to write. Must satisfy `0 < byteLength <= 6`.

    @returns

    `offset` plus the number of bytes written.
  + [writeUintLE](https://bun.com/reference/node/buffer/Buffer/writeUintLE)(

    value: number,

    offset: number,

    byteLength: number

    ): number;
  + [writeUIntLE](https://bun.com/reference/node/buffer/Buffer/writeUIntLE)(

    value: number,

    offset: number,

    byteLength: number

    ): number;

    Writes `byteLength` bytes of `value` to `buf` at the specified `offset`as little-endian. Supports up to 48 bits of accuracy. Behavior is undefined when `value` is anything other than an unsigned integer.

    This function is also available under the `writeUintLE` alias.

    ```
    import { Buffer } from 'node:buffer';

    const buf = Buffer.allocUnsafe(6);

    buf.writeUIntLE(0x1234567890ab, 0, 6);

    console.log(buf);
    // Prints: <Buffer ab 90 78 56 34 12>
    ```

    @param value

    Number to be written to `buf`.

    @param offset

    Number of bytes to skip before starting to write. Must satisfy `0 <= offset <= buf.length - byteLength`.

    @param byteLength

    Number of bytes to write. Must satisfy `0 < byteLength <= 6`.

    @returns

    `offset` plus the number of bytes written.
* ### interface [FileOptions](https://bun.com/reference/node/buffer/FileOptions)

  + [endings](https://bun.com/reference/node/buffer/FileOptions/endings)?: 'transparent' | 'native'

    One of either `'transparent'` or `'native'`. When set to `'native'`, line endings in string source parts will be converted to the platform native line-ending as specified by `import { EOL } from 'node:os'`.
  + [lastModified](https://bun.com/reference/node/buffer/FileOptions/lastModified)?: number

    The last modified date of the file. `Default`: Date.now().
  + [type](https://bun.com/reference/node/buffer/FileOptions/type)?: string

    The File content-type.
* type [ImplicitArrayBuffer](https://bun.com/reference/node/buffer/ImplicitArrayBuffer)<T extends [WithImplicitCoercion](https://bun.com/reference/node/buffer/WithImplicitCoercion)<ArrayBufferLike>> = T extends { valueOf(): V } ? V : T
* type [TranscodeEncoding](https://bun.com/reference/node/buffer/TranscodeEncoding) = 'ascii' | 'utf8' | 'utf-8' | 'utf16le' | 'utf-16le' | 'ucs2' | 'ucs-2' | 'latin1' | 'binary'
* type [WithImplicitCoercion](https://bun.com/reference/node/buffer/WithImplicitCoercion)<T> = T | { valueOf(): T } | T extends string ? { [toPrimitive](hint: 'string'): T<T> } : never