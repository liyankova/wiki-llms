---
url: https://bun.com/reference/bun/ffi
title: bun:ffi module | API Reference | Bun
source_domain: bun.com
---

# bun:ffi module | API Reference | Bun

module

# [bun:ffi](https://bun.com/reference/bun/ffi)

The `'bun:ffi'` module enables high-performance calls to native libraries from JavaScript. It works with languages that support the C ABI (Zig, Rust, C/C++, C#, Nim, Kotlin, etc).

Bun generates and just-in-time compiles C bindings that efficiently convert values between JavaScript types and native types, using embedded TinyCC (a small and fast C compiler). According to benchmarks, bun:ffi is roughly 2-6x faster than Node.js FFI via Node-API.

**⚠️ Experimental** — bun:ffi has known bugs and limitations, and should not be relied on in production. The most stable way to interact with native code from Bun is to write a Node-API module.

* ### namespace [read](https://bun.com/reference/bun/ffi/read)

  + function [f32](https://bun.com/reference/bun/ffi/read/f32)(

    ptr: [Pointer](https://bun.com/reference/bun/ffi/Pointer),

    byteOffset?: number

    ): number;

    The read function behaves similarly to DataView, but it's usually faster because it doesn't need to create a DataView or ArrayBuffer.

    @param ptr

    The memory address to read

    @param byteOffset

    bytes to skip before reading

    While there are some checks to catch invalid pointers, this is a difficult thing to do safely. Passing an invalid pointer can crash the program and reading beyond the bounds of the pointer will crash the program or cause undefined behavior. Use with care!
  + function [f64](https://bun.com/reference/bun/ffi/read/f64)(

    ptr: [Pointer](https://bun.com/reference/bun/ffi/Pointer),

    byteOffset?: number

    ): number;

    The read function behaves similarly to DataView, but it's usually faster because it doesn't need to create a DataView or ArrayBuffer.

    @param ptr

    The memory address to read

    @param byteOffset

    bytes to skip before reading

    While there are some checks to catch invalid pointers, this is a difficult thing to do safely. Passing an invalid pointer can crash the program and reading beyond the bounds of the pointer will crash the program or cause undefined behavior. Use with care!
  + function [i16](https://bun.com/reference/bun/ffi/read/i16)(

    ptr: [Pointer](https://bun.com/reference/bun/ffi/Pointer),

    byteOffset?: number

    ): number;

    The read function behaves similarly to DataView, but it's usually faster because it doesn't need to create a DataView or ArrayBuffer.

    @param ptr

    The memory address to read

    @param byteOffset

    bytes to skip before reading

    While there are some checks to catch invalid pointers, this is a difficult thing to do safely. Passing an invalid pointer can crash the program and reading beyond the bounds of the pointer will crash the program or cause undefined behavior. Use with care!
  + function [i32](https://bun.com/reference/bun/ffi/read/i32)(

    ptr: [Pointer](https://bun.com/reference/bun/ffi/Pointer),

    byteOffset?: number

    ): number;

    The read function behaves similarly to DataView, but it's usually faster because it doesn't need to create a DataView or ArrayBuffer.

    @param ptr

    The memory address to read

    @param byteOffset

    bytes to skip before reading

    While there are some checks to catch invalid pointers, this is a difficult thing to do safely. Passing an invalid pointer can crash the program and reading beyond the bounds of the pointer will crash the program or cause undefined behavior. Use with care!
  + function [i64](https://bun.com/reference/bun/ffi/read/i64)(

    ptr: [Pointer](https://bun.com/reference/bun/ffi/Pointer),

    byteOffset?: number

    ): bigint;

    The read function behaves similarly to DataView, but it's usually faster because it doesn't need to create a DataView or ArrayBuffer.

    @param ptr

    The memory address to read

    @param byteOffset

    bytes to skip before reading

    While there are some checks to catch invalid pointers, this is a difficult thing to do safely. Passing an invalid pointer can crash the program and reading beyond the bounds of the pointer will crash the program or cause undefined behavior. Use with care!
  + function [i8](https://bun.com/reference/bun/ffi/read/i8)(

    ptr: [Pointer](https://bun.com/reference/bun/ffi/Pointer),

    byteOffset?: number

    ): number;

    The read function behaves similarly to DataView, but it's usually faster because it doesn't need to create a DataView or ArrayBuffer.

    @param ptr

    The memory address to read

    @param byteOffset

    bytes to skip before reading

    While there are some checks to catch invalid pointers, this is a difficult thing to do safely. Passing an invalid pointer can crash the program and reading beyond the bounds of the pointer will crash the program or cause undefined behavior. Use with care!
  + function [intptr](https://bun.com/reference/bun/ffi/read/intptr)(

    ptr: [Pointer](https://bun.com/reference/bun/ffi/Pointer),

    byteOffset?: number

    ): number;

    The read function behaves similarly to DataView, but it's usually faster because it doesn't need to create a DataView or ArrayBuffer.

    @param ptr

    The memory address to read

    @param byteOffset

    bytes to skip before reading

    While there are some checks to catch invalid pointers, this is a difficult thing to do safely. Passing an invalid pointer can crash the program and reading beyond the bounds of the pointer will crash the program or cause undefined behavior. Use with care!
  + function [ptr](https://bun.com/reference/bun/ffi/read/ptr)(

    ptr: [Pointer](https://bun.com/reference/bun/ffi/Pointer),

    byteOffset?: number

    ): number;

    The read function behaves similarly to DataView, but it's usually faster because it doesn't need to create a DataView or ArrayBuffer.

    @param ptr

    The memory address to read

    @param byteOffset

    bytes to skip before reading

    While there are some checks to catch invalid pointers, this is a difficult thing to do safely. Passing an invalid pointer can crash the program and reading beyond the bounds of the pointer will crash the program or cause undefined behavior. Use with care!
  + function [u16](https://bun.com/reference/bun/ffi/read/u16)(

    ptr: [Pointer](https://bun.com/reference/bun/ffi/Pointer),

    byteOffset?: number

    ): number;

    The read function behaves similarly to DataView, but it's usually faster because it doesn't need to create a DataView or ArrayBuffer.

    @param ptr

    The memory address to read

    @param byteOffset

    bytes to skip before reading

    While there are some checks to catch invalid pointers, this is a difficult thing to do safely. Passing an invalid pointer can crash the program and reading beyond the bounds of the pointer will crash the program or cause undefined behavior. Use with care!
  + function [u32](https://bun.com/reference/bun/ffi/read/u32)(

    ptr: [Pointer](https://bun.com/reference/bun/ffi/Pointer),

    byteOffset?: number

    ): number;

    The read function behaves similarly to DataView, but it's usually faster because it doesn't need to create a DataView or ArrayBuffer.

    @param ptr

    The memory address to read

    @param byteOffset

    bytes to skip before reading

    While there are some checks to catch invalid pointers, this is a difficult thing to do safely. Passing an invalid pointer can crash the program and reading beyond the bounds of the pointer will crash the program or cause undefined behavior. Use with care!
  + function [u64](https://bun.com/reference/bun/ffi/read/u64)(

    ptr: [Pointer](https://bun.com/reference/bun/ffi/Pointer),

    byteOffset?: number

    ): bigint;

    The read function behaves similarly to DataView, but it's usually faster because it doesn't need to create a DataView or ArrayBuffer.

    @param ptr

    The memory address to read

    @param byteOffset

    bytes to skip before reading

    While there are some checks to catch invalid pointers, this is a difficult thing to do safely. Passing an invalid pointer can crash the program and reading beyond the bounds of the pointer will crash the program or cause undefined behavior. Use with care!
  + function [u8](https://bun.com/reference/bun/ffi/read/u8)(

    ptr: [Pointer](https://bun.com/reference/bun/ffi/Pointer),

    byteOffset?: number

    ): number;

    The read function behaves similarly to DataView, but it's usually faster because it doesn't need to create a DataView or ArrayBuffer.

    @param ptr

    The memory address to read

    @param byteOffset

    bytes to skip before reading

    While there are some checks to catch invalid pointers, this is a difficult thing to do safely. Passing an invalid pointer can crash the program and reading beyond the bounds of the pointer will crash the program or cause undefined behavior. Use with care!
* ### enum [FFIType](https://bun.com/reference/bun/ffi/FFIType)

  + [bool](https://bun.com/reference/bun/ffi/FFIType/bool) = 11

    Boolean value

    Must be `true` or `false`. `0` and `1` type coercion is not supported.

    In C, this corresponds to:

    ```
    bool
    _Bool
    ```
  + [buffer](https://bun.com/reference/bun/ffi/FFIType/buffer) = 20
  + [char](https://bun.com/reference/bun/ffi/FFIType/char) = 0
  + [cstring](https://bun.com/reference/bun/ffi/FFIType/cstring) = 14

    When used as a `returns`, this will automatically become a CString.

    When used in `args` it is equivalent to FFIType.pointer
  + [double](https://bun.com/reference/bun/ffi/FFIType/double) = 9

    IEEE-754 double precision float
  + [f32](https://bun.com/reference/bun/ffi/FFIType/f32) = 10

    Alias of FFIType.float
  + [f64](https://bun.com/reference/bun/ffi/FFIType/f64) = 9

    Alias of FFIType.double
  + [float](https://bun.com/reference/bun/ffi/FFIType/float) = 10

    IEEE-754 single precision float
  + [function](https://bun.com/reference/bun/ffi/FFIType/function) = 17
  + [i16](https://bun.com/reference/bun/ffi/FFIType/i16) = 3

    16-bit signed integer

    Must be a value between -32768 and 32767

    When passing to a FFI function (C ABI), type coercion is not performed.

    In C:

    ```
    in16_t
    short // on arm64 & x64
    ```

    In JavaScript:

    ```
    var num = 0;
    ```
  + [i32](https://bun.com/reference/bun/ffi/FFIType/i32) = 5

    32-bit signed integer

    Alias of FFIType.int32\_t
  + [i64](https://bun.com/reference/bun/ffi/FFIType/i64) = 7

    i64 is a 64-bit signed integer
  + [i64\_fast](https://bun.com/reference/bun/ffi/FFIType/i64_fast) = 15

    Attempt to coerce `BigInt` into a `Number` if it fits. This improves performance but means you might get a `BigInt` or you might get a `number`.

    In C, this always becomes `int64_t`

    In JavaScript, this could be number or it could be BigInt, depending on what value is passed in.
  + [i8](https://bun.com/reference/bun/ffi/FFIType/i8) = 1

    8-bit signed integer

    Must be a value between -127 and 127

    When passing to a FFI function (C ABI), type coercion is not performed.

    In C:

    ```
    signed char
    char // on x64 & aarch64 macOS
    ```

    In JavaScript:

    ```
    var num = 0;
    ```
  + [int](https://bun.com/reference/bun/ffi/FFIType/int) = 5

    32-bit signed integer

    The same as `int` in C

    ```
    int
    ```
  + [int16\_t](https://bun.com/reference/bun/ffi/FFIType/int16_t) = 3

    16-bit signed integer

    Must be a value between -32768 and 32767

    When passing to a FFI function (C ABI), type coercion is not performed.

    In C:

    ```
    in16_t
    short // on arm64 & x64
    ```

    In JavaScript:

    ```
    var num = 0;
    ```
  + [int32\_t](https://bun.com/reference/bun/ffi/FFIType/int32_t) = 5

    32-bit signed integer
  + [int64\_t](https://bun.com/reference/bun/ffi/FFIType/int64_t) = 7

    int64 is a 64-bit signed integer
  + [int8\_t](https://bun.com/reference/bun/ffi/FFIType/int8_t) = 1

    8-bit signed integer

    Must be a value between -127 and 127

    When passing to a FFI function (C ABI), type coercion is not performed.

    In C:

    ```
    signed char
    char // on x64 & aarch64 macOS
    ```

    In JavaScript:

    ```
    var num = 0;
    ```
  + [napi\_env](https://bun.com/reference/bun/ffi/FFIType/napi_env) = 18
  + [napi\_value](https://bun.com/reference/bun/ffi/FFIType/napi_value) = 19
  + [pointer](https://bun.com/reference/bun/ffi/FFIType/pointer) = 12

    Pointer value

    alias of FFIType.ptr
  + [ptr](https://bun.com/reference/bun/ffi/FFIType/ptr) = 12

    Pointer value

    See Bun.FFI.ptr for more information

    In C:

    ```
    void*
    ```

    In JavaScript:

    ```
    ptr(new Uint8Array(1))
    ```
  + [u16](https://bun.com/reference/bun/ffi/FFIType/u16) = 4

    16-bit unsigned integer

    Must be a value between 0 and 65535, inclusive.

    When passing to a FFI function (C ABI), type coercion is not performed.

    In C:

    ```
    uint16_t
    unsigned short // on arm64 & x64
    ```

    In JavaScript:

    ```
    var num = 0;
    ```
  + [u32](https://bun.com/reference/bun/ffi/FFIType/u32) = 6

    32-bit unsigned integer

    Alias of FFIType.uint32\_t
  + [u64](https://bun.com/reference/bun/ffi/FFIType/u64) = 8

    64-bit unsigned integer
  + [u64\_fast](https://bun.com/reference/bun/ffi/FFIType/u64_fast) = 16

    Attempt to coerce `BigInt` into a `Number` if it fits. This improves performance but means you might get a `BigInt` or you might get a `number`.

    In C, this always becomes `uint64_t`

    In JavaScript, this could be number or it could be BigInt, depending on what value is passed in.
  + [u8](https://bun.com/reference/bun/ffi/FFIType/u8) = 2

    8-bit unsigned integer

    Must be a value between 0 and 255

    When passing to a FFI function (C ABI), type coercion is not performed.

    In C:

    ```
    unsigned char
    ```

    In JavaScript:

    ```
    var num = 0;
    ```
  + [uint16\_t](https://bun.com/reference/bun/ffi/FFIType/uint16_t) = 4

    16-bit unsigned integer

    Must be a value between 0 and 65535, inclusive.

    When passing to a FFI function (C ABI), type coercion is not performed.

    In C:

    ```
    uint16_t
    unsigned short // on arm64 & x64
    ```

    In JavaScript:

    ```
    var num = 0;
    ```
  + [uint32\_t](https://bun.com/reference/bun/ffi/FFIType/uint32_t) = 6

    32-bit unsigned integer

    The same as `unsigned int` in C (on x64 & arm64)

    C:

    ```
    unsigned int
    ```

    JavaScript:

    ```
    ptr(new Uint32Array(1))
    ```
  + [uint64\_t](https://bun.com/reference/bun/ffi/FFIType/uint64_t) = 8

    64-bit unsigned integer
  + [uint8\_t](https://bun.com/reference/bun/ffi/FFIType/uint8_t) = 2

    8-bit unsigned integer

    Must be a value between 0 and 255

    When passing to a FFI function (C ABI), type coercion is not performed.

    In C:

    ```
    unsigned char
    ```

    In JavaScript:

    ```
    var num = 0;
    ```
  + [void](https://bun.com/reference/bun/ffi/FFIType/void) = 13

    void value

    void arguments are not supported

    void return type is the default return type

    In C:

    ```
    void
    ```
* ### class [CString](https://bun.com/reference/bun/ffi/CString)

  Get a string from a UTF-8 encoded C string If `byteLength` is not provided, the string is assumed to be null-terminated.

  ```
  var ptr = lib.symbols.getVersion();
  console.log(new CString(ptr));
  ```

  + [byteLength](https://bun.com/reference/bun/ffi/CString/byteLength)?: number
  + [byteOffset](https://bun.com/reference/bun/ffi/CString/byteOffset)?: number
  + readonly [length](https://bun.com/reference/bun/ffi/CString/length): number

    Returns the length of a String object.
  + [ptr](https://bun.com/reference/bun/ffi/CString/ptr): [Pointer](https://bun.com/reference/bun/ffi/Pointer)

    The ptr to the C string

    This `CString` instance is a clone of the string, so it is safe to continue using this instance after the `ptr` has been freed.
  + [[Symbol.iterator]](https://bun.com/reference/bun/ffi/CString/[iterator])(): StringIterator<string>;

    Iterator
  + [at](https://bun.com/reference/bun/ffi/CString/at)(

    index: number

    ): undefined | string;

    Returns a new String consisting of the single UTF-16 code unit located at the specified index.

    @param index

    The zero-based index of the desired code unit. A negative index will count back from the last item.

  + [charAt](https://bun.com/reference/bun/ffi/CString/charAt)(

    pos: number

    ): string;

    Returns the character at the specified index.

    @param pos

    The zero-based index of the desired character.
  + [charCodeAt](https://bun.com/reference/bun/ffi/CString/charCodeAt)(

    index: number

    ): number;

    Returns the Unicode value of the character at the specified location.

    @param index

    The zero-based index of the desired character. If there is no character at the specified index, NaN is returned.
  + [codePointAt](https://bun.com/reference/bun/ffi/CString/codePointAt)(

    pos: number

    ): undefined | number;

    Returns a nonnegative integer Number less than 1114112 (0x110000) that is the code point value of the UTF-16 encoded code point starting at the string element at position pos in the String resulting from converting this object to a String. If there is no element at that position, the result is undefined. If a valid UTF-16 surrogate pair does not begin at pos, the result is the code unit at pos.
  + [concat](https://bun.com/reference/bun/ffi/CString/concat)(

    ...strings: string[]

    ): string;

    Returns a string that contains the concatenation of two or more strings.

    @param strings

    The strings to append to the end of the string.
  + [endsWith](https://bun.com/reference/bun/ffi/CString/endsWith)(

    searchString: string,

    endPosition?: number

    ): boolean;

    Returns true if the sequence of elements of searchString converted to a String is the same as the corresponding elements of this object (converted to a String) starting at endPosition – length(this). Otherwise returns false.

  + [includes](https://bun.com/reference/bun/ffi/CString/includes)(

    searchString: string,

    position?: number

    ): boolean;

    Returns true if searchString appears as a substring of the result of converting this object to a String, at one or more positions that are greater than or equal to position; otherwise, returns false.

    @param searchString

    search string

    @param position

    If position is undefined, 0 is assumed, so as to search all of the String.
  + [indexOf](https://bun.com/reference/bun/ffi/CString/indexOf)(

    searchString: string,

    position?: number

    ): number;

    Returns the position of the first occurrence of a substring.

    @param searchString

    The substring to search for in the string

    @param position

    The index at which to begin searching the String object. If omitted, search starts at the beginning of the string.
  + [isWellFormed](https://bun.com/reference/bun/ffi/CString/isWellFormed)(): boolean;

    Returns true if all leading surrogates and trailing surrogates appear paired and in order.
  + [lastIndexOf](https://bun.com/reference/bun/ffi/CString/lastIndexOf)(

    searchString: string,

    position?: number

    ): number;

    Returns the last occurrence of a substring in the string.

    @param searchString

    The substring to search for.

    @param position

    The index at which to begin searching. If omitted, the search begins at the end of the string.
  + [localeCompare](https://bun.com/reference/bun/ffi/CString/localeCompare)(

    that: string

    ): number;

    Determines whether two strings are equivalent in the current locale.

    @param that

    String to compare to target string

    [localeCompare](https://bun.com/reference/bun/ffi/CString/localeCompare)(

    that: string,

    locales?: string | string[],

    options?: CollatorOptions

    ): number;

    Determines whether two strings are equivalent in the current or specified locale.

    @param that

    String to compare to target string

    @param locales

    A locale string or array of locale strings that contain one or more language or locale tags. If you include more than one locale string, list them in descending order of priority so that the first entry is the preferred locale. If you omit this parameter, the default locale of the JavaScript runtime is used. This parameter must conform to BCP 47 standards; see the Intl.Collator object for details.

    @param options

    An object that contains one or more properties that specify comparison options. see the Intl.Collator object for details.

    [localeCompare](https://bun.com/reference/bun/ffi/CString/localeCompare)(

    that: string,

    locales?: LocalesArgument,

    options?: CollatorOptions

    ): number;

    Determines whether two strings are equivalent in the current or specified locale.

    @param that

    String to compare to target string

    @param locales

    A locale string or array of locale strings that contain one or more language or locale tags. If you include more than one locale string, list them in descending order of priority so that the first entry is the preferred locale. If you omit this parameter, the default locale of the JavaScript runtime is used. This parameter must conform to BCP 47 standards; see the Intl.Collator object for details.

    @param options

    An object that contains one or more properties that specify comparison options. see the Intl.Collator object for details.
  + [match](https://bun.com/reference/bun/ffi/CString/match)(

    regexp: string | RegExp

    ): null | RegExpMatchArray;

    Matches a string with a regular expression, and returns an array containing the results of that search.

    @param regexp

    A variable name or string literal containing the regular expression pattern and flags.

    [match](https://bun.com/reference/bun/ffi/CString/match)(

    matcher: { [match](string: string): null | RegExpMatchArray }

    ): null | RegExpMatchArray;

    Matches a string or an object that supports being matched against, and returns an array containing the results of that search, or null if no matches are found.

    @param matcher

    An object that supports being matched against.
  + [matchAll](https://bun.com/reference/bun/ffi/CString/matchAll)(

    regexp: RegExp

    ): RegExpStringIterator<RegExpExecArray>;

    Matches a string with a regular expression, and returns an iterable of matches containing the results of that search.

    @param regexp

    A variable name or string literal containing the regular expression pattern and flags.
  + [normalize](https://bun.com/reference/bun/ffi/CString/normalize)(

    form: 'NFC' | 'NFD' | 'NFKC' | 'NFKD'

    ): string;

    Returns the String value result of normalizing the string into the normalization form named by form as specified in Unicode Standard Annex #15, Unicode Normalization Forms.

    @param form

    Applicable values: "NFC", "NFD", "NFKC", or "NFKD", If not specified default is "NFC"

    [normalize](https://bun.com/reference/bun/ffi/CString/normalize)(

    form?: string

    ): string;

    Returns the String value result of normalizing the string into the normalization form named by form as specified in Unicode Standard Annex #15, Unicode Normalization Forms.

    @param form

    Applicable values: "NFC", "NFD", "NFKC", or "NFKD", If not specified default is "NFC"
  + [padEnd](https://bun.com/reference/bun/ffi/CString/padEnd)(

    maxLength: number,

    fillString?: string

    ): string;

    Pads the current string with a given string (possibly repeated) so that the resulting string reaches a given length. The padding is applied from the end (right) of the current string.

    @param maxLength

    The length of the resulting string once the current string has been padded. If this parameter is smaller than the current string's length, the current string will be returned as it is.

    @param fillString

    The string to pad the current string with. If this string is too long, it will be truncated and the left-most part will be applied. The default value for this parameter is " " (U+0020).
  + [padStart](https://bun.com/reference/bun/ffi/CString/padStart)(

    maxLength: number,

    fillString?: string

    ): string;

    Pads the current string with a given string (possibly repeated) so that the resulting string reaches a given length. The padding is applied from the start (left) of the current string.

    @param maxLength

    The length of the resulting string once the current string has been padded. If this parameter is smaller than the current string's length, the current string will be returned as it is.

    @param fillString

    The string to pad the current string with. If this string is too long, it will be truncated and the left-most part will be applied. The default value for this parameter is " " (U+0020).
  + [repeat](https://bun.com/reference/bun/ffi/CString/repeat)(

    count: number

    ): string;

    Returns a String value that is made from count copies appended together. If count is 0, the empty string is returned.

    @param count

    number of copies to append
  + [replace](https://bun.com/reference/bun/ffi/CString/replace)(

    searchValue: string | RegExp,

    replaceValue: string

    ): string;

    Replaces text in a string, using a regular expression or search string.

    @param searchValue

    A string or regular expression to search for.

    @param replaceValue

    A string containing the text to replace. When the searchValue is a `RegExp`, all matches are replaced if the `g` flag is set (or only those matches at the beginning, if the `y` flag is also present). Otherwise, only the first match of searchValue is replaced.

    [replace](https://bun.com/reference/bun/ffi/CString/replace)(

    searchValue: string | RegExp,

    replacer: (substring: string, ...args: any[]) => string

    ): string;

    Replaces text in a string, using a regular expression or search string.

    @param searchValue

    A string to search for.

    @param replacer

    A function that returns the replacement text.

    [replace](https://bun.com/reference/bun/ffi/CString/replace)(

    searchValue: { [replace](string: string, replaceValue: string): string },

    replaceValue: string

    ): string;

    Passes a string and replaceValue to the `[Symbol.replace]` method on searchValue. This method is expected to implement its own replacement algorithm.

    @param searchValue

    An object that supports searching for and replacing matches within a string.

    @param replaceValue

    The replacement text.

    [replace](https://bun.com/reference/bun/ffi/CString/replace)(

    searchValue: { [replace](string: string, replacer: (substring: string, ...args: any[]) => string): string },

    replacer: (substring: string, ...args: any[]) => string

    ): string;

    Replaces text in a string, using an object that supports replacement within a string.

    @param searchValue

    A object can search for and replace matches within a string.

    @param replacer

    A function that returns the replacement text.
  + [replaceAll](https://bun.com/reference/bun/ffi/CString/replaceAll)(

    searchValue: string | RegExp,

    replaceValue: string

    ): string;

    Replace all instances of a substring in a string, using a regular expression or search string.

    @param searchValue

    A string to search for.

    @param replaceValue

    A string containing the text to replace for every successful match of searchValue in this string.

    [replaceAll](https://bun.com/reference/bun/ffi/CString/replaceAll)(

    searchValue: string | RegExp,

    replacer: (substring: string, ...args: any[]) => string

    ): string;

    Replace all instances of a substring in a string, using a regular expression or search string.

    @param searchValue

    A string to search for.

    @param replacer

    A function that returns the replacement text.
  + [search](https://bun.com/reference/bun/ffi/CString/search)(

    regexp: string | RegExp

    ): number;

    Finds the first substring match in a regular expression search.

    @param regexp

    The regular expression pattern and applicable flags.

    [search](https://bun.com/reference/bun/ffi/CString/search)(

    searcher: { [search](string: string): number }

    ): number;

    Finds the first substring match in a regular expression search.

    @param searcher

    An object which supports searching within a string.
  + [slice](https://bun.com/reference/bun/ffi/CString/slice)(

    start?: number,

    end?: number

    ): string;

    Returns a section of a string.

    @param start

    The index to the beginning of the specified portion of stringObj.

    @param end

    The index to the end of the specified portion of stringObj. The substring includes the characters up to, but not including, the character indicated by end. If this value is not specified, the substring continues to the end of stringObj.
  + [split](https://bun.com/reference/bun/ffi/CString/split)(

    separator: string | RegExp,

    limit?: number

    ): string[];

    Split a string into substrings using the specified separator and return them as an array.

    @param separator

    A string that identifies character or characters to use in separating the string. If omitted, a single-element array containing the entire string is returned.

    @param limit

    A value used to limit the number of elements returned in the array.

    [split](https://bun.com/reference/bun/ffi/CString/split)(

    splitter: { [split](string: string, limit?: number): string[] },

    limit?: number

    ): string[];

    Split a string into substrings using the specified separator and return them as an array.

    @param splitter

    An object that can split a string.

    @param limit

    A value used to limit the number of elements returned in the array.
  + [startsWith](https://bun.com/reference/bun/ffi/CString/startsWith)(

    searchString: string,

    position?: number

    ): boolean;

    Returns true if the sequence of elements of searchString converted to a String is the same as the corresponding elements of this object (converted to a String) starting at position. Otherwise returns false.

  + [substring](https://bun.com/reference/bun/ffi/CString/substring)(

    start: number,

    end?: number

    ): string;

    Returns the substring at the specified location within a String object.

    @param start

    The zero-based index number indicating the beginning of the substring.

    @param end

    Zero-based index number indicating the end of the substring. The substring includes the characters up to, but not including, the character indicated by end. If end is omitted, the characters from start through the end of the original string are returned.
  + [toLocaleLowerCase](https://bun.com/reference/bun/ffi/CString/toLocaleLowerCase)(

    locales?: string | string[]

    ): string;

    Converts all alphabetic characters to lowercase, taking into account the host environment's current locale.

    [toLocaleLowerCase](https://bun.com/reference/bun/ffi/CString/toLocaleLowerCase)(

    locales?: LocalesArgument

    ): string;

    Converts all alphabetic characters to lowercase, taking into account the host environment's current locale.
  + [toLocaleUpperCase](https://bun.com/reference/bun/ffi/CString/toLocaleUpperCase)(

    locales?: string | string[]

    ): string;

    Returns a string where all alphabetic characters have been converted to uppercase, taking into account the host environment's current locale.

    [toLocaleUpperCase](https://bun.com/reference/bun/ffi/CString/toLocaleUpperCase)(

    locales?: LocalesArgument

    ): string;

    Returns a string where all alphabetic characters have been converted to uppercase, taking into account the host environment's current locale.
  + [toLowerCase](https://bun.com/reference/bun/ffi/CString/toLowerCase)(): string;

    Converts all the alphabetic characters in a string to lowercase.
  + [toString](https://bun.com/reference/bun/ffi/CString/toString)(): string;

    Returns a string representation of a string.
  + [toUpperCase](https://bun.com/reference/bun/ffi/CString/toUpperCase)(): string;

    Converts all the alphabetic characters in a string to uppercase.
  + [toWellFormed](https://bun.com/reference/bun/ffi/CString/toWellFormed)(): string;

    Returns a string where all lone or out-of-order surrogates have been replaced by the Unicode replacement character (U+FFFD).
  + [trim](https://bun.com/reference/bun/ffi/CString/trim)(): string;

    Removes the leading and trailing white space and line terminator characters from a string.
  + [trimEnd](https://bun.com/reference/bun/ffi/CString/trimEnd)(): string;

    Removes the trailing white space and line terminator characters from a string.

  + [trimStart](https://bun.com/reference/bun/ffi/CString/trimStart)(): string;

    Removes the leading white space and line terminator characters from a string.
  + [valueOf](https://bun.com/reference/bun/ffi/CString/valueOf)(): string;

    Returns the primitive value of the specified object.
  + static [fromCharCode](https://bun.com/reference/bun/ffi/CString/fromCharCode)(

    ...codes: number[]

    ): string;
  + static [fromCodePoint](https://bun.com/reference/bun/ffi/CString/fromCodePoint)(

    ...codePoints: number[]

    ): string;

    Return the String value whose elements are, in order, the elements in the List elements. If length is 0, the empty string is returned.
  + static [raw](https://bun.com/reference/bun/ffi/CString/raw)(

    template: { raw: readonly string[] | ArrayLike<string> },

    ...substitutions: any[]

    ): string;

    String.raw is usually used as a tag function of a Tagged Template String. When called as such, the first argument will be a well formed template call site object and the rest parameter will contain the substitution values. It can also be called directly, for example, to interleave strings and values from your own tag function, and in this case the only thing it needs from the first argument is the raw property.

    @param template

    A well-formed template string call site representation.

    @param substitutions

    A set of substitution values.
* ### class [JSCallback](https://bun.com/reference/bun/ffi/JSCallback)

  Pass a JavaScript function to FFI (Foreign Function Interface)

  + readonly [ptr](https://bun.com/reference/bun/ffi/JSCallback/ptr): null | [Pointer](https://bun.com/reference/bun/ffi/Pointer)

    The pointer to the C function

    Becomes `null` once JSCallback.prototype.close is called
  + readonly [threadsafe](https://bun.com/reference/bun/ffi/JSCallback/threadsafe): boolean

    Can the callback be called from a different thread?
  + [close](https://bun.com/reference/bun/ffi/JSCallback/close)(): void;

    Free the memory allocated for the callback

    If called multiple times, does nothing after the first call.
* const [FFIFunctionCallableSymbol](https://bun.com/reference/bun/ffi/FFIFunctionCallableSymbol): unique symbol
* const [suffix](https://bun.com/reference/bun/ffi/suffix): string

  Platform-specific file extension name for dynamic libraries

  "." is not included

  ```
  "dylib" // macOS
  ```
* function [cc](https://bun.com/reference/bun/ffi/cc)<Fns extends Record<string, [FFIFunction](https://bun.com/reference/bun/ffi/FFIFunction)>>(

  options: { define: Record<string, string>; flags: string | string[]; include: string | string[]; library: string | string[]; source: string | [BunFile](https://bun.com/reference/bun/BunFile) | [URL](https://bun.com/reference/globals/URL); symbols: Fns }

  ): [Library](https://bun.com/reference/bun/ffi/Library)<Fns>;

  **Experimental:** Compile ISO C11 source code using TinyCC, and make symbols available as functions to JavaScript.

  @returns

  Library<Fns>

  ## [Hello, World!](https://bun.com/reference/bun/ffi#hello-world)

  JavaScript:

  ```
  import { cc } from "bun:ffi";
  import source from "./hello.c" with {type: "file"};
  const {symbols: {hello}} = cc({
    source,
    symbols: {
      hello: {
        returns: "cstring",
        args: [],
      },
    },
  });
  // "Hello, World!"
  console.log(hello());
  ```

  `./hello.c`:

  ```
  #include <stdio.h>
  const char* hello() {
    return "Hello, World!";
  }
  ```
* function [CFunction](https://bun.com/reference/bun/ffi/CFunction)(

  fn: [FFIFunction](https://bun.com/reference/bun/ffi/FFIFunction) & { ptr: [Pointer](https://bun.com/reference/bun/ffi/Pointer) }

  ): CallableFunction & { close(): void };

  Turn a native library's function pointer into a JavaScript function

  Libraries using Node-API & bun:ffi in the same module could use this to skip an extra dlopen() step.

  @param fn

  FFIFunction declaration. `ptr` is required

  ```
  import {CFunction} from 'bun:ffi';

  const getVersion = new CFunction({
    returns: "cstring",
    args: [],
    ptr: myNativeLibraryGetVersion,
  });
  getVersion();
  getVersion.close();
  ```

  This is powered by just-in-time compiling C wrappers that convert JavaScript types to C types and back. Internally, bun uses [tinycc](https://github.com/TinyCC/tinycc), so a big thanks goes to Fabrice Bellard and TinyCC maintainers for making this possible.
* function [dlopen](https://bun.com/reference/bun/ffi/dlopen)<Fns extends Record<string, [FFIFunction](https://bun.com/reference/bun/ffi/FFIFunction)>>(

  name: string | [BunFile](https://bun.com/reference/bun/BunFile) | [URL](https://bun.com/reference/globals/URL),

  symbols: Fns

  ): [Library](https://bun.com/reference/bun/ffi/Library)<Fns>;

  Open a library using `"bun:ffi"`

  @param name

  The name of the library or file path. This will be passed to `dlopen()`

  @param symbols

  Map of symbols to load where the key is the symbol name and the value is the FFIFunction

  ```
  import {dlopen} from 'bun:ffi';

  const lib = dlopen("duckdb.dylib", {
    get_version: {
      returns: "cstring",
      args: [],
    },
  });
  lib.symbols.get_version();
  // "1.0.0"
  ```

  This is powered by just-in-time compiling C wrappers that convert JavaScript types to C types and back. Internally, bun uses [tinycc](https://github.com/TinyCC/tinycc), so a big thanks goes to Fabrice Bellard and TinyCC maintainers for making this possible.
* function [linkSymbols](https://bun.com/reference/bun/ffi/linkSymbols)<Fns extends Record<string, [FFIFunction](https://bun.com/reference/bun/ffi/FFIFunction)>>(

  symbols: Fns

  ): [Library](https://bun.com/reference/bun/ffi/Library)<Fns>;

  Link a map of symbols to JavaScript functions

  This lets you use native libraries that were already loaded somehow. You usually will want dlopen instead.

  You could use this with Node-API to skip loading a second time.

  @param symbols

  Map of symbols to load where the key is the symbol name and the value is the FFIFunction

  ```
  import { linkSymbols } from "bun:ffi";

  const [majorPtr, minorPtr, patchPtr] = getVersionPtrs();

  const lib = linkSymbols({
    // Unlike with dlopen(), the names here can be whatever you want
    getMajor: {
      returns: "cstring",
      args: [],

      // Since this doesn't use dlsym(), you have to provide a valid ptr
      // That ptr could be a number or a bigint
      // An invalid pointer will crash your program.
      ptr: majorPtr,
    },
    getMinor: {
      returns: "cstring",
      args: [],
      ptr: minorPtr,
    },
    getPatch: {
      returns: "cstring",
      args: [],
      ptr: patchPtr,
    },
  });

  const [major, minor, patch] = [
    lib.symbols.getMajor(),
    lib.symbols.getMinor(),
    lib.symbols.getPatch(),
  ];
  ```

  This is powered by just-in-time compiling C wrappers that convert JavaScript types to C types and back. Internally, bun uses [tinycc](https://github.com/TinyCC/tinycc), so a big thanks goes to Fabrice Bellard and TinyCC maintainers for making this possible.
* function [ptr](https://bun.com/reference/bun/ffi/ptr)(

  view: ArrayBufferLike | TypedArray<ArrayBufferLike> | DataView<ArrayBufferLike>,

  byteOffset?: number

  ): [Pointer](https://bun.com/reference/bun/ffi/Pointer);

  Get the pointer backing a TypedArray or ArrayBuffer

  Use this to pass TypedArray or ArrayBuffer to C functions.

  This is for use with FFI functions. For performance reasons, FFI will not automatically convert typed arrays to C pointers.

  @param view

  the typed array or array buffer to get the pointer for

  @param byteOffset

  optional offset into the view in bytes

  From JavaScript:

  ```
  const array = new Uint8Array(10);
  const rawPtr = ptr(array);
  myFFIFunction(rawPtr);
  ```

  To C:

  ```
  void myFFIFunction(char* rawPtr) {
   // Do something with rawPtr
  }
  ```
* function [toArrayBuffer](https://bun.com/reference/bun/ffi/toArrayBuffer)(

  ptr: [Pointer](https://bun.com/reference/bun/ffi/Pointer),

  byteOffset?: number,

  byteLength?: number

  ): [ArrayBuffer](https://bun.com/reference/globals/ArrayBuffer);

  Read a pointer as an ArrayBuffer

  If `byteLength` is not provided, the pointer is assumed to be 0-terminated.

  @param ptr

  The memory address to read

  @param byteOffset

  bytes to skip before reading

  @param byteLength

  bytes to read

  While there are some checks to catch invalid pointers, this is a difficult thing to do safely. Passing an invalid pointer can crash the program and reading beyond the bounds of the pointer will crash the program or cause undefined behavior. Use with care!
* function [toBuffer](https://bun.com/reference/bun/ffi/toBuffer)(

  ptr: [Pointer](https://bun.com/reference/bun/ffi/Pointer),

  byteOffset?: number,

  byteLength?: number

  ): [Buffer](https://bun.com/reference/node/buffer/Buffer);

  Read a pointer as a Buffer

  If `byteLength` is not provided, the pointer is assumed to be 0-terminated.

  @param ptr

  The memory address to read

  @param byteOffset

  bytes to skip before reading

  @param byteLength

  bytes to read

  While there are some checks to catch invalid pointers, this is a difficult thing to do safely. Passing an invalid pointer can crash the program and reading beyond the bounds of the pointer will crash the program or cause undefined behavior. Use with care!
* function [viewSource](https://bun.com/reference/bun/ffi/viewSource)(

  symbols: Readonly,

  is\_callback?: false

  ): string[];

  View the generated C code for FFI bindings

  You probably won't need this unless there's a bug in the FFI bindings generator or you're just curious.

  function [viewSource](https://bun.com/reference/bun/ffi/viewSource)(

  callback: [FFIFunction](https://bun.com/reference/bun/ffi/FFIFunction),

  is\_callback: true

  ): string;

  View the generated C code for FFI bindings

  You probably won't need this unless there's a bug in the FFI bindings generator or you're just curious.

## Type definitions

* ### interface [FFIFunction](https://bun.com/reference/bun/ffi/FFIFunction)

  + readonly [args](https://bun.com/reference/bun/ffi/FFIFunction/args)?: readonly [FFITypeOrString](https://bun.com/reference/bun/ffi/FFITypeOrString)[]

    Arguments to a FFI function (C ABI)

    Defaults to an empty array, which means no arguments.

    To pass a pointer, use "ptr" or "pointer" as the type name. To get a pointer, see ptr.

    From JavaScript:

    ```
    import { dlopen, FFIType, suffix } from "bun:ffi"

    const lib = dlopen(`adder.${suffix}`, {
    	add: {
    		// FFIType can be used or you can pass string labels.
    		args: [FFIType.i32, "i32"],
    		returns: "i32",
    	},
    })
    lib.symbols.add(1, 2)
    ```

    In C:

    ```
    int add(int a, int b) {
      return a + b;
    }
    ```
  + readonly [ptr](https://bun.com/reference/bun/ffi/FFIFunction/ptr)?: bigint | [Pointer](https://bun.com/reference/bun/ffi/Pointer)

    Function pointer to the native function

    If provided, instead of using dlsym() to lookup the function, Bun will use this instead. This pointer should not be null (0).

    This is useful if the library has already been loaded or if the module is also using Node-API.
  + readonly [returns](https://bun.com/reference/bun/ffi/FFIFunction/returns)?: [FFITypeOrString](https://bun.com/reference/bun/ffi/FFITypeOrString)

    Return type to a FFI function (C ABI)

    Defaults to FFIType.void

    To pass a pointer, use "ptr" or "pointer" as the type name. To get a pointer, see ptr.

    From JavaScript:

    ```
    import { dlopen, CString } from "bun:ffi"

    const lib = dlopen('z', {
       version: {
         returns: "ptr",
      }
    });
    console.log(new CString(lib.symbols.version()));
    ```

    In C:

    ```
    char* version()
    {
     return "1.0.0";
    }
    ```
  + readonly [threadsafe](https://bun.com/reference/bun/ffi/FFIFunction/threadsafe)?: boolean

    Can C/FFI code call this function from a separate thread?

    Only supported with JSCallback.

    This does not make the function run in a separate thread. It is still up to the application/library to run their code in a separate thread.

    By default, JSCallback calls are not thread-safe. Turning this on incurs a small performance penalty for every function call. That small performance penalty needs to be less than the performance gain from running the function in a separate thread.
* ### interface [FFITypeStringToType](https://bun.com/reference/bun/ffi/FFITypeStringToType)

  + [bool](https://bun.com/reference/bun/ffi/FFITypeStringToType/bool): [bool](https://bun.com/reference/bun/ffi/FFIType/bool)
  + [buffer](https://bun.com/reference/bun/ffi/FFITypeStringToType/buffer): [buffer](https://bun.com/reference/bun/ffi/FFIType/buffer)
  + [callback](https://bun.com/reference/bun/ffi/FFITypeStringToType/callback): [ptr](https://bun.com/reference/bun/ffi/FFIType/ptr)
  + [char](https://bun.com/reference/bun/ffi/FFITypeStringToType/char): [char](https://bun.com/reference/bun/ffi/FFIType/char)
  + [cstring](https://bun.com/reference/bun/ffi/FFITypeStringToType/cstring): [cstring](https://bun.com/reference/bun/ffi/FFIType/cstring)
  + [double](https://bun.com/reference/bun/ffi/FFITypeStringToType/double): [double](https://bun.com/reference/bun/ffi/FFIType/double)
  + [f32](https://bun.com/reference/bun/ffi/FFITypeStringToType/f32): [float](https://bun.com/reference/bun/ffi/FFIType/float)
  + [f64](https://bun.com/reference/bun/ffi/FFITypeStringToType/f64): [double](https://bun.com/reference/bun/ffi/FFIType/double)
  + [float](https://bun.com/reference/bun/ffi/FFITypeStringToType/float): [float](https://bun.com/reference/bun/ffi/FFIType/float)
  + [function](https://bun.com/reference/bun/ffi/FFITypeStringToType/function): [ptr](https://bun.com/reference/bun/ffi/FFIType/ptr)
  + [i16](https://bun.com/reference/bun/ffi/FFITypeStringToType/i16): [int16\_t](https://bun.com/reference/bun/ffi/FFIType/int16_t)
  + [i32](https://bun.com/reference/bun/ffi/FFITypeStringToType/i32): [int32\_t](https://bun.com/reference/bun/ffi/FFIType/int32_t)
  + [i64](https://bun.com/reference/bun/ffi/FFITypeStringToType/i64): [int64\_t](https://bun.com/reference/bun/ffi/FFIType/int64_t)
  + [i8](https://bun.com/reference/bun/ffi/FFITypeStringToType/i8): [int8\_t](https://bun.com/reference/bun/ffi/FFIType/int8_t)
  + [int](https://bun.com/reference/bun/ffi/FFITypeStringToType/int): [int32\_t](https://bun.com/reference/bun/ffi/FFIType/int32_t)
  + [int16\_t](https://bun.com/reference/bun/ffi/FFITypeStringToType/int16_t): [int16\_t](https://bun.com/reference/bun/ffi/FFIType/int16_t)
  + [int32\_t](https://bun.com/reference/bun/ffi/FFITypeStringToType/int32_t): [int32\_t](https://bun.com/reference/bun/ffi/FFIType/int32_t)
  + [int64\_t](https://bun.com/reference/bun/ffi/FFITypeStringToType/int64_t): [int64\_t](https://bun.com/reference/bun/ffi/FFIType/int64_t)
  + [int8\_t](https://bun.com/reference/bun/ffi/FFITypeStringToType/int8_t): [int8\_t](https://bun.com/reference/bun/ffi/FFIType/int8_t)
  + [napi\_env](https://bun.com/reference/bun/ffi/FFITypeStringToType/napi_env): [napi\_env](https://bun.com/reference/bun/ffi/FFIType/napi_env)
  + [napi\_value](https://bun.com/reference/bun/ffi/FFITypeStringToType/napi_value): [napi\_value](https://bun.com/reference/bun/ffi/FFIType/napi_value)
  + [pointer](https://bun.com/reference/bun/ffi/FFITypeStringToType/pointer): [ptr](https://bun.com/reference/bun/ffi/FFIType/ptr)
  + [ptr](https://bun.com/reference/bun/ffi/FFITypeStringToType/ptr): [ptr](https://bun.com/reference/bun/ffi/FFIType/ptr)
  + [u16](https://bun.com/reference/bun/ffi/FFITypeStringToType/u16): [uint16\_t](https://bun.com/reference/bun/ffi/FFIType/uint16_t)
  + [u32](https://bun.com/reference/bun/ffi/FFITypeStringToType/u32): [uint32\_t](https://bun.com/reference/bun/ffi/FFIType/uint32_t)
  + [u64](https://bun.com/reference/bun/ffi/FFITypeStringToType/u64): [uint64\_t](https://bun.com/reference/bun/ffi/FFIType/uint64_t)
  + [u8](https://bun.com/reference/bun/ffi/FFITypeStringToType/u8): [uint8\_t](https://bun.com/reference/bun/ffi/FFIType/uint8_t)
  + [uint16\_t](https://bun.com/reference/bun/ffi/FFITypeStringToType/uint16_t): [uint16\_t](https://bun.com/reference/bun/ffi/FFIType/uint16_t)
  + [uint32\_t](https://bun.com/reference/bun/ffi/FFITypeStringToType/uint32_t): [uint32\_t](https://bun.com/reference/bun/ffi/FFIType/uint32_t)
  + [uint64\_t](https://bun.com/reference/bun/ffi/FFITypeStringToType/uint64_t): [uint64\_t](https://bun.com/reference/bun/ffi/FFIType/uint64_t)
  + [uint8\_t](https://bun.com/reference/bun/ffi/FFITypeStringToType/uint8_t): [uint8\_t](https://bun.com/reference/bun/ffi/FFIType/uint8_t)
  + [usize](https://bun.com/reference/bun/ffi/FFITypeStringToType/usize): [uint64\_t](https://bun.com/reference/bun/ffi/FFIType/uint64_t)
  + [void](https://bun.com/reference/bun/ffi/FFITypeStringToType/void): [void](https://bun.com/reference/bun/ffi/FFIType/void)
* ### interface [FFITypeToArgsType](https://bun.com/reference/bun/ffi/FFITypeToArgsType)

  + [0](https://bun.com/reference/bun/ffi/FFITypeToArgsType/0): number
  + [1](https://bun.com/reference/bun/ffi/FFITypeToArgsType/1): number
  + [10](https://bun.com/reference/bun/ffi/FFITypeToArgsType/10): number
  + [11](https://bun.com/reference/bun/ffi/FFITypeToArgsType/11): boolean
  + [12](https://bun.com/reference/bun/ffi/FFITypeToArgsType/12): null | TypedArray<ArrayBufferLike> | [Pointer](https://bun.com/reference/bun/ffi/Pointer) | [CString](https://bun.com/reference/bun/ffi/CString)
  + [13](https://bun.com/reference/bun/ffi/FFITypeToArgsType/13): undefined
  + [14](https://bun.com/reference/bun/ffi/FFITypeToArgsType/14): null | TypedArray<ArrayBufferLike> | [Pointer](https://bun.com/reference/bun/ffi/Pointer) | [CString](https://bun.com/reference/bun/ffi/CString)
  + [15](https://bun.com/reference/bun/ffi/FFITypeToArgsType/15): number | bigint
  + [16](https://bun.com/reference/bun/ffi/FFITypeToArgsType/16): number | bigint
  + [17](https://bun.com/reference/bun/ffi/FFITypeToArgsType/17): [Pointer](https://bun.com/reference/bun/ffi/Pointer) | [JSCallback](https://bun.com/reference/bun/ffi/JSCallback)
  + [18](https://bun.com/reference/bun/ffi/FFITypeToArgsType/18): unknown
  + [19](https://bun.com/reference/bun/ffi/FFITypeToArgsType/19): unknown
  + [2](https://bun.com/reference/bun/ffi/FFITypeToArgsType/2): number
  + [20](https://bun.com/reference/bun/ffi/FFITypeToArgsType/20): TypedArray<ArrayBufferLike> | DataView<ArrayBufferLike>
  + [3](https://bun.com/reference/bun/ffi/FFITypeToArgsType/3): number
  + [4](https://bun.com/reference/bun/ffi/FFITypeToArgsType/4): number
  + [5](https://bun.com/reference/bun/ffi/FFITypeToArgsType/5): number
  + [6](https://bun.com/reference/bun/ffi/FFITypeToArgsType/6): number
  + [7](https://bun.com/reference/bun/ffi/FFITypeToArgsType/7): number | bigint
  + [8](https://bun.com/reference/bun/ffi/FFITypeToArgsType/8): number | bigint
  + [9](https://bun.com/reference/bun/ffi/FFITypeToArgsType/9): number
* ### interface [FFITypeToReturnsType](https://bun.com/reference/bun/ffi/FFITypeToReturnsType)

  + [0](https://bun.com/reference/bun/ffi/FFITypeToReturnsType/0): number
  + [1](https://bun.com/reference/bun/ffi/FFITypeToReturnsType/1): number
  + [10](https://bun.com/reference/bun/ffi/FFITypeToReturnsType/10): number
  + [11](https://bun.com/reference/bun/ffi/FFITypeToReturnsType/11): boolean
  + [12](https://bun.com/reference/bun/ffi/FFITypeToReturnsType/12): null | [Pointer](https://bun.com/reference/bun/ffi/Pointer)
  + [13](https://bun.com/reference/bun/ffi/FFITypeToReturnsType/13): undefined
  + [14](https://bun.com/reference/bun/ffi/FFITypeToReturnsType/14): [CString](https://bun.com/reference/bun/ffi/CString)
  + [15](https://bun.com/reference/bun/ffi/FFITypeToReturnsType/15): number | bigint
  + [16](https://bun.com/reference/bun/ffi/FFITypeToReturnsType/16): number | bigint
  + [17](https://bun.com/reference/bun/ffi/FFITypeToReturnsType/17): null | [Pointer](https://bun.com/reference/bun/ffi/Pointer)
  + [18](https://bun.com/reference/bun/ffi/FFITypeToReturnsType/18): unknown
  + [19](https://bun.com/reference/bun/ffi/FFITypeToReturnsType/19): unknown
  + [2](https://bun.com/reference/bun/ffi/FFITypeToReturnsType/2): number
  + [20](https://bun.com/reference/bun/ffi/FFITypeToReturnsType/20): TypedArray<ArrayBufferLike> | DataView<ArrayBufferLike>
  + [3](https://bun.com/reference/bun/ffi/FFITypeToReturnsType/3): number
  + [4](https://bun.com/reference/bun/ffi/FFITypeToReturnsType/4): number
  + [5](https://bun.com/reference/bun/ffi/FFITypeToReturnsType/5): number
  + [6](https://bun.com/reference/bun/ffi/FFITypeToReturnsType/6): number
  + [7](https://bun.com/reference/bun/ffi/FFITypeToReturnsType/7): bigint
  + [8](https://bun.com/reference/bun/ffi/FFITypeToReturnsType/8): bigint
  + [9](https://bun.com/reference/bun/ffi/FFITypeToReturnsType/9): number
* ### interface [Library](https://bun.com/reference/bun/ffi/Library)<Fns extends [Symbols](https://bun.com/reference/bun/ffi/Symbols)>

  + [symbols](https://bun.com/reference/bun/ffi/Library/symbols): [ConvertFns](https://bun.com/reference/bun/ffi/ConvertFns)<Fns>
  + [close](https://bun.com/reference/bun/ffi/Library/close)(): void;

    `dlclose` the library, unloading the symbols and freeing allocated memory.

    Once called, the library is no longer usable.

    Calling a function from a library that has been closed is undefined behavior.
* type [ConvertFns](https://bun.com/reference/bun/ffi/ConvertFns)<Fns extends [Symbols](https://bun.com/reference/bun/ffi/Symbols)> = { [K in keyof Fns]: (...args: Fns[K]['args'] extends A ? { [K in string | number | symbol]: [FFITypeToArgsType](https://bun.com/reference/bun/ffi/FFITypeToArgsType)[[ToFFIType](https://bun.com/reference/bun/ffi/ToFFIType)<A[L<L>]>] } : [unknown] extends [Fns[K]['args']] ? [] : never) => [unknown] extends [Fns[K]['returns']] ? undefined : [FFITypeToReturnsType](https://bun.com/reference/bun/ffi/FFITypeToReturnsType)[[ToFFIType](https://bun.com/reference/bun/ffi/ToFFIType)<NonNullable<Fns[K]['returns']>>] }
* type [FFITypeOrString](https://bun.com/reference/bun/ffi/FFITypeOrString) = [FFIType](https://bun.com/reference/bun/ffi/FFIType) | keyof [FFITypeStringToType](https://bun.com/reference/bun/ffi/FFITypeStringToType)
* type [Pointer](https://bun.com/reference/bun/ffi/Pointer) = number & { \_\_pointer\_\_: null }
* type [Symbols](https://bun.com/reference/bun/ffi/Symbols) = Readonly<Record<string, [FFIFunction](https://bun.com/reference/bun/ffi/FFIFunction)>>
* type [ToFFIType](https://bun.com/reference/bun/ffi/ToFFIType)<T extends [FFITypeOrString](https://bun.com/reference/bun/ffi/FFITypeOrString)> = T extends [FFIType](https://bun.com/reference/bun/ffi/FFIType) ? T : T extends string ? [FFITypeStringToType](https://bun.com/reference/bun/ffi/FFITypeStringToType)[T] : never