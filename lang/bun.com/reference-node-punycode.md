---
url: https://bun.com/reference/node/punycode
title: node:punycode module | API Reference | Bun
source_domain: bun.com
---

# node:punycode module | API Reference | Bun

Node.js module

# [node:punycode](https://bun.com/reference/node/punycode)

The `'node:punycode'` module provides utilities for converting Unicode strings to ASCII using Punycode encoding, as defined by RFC 3492. It enables safe handling of Internationalized Domain Names (IDNs).

Functions include `encode`, `decode`, `toASCII`, and `toUnicode`.

Works in Bun

Fully implemented. 100% of Node.js's test suite passes. Note: This module is deprecated by Node.js.

* function [decode](https://bun.com/reference/node/punycode/decode)(

  string: string

  ): string;

  The `punycode.decode()` method converts a [Punycode](https://tools.ietf.org/html/rfc3492) string of ASCII-only characters to the equivalent string of Unicode codepoints.

  ```
  punycode.decode('maana-pta'); // 'mañana'
  punycode.decode('--dqo34k'); // '☃-⌘'
  ```
* function [encode](https://bun.com/reference/node/punycode/encode)(

  string: string

  ): string;

  The `punycode.encode()` method converts a string of Unicode codepoints to a [Punycode](https://tools.ietf.org/html/rfc3492) string of ASCII-only characters.

  ```
  punycode.encode('mañana'); // 'maana-pta'
  punycode.encode('☃-⌘'); // '--dqo34k'
  ```
* function [toASCII](https://bun.com/reference/node/punycode/toASCII)(

  domain: string

  ): string;

  The `punycode.toASCII()` method converts a Unicode string representing an Internationalized Domain Name to [Punycode](https://tools.ietf.org/html/rfc3492). Only the non-ASCII parts of the domain name will be converted. Calling `punycode.toASCII()` on a string that already only contains ASCII characters will have no effect.

  ```
  // encode domain names
  punycode.toASCII('mañana.com');  // 'xn--maana-pta.com'
  punycode.toASCII('☃-⌘.com');   // 'xn----dqo34k.com'
  punycode.toASCII('example.com'); // 'example.com'
  ```
* function [toUnicode](https://bun.com/reference/node/punycode/toUnicode)(

  domain: string

  ): string;

  The `punycode.toUnicode()` method converts a string representing a domain name containing [Punycode](https://tools.ietf.org/html/rfc3492) encoded characters into Unicode. Only the [Punycode](https://tools.ietf.org/html/rfc3492) encoded parts of the domain name are be converted.

  ```
  // decode domain names
  punycode.toUnicode('xn--maana-pta.com'); // 'mañana.com'
  punycode.toUnicode('xn----dqo34k.com');  // '☃-⌘.com'
  punycode.toUnicode('example.com');       // 'example.com'
  ```

## Type definitions

* ### interface [ucs2](https://bun.com/reference/node/punycode/ucs2)