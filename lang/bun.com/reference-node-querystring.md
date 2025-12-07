---
url: https://bun.com/reference/node/querystring
title: Node.js querystring module | API Reference | Bun
source_domain: bun.com
---

# Node.js querystring module | API Reference | Bun

Node.js module

# [querystring](https://bun.com/reference/node/querystring)

The `'node:querystring'` module provides utilities for parsing and formatting URL query strings. It includes `parse` and `stringify` methods.

Works in Bun

Fully implemented. 100% of Node.js's test suite passes.

* const [decode](https://bun.com/reference/node/querystring/decode): typeof [parse](https://bun.com/reference/node/querystring/parse)

  The querystring.decode() function is an alias for querystring.parse().
* const [encode](https://bun.com/reference/node/querystring/encode): typeof [stringify](https://bun.com/reference/node/querystring/stringify)

  The querystring.encode() function is an alias for querystring.stringify().
* function [escape](https://bun.com/reference/node/querystring/escape)(

  str: string

  ): string;

  The `querystring.escape()` method performs URL percent-encoding on the given `str` in a manner that is optimized for the specific requirements of URL query strings.

  The `querystring.escape()` method is used by `querystring.stringify()` and is generally not expected to be used directly. It is exported primarily to allow application code to provide a replacement percent-encoding implementation if necessary by assigning `querystring.escape` to an alternative function.
* function [parse](https://bun.com/reference/node/querystring/parse)(

  str: string,

  sep?: string,

  eq?: string,

  options?: [ParseOptions](https://bun.com/reference/node/querystring/ParseOptions)

  ): [ParsedUrlQuery](https://bun.com/reference/node/querystring/ParsedUrlQuery);

  The `querystring.parse()` method parses a URL query string (`str`) into a collection of key and value pairs.

  For example, the query string `'foo=bar&#x26;abc=xyz&#x26;abc=123'` is parsed into:

  ```
  {
    "foo": "bar",
    "abc": ["xyz", "123"]
  }
  ```

  The object returned by the `querystring.parse()` method *does not* prototypically inherit from the JavaScript `Object`. This means that typical `Object` methods such as `obj.toString()`, `obj.hasOwnProperty()`, and others are not defined and *will not work*.

  By default, percent-encoded characters within the query string will be assumed to use UTF-8 encoding. If an alternative character encoding is used, then an alternative `decodeURIComponent` option will need to be specified:

  ```
  // Assuming gbkDecodeURIComponent function already exists...

  querystring.parse('w=%D6%D0%CE%C4&#x26;foo=bar', null, null,
                    { decodeURIComponent: gbkDecodeURIComponent });
  ```

  @param str

  The URL query string to parse

  @param sep

  The substring used to delimit key and value pairs in the query string.

  @param eq

  The substring used to delimit keys and values in the query string.
* function [stringify](https://bun.com/reference/node/querystring/stringify)(

  obj?: [ParsedUrlQueryInput](https://bun.com/reference/node/querystring/ParsedUrlQueryInput),

  sep?: string,

  eq?: string,

  options?: [StringifyOptions](https://bun.com/reference/node/querystring/StringifyOptions)

  ): string;

  The `querystring.stringify()` method produces a URL query string from a given `obj` by iterating through the object's "own properties".

  It serializes the following types of values passed in `obj`: [string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type) | [number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Number_type) | [bigint](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt) | [boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type) | [string[]](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type) | [number[]](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Number_type) | [bigint[]](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt) | [boolean[]](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type) The numeric values must be finite. Any other input values will be coerced to empty strings.

  ```
  querystring.stringify({ foo: 'bar', baz: ['qux', 'quux'], corge: '' });
  // Returns 'foo=bar&#x26;baz=qux&#x26;baz=quux&#x26;corge='

  querystring.stringify({ foo: 'bar', baz: 'qux' }, ';', ':');
  // Returns 'foo:bar;baz:qux'
  ```

  By default, characters requiring percent-encoding within the query string will be encoded as UTF-8. If an alternative encoding is required, then an alternative `encodeURIComponent` option will need to be specified:

  ```
  // Assuming gbkEncodeURIComponent function already exists,

  querystring.stringify({ w: '中文', foo: 'bar' }, null, null,
                        { encodeURIComponent: gbkEncodeURIComponent });
  ```

  @param obj

  The object to serialize into a URL query string

  @param sep

  The substring used to delimit key and value pairs in the query string.

  @param eq

  . The substring used to delimit keys and values in the query string.
* function [unescape](https://bun.com/reference/node/querystring/unescape)(

  str: string

  ): string;

  The `querystring.unescape()` method performs decoding of URL percent-encoded characters on the given `str`.

  The `querystring.unescape()` method is used by `querystring.parse()` and is generally not expected to be used directly. It is exported primarily to allow application code to provide a replacement decoding implementation if necessary by assigning `querystring.unescape` to an alternative function.

  By default, the `querystring.unescape()` method will attempt to use the JavaScript built-in `decodeURIComponent()` method to decode. If that fails, a safer equivalent that does not throw on malformed URLs will be used.

## Type definitions

* ### interface [ParsedUrlQuery](https://bun.com/reference/node/querystring/ParsedUrlQuery)
* ### interface [ParsedUrlQueryInput](https://bun.com/reference/node/querystring/ParsedUrlQueryInput)
* ### interface [ParseOptions](https://bun.com/reference/node/querystring/ParseOptions)

  + [decodeURIComponent](https://bun.com/reference/node/querystring/ParseOptions/decodeURIComponent)?: (str: string) => string

    The function to use when decoding percent-encoded characters in the query string.
  + [maxKeys](https://bun.com/reference/node/querystring/ParseOptions/maxKeys)?: number

    Specifies the maximum number of keys to parse. Specify `0` to remove key counting limitations.
* ### interface [StringifyOptions](https://bun.com/reference/node/querystring/StringifyOptions)

  + [encodeURIComponent](https://bun.com/reference/node/querystring/StringifyOptions/encodeURIComponent)?: (str: string) => string

    The function to use when converting URL-unsafe characters to percent-encoding in the query string.