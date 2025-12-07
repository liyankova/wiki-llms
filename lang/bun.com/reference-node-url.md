---
url: https://bun.com/reference/node/url
title: Node.js url module | API Reference | Bun
source_domain: bun.com
---

# Node.js url module | API Reference | Bun

Node.js module

# [url](https://bun.com/reference/node/url)

The `'node:url'` module provides utilities to parse, format, and resolve URLs. It includes the `URL` and `URLSearchParams` classes that conform to the WHATWG URL specification.

Features include protocol, hostname, pathname, query string parsing, and manipulation, allowing robust URL handling in network applications.

Works in Bun

Fully implemented.

* ### class [URL](https://bun.com/reference/node/url/URL)

  Browser-compatible `URL` class, implemented by following the WHATWG URL Standard. [Examples of parsed URLs](https://url.spec.whatwg.org/#example-url-parsing) may be found in the Standard itself. The `URL` class is also available on the global object.

  In accordance with browser conventions, all properties of `URL` objects are implemented as getters and setters on the class prototype, rather than as data properties on the object itself. Thus, unlike `legacy urlObject`s, using the `delete` keyword on any properties of `URL` objects (e.g. `delete myURL.protocol`, `delete myURL.pathname`, etc) has no effect but will still return `true`.

  + [hash](https://bun.com/reference/node/url/URL/hash): string

    Gets and sets the fragment portion of the URL.

    ```
    const myURL = new URL('https://example.org/foo#bar');
    console.log(myURL.hash);
    // Prints #bar

    myURL.hash = 'baz';
    console.log(myURL.href);
    // Prints https://example.org/foo#baz
    ```

    Invalid URL characters included in the value assigned to the `hash` property are `percent-encoded`. The selection of which characters to percent-encode may vary somewhat from what the parse and format methods would produce.
  + [host](https://bun.com/reference/node/url/URL/host): string

    Gets and sets the host portion of the URL.

    ```
    const myURL = new URL('https://example.org:81/foo');
    console.log(myURL.host);
    // Prints example.org:81

    myURL.host = 'example.com:82';
    console.log(myURL.href);
    // Prints https://example.com:82/foo
    ```

    Invalid host values assigned to the `host` property are ignored.
  + [hostname](https://bun.com/reference/node/url/URL/hostname): string

    Gets and sets the host name portion of the URL. The key difference between`url.host` and `url.hostname` is that `url.hostname` does *not* include the port.

    ```
    const myURL = new URL('https://example.org:81/foo');
    console.log(myURL.hostname);
    // Prints example.org

    // Setting the hostname does not change the port
    myURL.hostname = 'example.com';
    console.log(myURL.href);
    // Prints https://example.com:81/foo

    // Use myURL.host to change the hostname and port
    myURL.host = 'example.org:82';
    console.log(myURL.href);
    // Prints https://example.org:82/foo
    ```

    Invalid host name values assigned to the `hostname` property are ignored.
  + [href](https://bun.com/reference/node/url/URL/href): string

    Gets and sets the serialized URL.

    ```
    const myURL = new URL('https://example.org/foo');
    console.log(myURL.href);
    // Prints https://example.org/foo

    myURL.href = 'https://example.com/bar';
    console.log(myURL.href);
    // Prints https://example.com/bar
    ```

    Getting the value of the `href` property is equivalent to calling toString.

    Setting the value of this property to a new value is equivalent to creating a new `URL` object using `new URL(value)`. Each of the `URL` object's properties will be modified.

    If the value assigned to the `href` property is not a valid URL, a `TypeError` will be thrown.
  + readonly [origin](https://bun.com/reference/node/url/URL/origin): string

    Gets the read-only serialization of the URL's origin.

    ```
    const myURL = new URL('https://example.org/foo/bar?baz');
    console.log(myURL.origin);
    // Prints https://example.org
    ```

    ```
    const idnURL = new URL('https://測試');
    console.log(idnURL.origin);
    // Prints https://xn--g6w251d

    console.log(idnURL.hostname);
    // Prints xn--g6w251d
    ```
  + [password](https://bun.com/reference/node/url/URL/password): string

    Gets and sets the password portion of the URL.

    ```
    const myURL = new URL('https://abc:xyz@example.com');
    console.log(myURL.password);
    // Prints xyz

    myURL.password = '123';
    console.log(myURL.href);
    // Prints https://abc:123@example.com/
    ```

    Invalid URL characters included in the value assigned to the `password` property are `percent-encoded`. The selection of which characters to percent-encode may vary somewhat from what the parse and format methods would produce.
  + [pathname](https://bun.com/reference/node/url/URL/pathname): string

    Gets and sets the path portion of the URL.

    ```
    const myURL = new URL('https://example.org/abc/xyz?123');
    console.log(myURL.pathname);
    // Prints /abc/xyz

    myURL.pathname = '/abcdef';
    console.log(myURL.href);
    // Prints https://example.org/abcdef?123
    ```

    Invalid URL characters included in the value assigned to the `pathname` property are `percent-encoded`. The selection of which characters to percent-encode may vary somewhat from what the parse and format methods would produce.
  + [port](https://bun.com/reference/node/url/URL/port): string

    Gets and sets the port portion of the URL.

    The port value may be a number or a string containing a number in the range `0` to `65535` (inclusive). Setting the value to the default port of the `URL` objects given `protocol` will result in the `port` value becoming the empty string (`''`).

    The port value can be an empty string in which case the port depends on the protocol/scheme:

    <omitted>

    Upon assigning a value to the port, the value will first be converted to a string using `.toString()`.

    If that string is invalid but it begins with a number, the leading number is assigned to `port`. If the number lies outside the range denoted above, it is ignored.

    ```
    const myURL = new URL('https://example.org:8888');
    console.log(myURL.port);
    // Prints 8888

    // Default ports are automatically transformed to the empty string
    // (HTTPS protocol's default port is 443)
    myURL.port = '443';
    console.log(myURL.port);
    // Prints the empty string
    console.log(myURL.href);
    // Prints https://example.org/

    myURL.port = 1234;
    console.log(myURL.port);
    // Prints 1234
    console.log(myURL.href);
    // Prints https://example.org:1234/

    // Completely invalid port strings are ignored
    myURL.port = 'abcd';
    console.log(myURL.port);
    // Prints 1234

    // Leading numbers are treated as a port number
    myURL.port = '5678abcd';
    console.log(myURL.port);
    // Prints 5678

    // Non-integers are truncated
    myURL.port = 1234.5678;
    console.log(myURL.port);
    // Prints 1234

    // Out-of-range numbers which are not represented in scientific notation
    // will be ignored.
    myURL.port = 1e10; // 10000000000, will be range-checked as described below
    console.log(myURL.port);
    // Prints 1234
    ```

    Numbers which contain a decimal point, such as floating-point numbers or numbers in scientific notation, are not an exception to this rule. Leading numbers up to the decimal point will be set as the URL's port, assuming they are valid:

    ```
    myURL.port = 4.567e21;
    console.log(myURL.port);
    // Prints 4 (because it is the leading number in the string '4.567e21')
    ```
  + [search](https://bun.com/reference/node/url/URL/search): string

    Gets and sets the serialized query portion of the URL.

    ```
    const myURL = new URL('https://example.org/abc?123');
    console.log(myURL.search);
    // Prints ?123

    myURL.search = 'abc=xyz';
    console.log(myURL.href);
    // Prints https://example.org/abc?abc=xyz
    ```

    Any invalid URL characters appearing in the value assigned the `search` property will be `percent-encoded`. The selection of which characters to percent-encode may vary somewhat from what the parse and format methods would produce.
  + readonly [searchParams](https://bun.com/reference/node/url/URL/searchParams): [URLSearchParams](https://bun.com/reference/node/url/URLSearchParams)

    Gets the `URLSearchParams` object representing the query parameters of the URL. This property is read-only but the `URLSearchParams` object it provides can be used to mutate the URL instance; to replace the entirety of query parameters of the URL, use the search setter. See `URLSearchParams` documentation for details.

    Use care when using `.searchParams` to modify the `URL` because, per the WHATWG specification, the `URLSearchParams` object uses different rules to determine which characters to percent-encode. For instance, the `URL` object will not percent encode the ASCII tilde (`~`) character, while `URLSearchParams` will always encode it:

    ```
    const myURL = new URL('https://example.org/abc?foo=~bar');

    console.log(myURL.search);  // prints ?foo=~bar

    // Modify the URL via searchParams...
    myURL.searchParams.sort();

    console.log(myURL.search);  // prints ?foo=%7Ebar
    ```
  + [username](https://bun.com/reference/node/url/URL/username): string

    Gets and sets the username portion of the URL.

    ```
    const myURL = new URL('https://abc:xyz@example.com');
    console.log(myURL.username);
    // Prints abc

    myURL.username = '123';
    console.log(myURL.href);
    // Prints https://123:xyz@example.com/
    ```

    Any invalid URL characters appearing in the value assigned the `username` property will be `percent-encoded`. The selection of which characters to percent-encode may vary somewhat from what the parse and format methods would produce.
  + [toJSON](https://bun.com/reference/node/url/URL/toJSON)(): string;

    The `toJSON()` method on the `URL` object returns the serialized URL. The value returned is equivalent to that of href and toString.

    This method is automatically called when an `URL` object is serialized with [`JSON.stringify()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify).

    ```
    const myURLs = [
      new URL('https://www.example.com'),
      new URL('https://test.example.org'),
    ];
    console.log(JSON.stringify(myURLs));
    // Prints ["https://www.example.com/","https://test.example.org/"]
    ```
  + [toString](https://bun.com/reference/node/url/URL/toString)(): string;

    The `toString()` method on the `URL` object returns the serialized URL. The value returned is equivalent to that of href and toJSON.
  + static [canParse](https://bun.com/reference/node/url/URL/canParse)(

    input: string,

    base?: string

    ): boolean;

    Checks if an `input` relative to the `base` can be parsed to a `URL`.

    ```
    const isValid = URL.canParse('/foo', 'https://example.org/'); // true

    const isNotValid = URL.canParse('/foo'); // false
    ```

    @param input

    The absolute or relative input URL to parse. If `input` is relative, then `base` is required. If `input` is absolute, the `base` is ignored. If `input` is not a string, it is `converted to a string` first.

    @param base

    The base URL to resolve against if the `input` is not absolute. If `base` is not a string, it is `converted to a string` first.
  + static [createObjectURL](https://bun.com/reference/node/url/URL/createObjectURL)(

    blob: [Blob](https://bun.com/reference/node/buffer/Blob)

    ): string;

    Creates a `'blob:nodedata:...'` URL string that represents the given `Blob` object and can be used to retrieve the `Blob` later.

    ```
    import {
      Blob,
      resolveObjectURL,
    } from 'node:buffer';

    const blob = new Blob(['hello']);
    const id = URL.createObjectURL(blob);

    // later...

    const otherBlob = resolveObjectURL(id);
    console.log(otherBlob.size);
    ```

    The data stored by the registered `Blob` will be retained in memory until `URL.revokeObjectURL()` is called to remove it.

    `Blob` objects are registered within the current thread. If using Worker Threads, `Blob` objects registered within one Worker will not be available to other workers or the main thread.
  + static [parse](https://bun.com/reference/node/url/URL/parse)(

    input: string,

    base?: string

    ): null | [URL](https://bun.com/reference/node/url/URL);

    Parses a string as a URL. If `base` is provided, it will be used as the base URL for the purpose of resolving non-absolute `input` URLs. Returns `null` if the parameters can't be resolved to a valid URL.

    @param input

    The absolute or relative input URL to parse. If `input` is relative, then `base` is required. If `input` is absolute, the `base` is ignored. If `input` is not a string, it is [converted to a string](https://tc39.es/ecma262/#sec-tostring) first.

    @param base

    The base URL to resolve against if the `input` is not absolute. If `base` is not a string, it is [converted to a string](https://tc39.es/ecma262/#sec-tostring) first.
  + static [revokeObjectURL](https://bun.com/reference/node/url/URL/revokeObjectURL)(

    id: string

    ): void;

    Removes the stored `Blob` identified by the given ID. Attempting to revoke a ID that isn't registered will silently fail.

    @param id

    A `'blob:nodedata:...` URL string returned by a prior call to `URL.createObjectURL()`.
* ### class [URLPattern](https://bun.com/reference/node/url/URLPattern)

  + readonly [hash](https://bun.com/reference/node/url/URLPattern/hash): string
  + readonly [hasRegExpGroups](https://bun.com/reference/node/url/URLPattern/hasRegExpGroups): boolean
  + readonly [hostname](https://bun.com/reference/node/url/URLPattern/hostname): string
  + readonly [password](https://bun.com/reference/node/url/URLPattern/password): string
  + readonly [pathname](https://bun.com/reference/node/url/URLPattern/pathname): string
  + readonly [port](https://bun.com/reference/node/url/URLPattern/port): string
  + readonly [search](https://bun.com/reference/node/url/URLPattern/search): string
  + readonly [username](https://bun.com/reference/node/url/URLPattern/username): string
  + [exec](https://bun.com/reference/node/url/URLPattern/exec)(

    input?: string | [URLPatternInit](https://bun.com/reference/node/url/URLPatternInit),

    baseURL?: string

    ): null | [URLPatternResult](https://bun.com/reference/node/url/URLPatternResult);
  + [test](https://bun.com/reference/node/url/URLPattern/test)(

    input?: string | [URLPatternInit](https://bun.com/reference/node/url/URLPatternInit),

    baseURL?: string

    ): boolean;
* ### class [URLSearchParams](https://bun.com/reference/node/url/URLSearchParams)

  The `URLSearchParams` API provides read and write access to the query of a `URL`. The `URLSearchParams` class can also be used standalone with one of the four following constructors. The `URLSearchParams` class is also available on the global object.

  The WHATWG `URLSearchParams` interface and the `querystring` module have similar purpose, but the purpose of the `querystring` module is more general, as it allows the customization of delimiter characters (`&#x26;` and `=`). On the other hand, this API is designed purely for URL query strings.

  ```
  const myURL = new URL('https://example.org/?abc=123');
  console.log(myURL.searchParams.get('abc'));
  // Prints 123

  myURL.searchParams.append('abc', 'xyz');
  console.log(myURL.href);
  // Prints https://example.org/?abc=123&#x26;abc=xyz

  myURL.searchParams.delete('abc');
  myURL.searchParams.set('a', 'b');
  console.log(myURL.href);
  // Prints https://example.org/?a=b

  const newSearchParams = new URLSearchParams(myURL.searchParams);
  // The above is equivalent to
  // const newSearchParams = new URLSearchParams(myURL.search);

  newSearchParams.append('a', 'c');
  console.log(myURL.href);
  // Prints https://example.org/?a=b
  console.log(newSearchParams.toString());
  // Prints a=b&#x26;a=c

  // newSearchParams.toString() is implicitly called
  myURL.search = newSearchParams;
  console.log(myURL.href);
  // Prints https://example.org/?a=b&#x26;a=c
  newSearchParams.delete('a');
  console.log(myURL.href);
  // Prints https://example.org/?a=b&#x26;a=c
  ```

  + readonly [size](https://bun.com/reference/node/url/URLSearchParams/size): number

    The total number of parameter entries.
  + [[Symbol.iterator]](https://bun.com/reference/node/url/URLSearchParams/[iterator])(): [URLSearchParamsIterator](https://bun.com/reference/node/url/URLSearchParamsIterator)<[string, string]>;
  + [append](https://bun.com/reference/node/url/URLSearchParams/append)(

    name: string,

    value: string

    ): void;

    Append a new name-value pair to the query string.
  + [delete](https://bun.com/reference/node/url/URLSearchParams/delete)(

    name: string,

    value?: string

    ): void;

    If `value` is provided, removes all name-value pairs where name is `name` and value is `value`.

    If `value` is not provided, removes all name-value pairs whose name is `name`.
  + [entries](https://bun.com/reference/node/url/URLSearchParams/entries)(): [URLSearchParamsIterator](https://bun.com/reference/node/url/URLSearchParamsIterator)<[string, string]>;

    Returns an ES6 `Iterator` over each of the name-value pairs in the query. Each item of the iterator is a JavaScript `Array`. The first item of the `Array` is the `name`, the second item of the `Array` is the `value`.

    Alias for `urlSearchParams[Symbol.iterator]()`.
  + [forEach](https://bun.com/reference/node/url/URLSearchParams/forEach)<TThis = [URLSearchParams](https://bun.com/reference/node/url/URLSearchParams)>(

    fn: (this: TThis, value: string, name: string, searchParams: [URLSearchParams](https://bun.com/reference/node/url/URLSearchParams)) => void,

    thisArg?: TThis

    ): void;

    Iterates over each name-value pair in the query and invokes the given function.

    ```
    const myURL = new URL('https://example.org/?a=b&#x26;c=d');
    myURL.searchParams.forEach((value, name, searchParams) => {
      console.log(name, value, myURL.searchParams === searchParams);
    });
    // Prints:
    //   a b true
    //   c d true
    ```

    @param fn

    Invoked for each name-value pair in the query

    @param thisArg

    To be used as `this` value for when `fn` is called
  + [get](https://bun.com/reference/node/url/URLSearchParams/get)(

    name: string

    ): null | string;

    Returns the value of the first name-value pair whose name is `name`. If there are no such pairs, `null` is returned.

    @returns

    or `null` if there is no name-value pair with the given `name`.
  + [getAll](https://bun.com/reference/node/url/URLSearchParams/getAll)(

    name: string

    ): string[];

    Returns the values of all name-value pairs whose name is `name`. If there are no such pairs, an empty array is returned.
  + [has](https://bun.com/reference/node/url/URLSearchParams/has)(

    name: string,

    value?: string

    ): boolean;

    Checks if the `URLSearchParams` object contains key-value pair(s) based on `name` and an optional `value` argument.

    If `value` is provided, returns `true` when name-value pair with same `name` and `value` exists.

    If `value` is not provided, returns `true` if there is at least one name-value pair whose name is `name`.
  + [keys](https://bun.com/reference/node/url/URLSearchParams/keys)(): [URLSearchParamsIterator](https://bun.com/reference/node/url/URLSearchParamsIterator)<string>;

    Returns an ES6 `Iterator` over the names of each name-value pair.

    ```
    const params = new URLSearchParams('foo=bar&#x26;foo=baz');
    for (const name of params.keys()) {
      console.log(name);
    }
    // Prints:
    //   foo
    //   foo
    ```
  + [set](https://bun.com/reference/node/url/URLSearchParams/set)(

    name: string,

    value: string

    ): void;

    Sets the value in the `URLSearchParams` object associated with `name` to `value`. If there are any pre-existing name-value pairs whose names are `name`, set the first such pair's value to `value` and remove all others. If not, append the name-value pair to the query string.

    ```
    const params = new URLSearchParams();
    params.append('foo', 'bar');
    params.append('foo', 'baz');
    params.append('abc', 'def');
    console.log(params.toString());
    // Prints foo=bar&#x26;foo=baz&#x26;abc=def

    params.set('foo', 'def');
    params.set('xyz', 'opq');
    console.log(params.toString());
    // Prints foo=def&#x26;abc=def&#x26;xyz=opq
    ```
  + [sort](https://bun.com/reference/node/url/URLSearchParams/sort)(): void;

    Sort all existing name-value pairs in-place by their names. Sorting is done with a [stable sorting algorithm](https://en.wikipedia.org/wiki/Sorting_algorithm#Stability), so relative order between name-value pairs with the same name is preserved.

    This method can be used, in particular, to increase cache hits.

    ```
    const params = new URLSearchParams('query[]=abc&#x26;type=search&#x26;query[]=123');
    params.sort();
    console.log(params.toString());
    // Prints query%5B%5D=abc&#x26;query%5B%5D=123&#x26;type=search
    ```
  + [toJSON](https://bun.com/reference/node/url/URLSearchParams/toJSON)(): Record<string, string>;
  + [toString](https://bun.com/reference/node/url/URLSearchParams/toString)(): string;

    Returns the search parameters serialized as a string, with characters percent-encoded where necessary.
  + [values](https://bun.com/reference/node/url/URLSearchParams/values)(): [URLSearchParamsIterator](https://bun.com/reference/node/url/URLSearchParamsIterator)<string>;

    Returns an ES6 `Iterator` over the values of each name-value pair.
* function [domainToASCII](https://bun.com/reference/node/url/domainToASCII)(

  domain: string

  ): string;

  Returns the [Punycode](https://tools.ietf.org/html/rfc5891#section-4.4) ASCII serialization of the `domain`. If `domain` is an invalid domain, the empty string is returned.

  It performs the inverse operation to domainToUnicode.

  ```
  import url from 'node:url';

  console.log(url.domainToASCII('español.com'));
  // Prints xn--espaol-zwa.com
  console.log(url.domainToASCII('中文.com'));
  // Prints xn--fiq228c.com
  console.log(url.domainToASCII('xn--iñvalid.com'));
  // Prints an empty string
  ```
* function [domainToUnicode](https://bun.com/reference/node/url/domainToUnicode)(

  domain: string

  ): string;

  Returns the Unicode serialization of the `domain`. If `domain` is an invalid domain, the empty string is returned.

  It performs the inverse operation to domainToASCII.

  ```
  import url from 'node:url';

  console.log(url.domainToUnicode('xn--espaol-zwa.com'));
  // Prints español.com
  console.log(url.domainToUnicode('xn--fiq228c.com'));
  // Prints 中文.com
  console.log(url.domainToUnicode('xn--iñvalid.com'));
  // Prints an empty string
  ```
* function [fileURLToPath](https://bun.com/reference/node/url/fileURLToPath)(

  url: string | [URL](https://bun.com/reference/node/url/URL),

  options?: [FileUrlToPathOptions](https://bun.com/reference/node/url/FileUrlToPathOptions)

  ): string;

  This function ensures the correct decodings of percent-encoded characters as well as ensuring a cross-platform valid absolute path string.

  ```
  import { fileURLToPath } from 'node:url';

  const __filename = fileURLToPath(import.meta.url);

  new URL('file:///C:/path/').pathname;      // Incorrect: /C:/path/
  fileURLToPath('file:///C:/path/');         // Correct:   C:\path\ (Windows)

  new URL('file://nas/foo.txt').pathname;    // Incorrect: /foo.txt
  fileURLToPath('file://nas/foo.txt');       // Correct:   \\nas\foo.txt (Windows)

  new URL('file:///你好.txt').pathname;      // Incorrect: /%E4%BD%A0%E5%A5%BD.txt
  fileURLToPath('file:///你好.txt');         // Correct:   /你好.txt (POSIX)

  new URL('file:///hello world').pathname;   // Incorrect: /hello%20world
  fileURLToPath('file:///hello world');      // Correct:   /hello world (POSIX)
  ```

  @param url

  The file URL string or URL object to convert to a path.

  @returns

  The fully-resolved platform-specific Node.js file path.
* function [fileURLToPathBuffer](https://bun.com/reference/node/url/fileURLToPathBuffer)(

  url: string | [URL](https://bun.com/reference/node/url/URL),

  options?: [FileUrlToPathOptions](https://bun.com/reference/node/url/FileUrlToPathOptions)

  ): NonSharedBuffer;

  Like `url.fileURLToPath(...)` except that instead of returning a string representation of the path, a `Buffer` is returned. This conversion is helpful when the input URL contains percent-encoded segments that are not valid UTF-8 / Unicode sequences.

  @param url

  The file URL string or URL object to convert to a path.

  @returns

  The fully-resolved platform-specific Node.js file path as a `Buffer`.
* function [format](https://bun.com/reference/node/url/format)(

  urlObject: [URL](https://bun.com/reference/node/url/URL),

  options?: [URLFormatOptions](https://bun.com/reference/node/url/URLFormatOptions)

  ): string;

  The `url.format()` method returns a formatted URL string derived from `urlObject`.

  ```
  import url from 'node:url';
  url.format({
    protocol: 'https',
    hostname: 'example.com',
    pathname: '/some/path',
    query: {
      page: 1,
      format: 'json',
    },
  });

  // => 'https://example.com/some/path?page=1&#x26;format=json'
  ```

  If `urlObject` is not an object or a string, `url.format()` will throw a `TypeError`.

  The formatting process operates as follows:

  + A new empty string `result` is created.
  + If `urlObject.protocol` is a string, it is appended as-is to `result`.
  + Otherwise, if `urlObject.protocol` is not `undefined` and is not a string, an `Error` is thrown.
  + For all string values of `urlObject.protocol` that *do not end* with an ASCII colon (`:`) character, the literal string `:` will be appended to `result`.
  + If either of the following conditions is true, then the literal string `//` will be appended to `result`:
    - `urlObject.slashes` property is true;
    - `urlObject.protocol` begins with `http`, `https`, `ftp`, `gopher`, or `file`;
  + If the value of the `urlObject.auth` property is truthy, and either `urlObject.host` or `urlObject.hostname` are not `undefined`, the value of `urlObject.auth` will be coerced into a string and appended to `result` followed by the literal string `@`.
  + If the `urlObject.host` property is `undefined` then:
    - If the `urlObject.hostname` is a string, it is appended to `result`.
    - Otherwise, if `urlObject.hostname` is not `undefined` and is not a string, an `Error` is thrown.
    - If the `urlObject.port` property value is truthy, and `urlObject.hostname` is not `undefined`: \* The literal string `:` is appended to `result`, and \* The value of `urlObject.port` is coerced to a string and appended to `result`.
  + Otherwise, if the `urlObject.host` property value is truthy, the value of `urlObject.host` is coerced to a string and appended to `result`.
  + If the `urlObject.pathname` property is a string that is not an empty string:
    - If the `urlObject.pathname` *does not start* with an ASCII forward slash (`/`), then the literal string `'/'` is appended to `result`.
    - The value of `urlObject.pathname` is appended to `result`.
  + Otherwise, if `urlObject.pathname` is not `undefined` and is not a string, an `Error` is thrown.
  + If the `urlObject.search` property is `undefined` and if the `urlObject.query`property is an `Object`, the literal string `?` is appended to `result` followed by the output of calling the `querystring` module's `stringify()` method passing the value of `urlObject.query`.
  + Otherwise, if `urlObject.search` is a string:
    - If the value of `urlObject.search` *does not start* with the ASCII question mark (`?`) character, the literal string `?` is appended to `result`.
    - The value of `urlObject.search` is appended to `result`.
  + Otherwise, if `urlObject.search` is not `undefined` and is not a string, an `Error` is thrown.
  + If the `urlObject.hash` property is a string:
    - If the value of `urlObject.hash` *does not start* with the ASCII hash (`#`) character, the literal string `#` is appended to `result`.
    - The value of `urlObject.hash` is appended to `result`.
  + Otherwise, if the `urlObject.hash` property is not `undefined` and is not a string, an `Error` is thrown.
  + `result` is returned.

  @param urlObject

  A URL object (as returned by `url.parse()` or constructed otherwise). If a string, it is converted to an object by passing it to `url.parse()`.

  function [format](https://bun.com/reference/node/url/format)(

  urlObject: string | [UrlObject](https://bun.com/reference/node/url/UrlObject)

  ): string;

  The `url.format()` method returns a formatted URL string derived from `urlObject`.

  ```
  import url from 'node:url';
  url.format({
    protocol: 'https',
    hostname: 'example.com',
    pathname: '/some/path',
    query: {
      page: 1,
      format: 'json',
    },
  });

  // => 'https://example.com/some/path?page=1&#x26;format=json'
  ```

  If `urlObject` is not an object or a string, `url.format()` will throw a `TypeError`.

  The formatting process operates as follows:

  + A new empty string `result` is created.
  + If `urlObject.protocol` is a string, it is appended as-is to `result`.
  + Otherwise, if `urlObject.protocol` is not `undefined` and is not a string, an `Error` is thrown.
  + For all string values of `urlObject.protocol` that *do not end* with an ASCII colon (`:`) character, the literal string `:` will be appended to `result`.
  + If either of the following conditions is true, then the literal string `//` will be appended to `result`:
    - `urlObject.slashes` property is true;
    - `urlObject.protocol` begins with `http`, `https`, `ftp`, `gopher`, or `file`;
  + If the value of the `urlObject.auth` property is truthy, and either `urlObject.host` or `urlObject.hostname` are not `undefined`, the value of `urlObject.auth` will be coerced into a string and appended to `result` followed by the literal string `@`.
  + If the `urlObject.host` property is `undefined` then:
    - If the `urlObject.hostname` is a string, it is appended to `result`.
    - Otherwise, if `urlObject.hostname` is not `undefined` and is not a string, an `Error` is thrown.
    - If the `urlObject.port` property value is truthy, and `urlObject.hostname` is not `undefined`: \* The literal string `:` is appended to `result`, and \* The value of `urlObject.port` is coerced to a string and appended to `result`.
  + Otherwise, if the `urlObject.host` property value is truthy, the value of `urlObject.host` is coerced to a string and appended to `result`.
  + If the `urlObject.pathname` property is a string that is not an empty string:
    - If the `urlObject.pathname` *does not start* with an ASCII forward slash (`/`), then the literal string `'/'` is appended to `result`.
    - The value of `urlObject.pathname` is appended to `result`.
  + Otherwise, if `urlObject.pathname` is not `undefined` and is not a string, an `Error` is thrown.
  + If the `urlObject.search` property is `undefined` and if the `urlObject.query`property is an `Object`, the literal string `?` is appended to `result` followed by the output of calling the `querystring` module's `stringify()` method passing the value of `urlObject.query`.
  + Otherwise, if `urlObject.search` is a string:
    - If the value of `urlObject.search` *does not start* with the ASCII question mark (`?`) character, the literal string `?` is appended to `result`.
    - The value of `urlObject.search` is appended to `result`.
  + Otherwise, if `urlObject.search` is not `undefined` and is not a string, an `Error` is thrown.
  + If the `urlObject.hash` property is a string:
    - If the value of `urlObject.hash` *does not start* with the ASCII hash (`#`) character, the literal string `#` is appended to `result`.
    - The value of `urlObject.hash` is appended to `result`.
  + Otherwise, if the `urlObject.hash` property is not `undefined` and is not a string, an `Error` is thrown.
  + `result` is returned.

  @param urlObject

  A URL object (as returned by `url.parse()` or constructed otherwise). If a string, it is converted to an object by passing it to `url.parse()`.
* function [pathToFileURL](https://bun.com/reference/node/url/pathToFileURL)(

  path: string,

  options?: [PathToFileUrlOptions](https://bun.com/reference/node/url/PathToFileUrlOptions)

  ): [URL](https://bun.com/reference/node/url/URL);

  This function ensures that `path` is resolved absolutely, and that the URL control characters are correctly encoded when converting into a File URL.

  ```
  import { pathToFileURL } from 'node:url';

  new URL('/foo#1', 'file:');           // Incorrect: file:///foo#1
  pathToFileURL('/foo#1');              // Correct:   file:///foo%231 (POSIX)

  new URL('/some/path%.c', 'file:');    // Incorrect: file:///some/path%.c
  pathToFileURL('/some/path%.c');       // Correct:   file:///some/path%25.c (POSIX)
  ```

  @param path

  The path to convert to a File URL.

  @returns

  The file URL object.
* function [resolve](https://bun.com/reference/node/url/resolve)(

  from: string,

  to: string

  ): string;

  The `url.resolve()` method resolves a target URL relative to a base URL in a manner similar to that of a web browser resolving an anchor tag.

  ```
  import url from 'node:url';
  url.resolve('/one/two/three', 'four');         // '/one/two/four'
  url.resolve('http://example.com/', '/one');    // 'http://example.com/one'
  url.resolve('http://example.com/one', '/two'); // 'http://example.com/two'
  ```

  To achieve the same result using the WHATWG URL API:

  ```
  function resolve(from, to) {
    const resolvedUrl = new URL(to, new URL(from, 'resolve://'));
    if (resolvedUrl.protocol === 'resolve:') {
      // `from` is a relative URL.
      const { pathname, search, hash } = resolvedUrl;
      return pathname + search + hash;
    }
    return resolvedUrl.toString();
  }

  resolve('/one/two/three', 'four');         // '/one/two/four'
  resolve('http://example.com/', '/one');    // 'http://example.com/one'
  resolve('http://example.com/one', '/two'); // 'http://example.com/two'
  ```

  @param from

  The base URL to use if `to` is a relative URL.

  @param to

  The target URL to resolve.
* function [urlToHttpOptions](https://bun.com/reference/node/url/urlToHttpOptions)(

  url: [URL](https://bun.com/reference/node/url/URL)

  ): [ClientRequestArgs](https://bun.com/reference/node/http/ClientRequestArgs);

  This utility function converts a URL object into an ordinary options object as expected by the `http.request()` and `https.request()` APIs.

  ```
  import { urlToHttpOptions } from 'node:url';
  const myURL = new URL('https://a:b@測試?abc#foo');

  console.log(urlToHttpOptions(myURL));
  /*
  {
    protocol: 'https:',
    hostname: 'xn--g6w251d',
    hash: '#foo',
    search: '?abc',
    pathname: '/',
    path: '/?abc',
    href: 'https://a:b@xn--g6w251d/?abc#foo',
    auth: 'a:b'
  }
  ```

  @param url

  The `WHATWG URL` object to convert to an options object.

  @returns

  Options object

## Type definitions

* ### interface [FileUrlToPathOptions](https://bun.com/reference/node/url/FileUrlToPathOptions)

  + [windows](https://bun.com/reference/node/url/FileUrlToPathOptions/windows)?: boolean

    `true` if the `path` should be return as a windows filepath, `false` for posix, and `undefined` for the system default.
* ### interface [PathToFileUrlOptions](https://bun.com/reference/node/url/PathToFileUrlOptions)

  + [windows](https://bun.com/reference/node/url/PathToFileUrlOptions/windows)?: boolean

    `true` if the `path` should be return as a windows filepath, `false` for posix, and `undefined` for the system default.
* ### interface [Url](https://bun.com/reference/node/url/Url)

  + [auth](https://bun.com/reference/node/url/Url/auth): null | string
  + [hash](https://bun.com/reference/node/url/Url/hash): null | string
  + [host](https://bun.com/reference/node/url/Url/host): null | string
  + [hostname](https://bun.com/reference/node/url/Url/hostname): null | string
  + [href](https://bun.com/reference/node/url/Url/href): string
  + [path](https://bun.com/reference/node/url/Url/path): null | string
  + [pathname](https://bun.com/reference/node/url/Url/pathname): null | string
  + [port](https://bun.com/reference/node/url/Url/port): null | string
  + [query](https://bun.com/reference/node/url/Url/query): null | string | [ParsedUrlQuery](https://bun.com/reference/node/querystring/ParsedUrlQuery)
  + [search](https://bun.com/reference/node/url/Url/search): null | string
  + [slashes](https://bun.com/reference/node/url/Url/slashes): null | boolean
* ### interface [URLFormatOptions](https://bun.com/reference/node/url/URLFormatOptions)

  + [auth](https://bun.com/reference/node/url/URLFormatOptions/auth)?: boolean

    `true` if the serialized URL string should include the username and password, `false` otherwise.
  + [fragment](https://bun.com/reference/node/url/URLFormatOptions/fragment)?: boolean

    `true` if the serialized URL string should include the fragment, `false` otherwise.
  + [search](https://bun.com/reference/node/url/URLFormatOptions/search)?: boolean

    `true` if the serialized URL string should include the search query, `false` otherwise.
  + [unicode](https://bun.com/reference/node/url/URLFormatOptions/unicode)?: boolean

    `true` if Unicode characters appearing in the host component of the URL string should be encoded directly as opposed to being Punycode encoded.
* ### interface [UrlObject](https://bun.com/reference/node/url/UrlObject)

  + [auth](https://bun.com/reference/node/url/UrlObject/auth)?: null | string
  + [hash](https://bun.com/reference/node/url/UrlObject/hash)?: null | string
  + [host](https://bun.com/reference/node/url/UrlObject/host)?: null | string
  + [hostname](https://bun.com/reference/node/url/UrlObject/hostname)?: null | string
  + [href](https://bun.com/reference/node/url/UrlObject/href)?: null | string
  + [pathname](https://bun.com/reference/node/url/UrlObject/pathname)?: null | string
  + [port](https://bun.com/reference/node/url/UrlObject/port)?: null | string | number
  + [query](https://bun.com/reference/node/url/UrlObject/query)?: null | string | [ParsedUrlQueryInput](https://bun.com/reference/node/querystring/ParsedUrlQueryInput)
  + [search](https://bun.com/reference/node/url/UrlObject/search)?: null | string
  + [slashes](https://bun.com/reference/node/url/UrlObject/slashes)?: null | boolean
* ### interface [URLPatternComponentResult](https://bun.com/reference/node/url/URLPatternComponentResult)

  + [groups](https://bun.com/reference/node/url/URLPatternComponentResult/groups): Record<string, undefined | string>
  + [input](https://bun.com/reference/node/url/URLPatternComponentResult/input): string
* ### interface [URLPatternInit](https://bun.com/reference/node/url/URLPatternInit)

  + [baseURL](https://bun.com/reference/node/url/URLPatternInit/baseURL)?: string
  + [hash](https://bun.com/reference/node/url/URLPatternInit/hash)?: string
  + [hostname](https://bun.com/reference/node/url/URLPatternInit/hostname)?: string
  + [password](https://bun.com/reference/node/url/URLPatternInit/password)?: string
  + [pathname](https://bun.com/reference/node/url/URLPatternInit/pathname)?: string
  + [port](https://bun.com/reference/node/url/URLPatternInit/port)?: string
  + [search](https://bun.com/reference/node/url/URLPatternInit/search)?: string
  + [username](https://bun.com/reference/node/url/URLPatternInit/username)?: string
* ### interface [URLPatternOptions](https://bun.com/reference/node/url/URLPatternOptions)

  + [ignoreCase](https://bun.com/reference/node/url/URLPatternOptions/ignoreCase)?: boolean
* ### interface [URLPatternResult](https://bun.com/reference/node/url/URLPatternResult)

  + [hash](https://bun.com/reference/node/url/URLPatternResult/hash): [URLPatternComponentResult](https://bun.com/reference/node/url/URLPatternComponentResult)
  + [hostname](https://bun.com/reference/node/url/URLPatternResult/hostname): [URLPatternComponentResult](https://bun.com/reference/node/url/URLPatternComponentResult)
  + [inputs](https://bun.com/reference/node/url/URLPatternResult/inputs): string | [URLPatternInit](https://bun.com/reference/node/url/URLPatternInit)[]
  + [password](https://bun.com/reference/node/url/URLPatternResult/password): [URLPatternComponentResult](https://bun.com/reference/node/url/URLPatternComponentResult)
  + [pathname](https://bun.com/reference/node/url/URLPatternResult/pathname): [URLPatternComponentResult](https://bun.com/reference/node/url/URLPatternComponentResult)
  + [port](https://bun.com/reference/node/url/URLPatternResult/port): [URLPatternComponentResult](https://bun.com/reference/node/url/URLPatternComponentResult)
  + [search](https://bun.com/reference/node/url/URLPatternResult/search): [URLPatternComponentResult](https://bun.com/reference/node/url/URLPatternComponentResult)
  + [username](https://bun.com/reference/node/url/URLPatternResult/username): [URLPatternComponentResult](https://bun.com/reference/node/url/URLPatternComponentResult)
* ### interface [URLSearchParamsIterator](https://bun.com/reference/node/url/URLSearchParamsIterator)<T>

  + readonly [[Symbol.toStringTag]](https://bun.com/reference/node/url/URLSearchParamsIterator/[toStringTag]): string
  + [[Symbol.dispose]](https://bun.com/reference/node/url/URLSearchParamsIterator/[dispose])(): void;
  + [[Symbol.iterator]](https://bun.com/reference/node/url/URLSearchParamsIterator/[iterator])(): [URLSearchParamsIterator](https://bun.com/reference/node/url/URLSearchParamsIterator)<T>;
  + [drop](https://bun.com/reference/node/url/URLSearchParamsIterator/drop)(

    count: number

    ): IteratorObject<T, undefined, unknown>;

    Creates an iterator whose values are the values from this iterator after skipping the provided count.

    @param count

    The number of values to drop.
  + [every](https://bun.com/reference/node/url/URLSearchParamsIterator/every)(

    predicate: (value: T, index: number) => unknown

    ): boolean;

    Determines whether all the members of this iterator satisfy the specified test.

    @param predicate

    A function that accepts up to two arguments. The every method calls the predicate function for each element in this iterator until the predicate returns false, or until the end of this iterator.
  + [filter](https://bun.com/reference/node/url/URLSearchParamsIterator/filter)<S>(

    predicate: (value: T, index: number) => value is S

    ): IteratorObject<S, undefined, unknown>;

    Creates an iterator whose values are those from this iterator for which the provided predicate returns true.

    @param predicate

    A function that accepts up to two arguments to be used to test values from the underlying iterator.

    [filter](https://bun.com/reference/node/url/URLSearchParamsIterator/filter)(

    predicate: (value: T, index: number) => unknown

    ): IteratorObject<T, undefined, unknown>;

    Creates an iterator whose values are those from this iterator for which the provided predicate returns true.

    @param predicate

    A function that accepts up to two arguments to be used to test values from the underlying iterator.
  + [find](https://bun.com/reference/node/url/URLSearchParamsIterator/find)<S>(

    predicate: (value: T, index: number) => value is S

    ): undefined | S;

    Returns the value of the first element in this iterator where predicate is true, and undefined otherwise.

    @param predicate

    find calls predicate once for each element of this iterator, in order, until it finds one where predicate returns true. If such an element is found, find immediately returns that element value. Otherwise, find returns undefined.

    [find](https://bun.com/reference/node/url/URLSearchParamsIterator/find)(

    predicate: (value: T, index: number) => unknown

    ): undefined | T;
  + [flatMap](https://bun.com/reference/node/url/URLSearchParamsIterator/flatMap)<U>(

    callback: (value: T, index: number) => Iterator<U, unknown, undefined> | Iterable<U, unknown, undefined>

    ): IteratorObject<U, undefined, unknown>;

    Creates an iterator whose values are the result of applying the callback to the values from this iterator and then flattening the resulting iterators or iterables.

    @param callback

    A function that accepts up to two arguments to be used to transform values from the underlying iterator into new iterators or iterables to be flattened into the result.
  + [forEach](https://bun.com/reference/node/url/URLSearchParamsIterator/forEach)(

    callbackfn: (value: T, index: number) => void

    ): void;

    Performs the specified action for each element in the iterator.

    @param callbackfn

    A function that accepts up to two arguments. forEach calls the callbackfn function one time for each element in the iterator.
  + [map](https://bun.com/reference/node/url/URLSearchParamsIterator/map)<U>(

    callbackfn: (value: T, index: number) => U

    ): IteratorObject<U, undefined, unknown>;

    Creates an iterator whose values are the result of applying the callback to the values from this iterator.

    @param callbackfn

    A function that accepts up to two arguments to be used to transform values from the underlying iterator.
  + [next](https://bun.com/reference/node/url/URLSearchParamsIterator/next)(

    ...\_\_namedParameters: [] | [unknown]

    ): IteratorResult<T, undefined>;
  + [reduce](https://bun.com/reference/node/url/URLSearchParamsIterator/reduce)(

    callbackfn: (previousValue: T, currentValue: T, currentIndex: number) => T

    ): T;

    Calls the specified callback function for all the elements in this iterator. The return value of the callback function is the accumulated result, and is provided as an argument in the next call to the callback function.

    @param callbackfn

    A function that accepts up to three arguments. The reduce method calls the callbackfn function one time for each element in the iterator.

    [reduce](https://bun.com/reference/node/url/URLSearchParamsIterator/reduce)(

    callbackfn: (previousValue: T, currentValue: T, currentIndex: number) => T,

    initialValue: T

    ): T;

    [reduce](https://bun.com/reference/node/url/URLSearchParamsIterator/reduce)<U>(

    callbackfn: (previousValue: U, currentValue: T, currentIndex: number) => U,

    initialValue: U

    ): U;

    Calls the specified callback function for all the elements in this iterator. The return value of the callback function is the accumulated result, and is provided as an argument in the next call to the callback function.

    @param callbackfn

    A function that accepts up to three arguments. The reduce method calls the callbackfn function one time for each element in the iterator.

    @param initialValue

    If initialValue is specified, it is used as the initial value to start the accumulation. The first call to the callbackfn function provides this value as an argument instead of a value from the iterator.
  + [return](https://bun.com/reference/node/url/URLSearchParamsIterator/return)(

    value?: undefined

    ): IteratorResult<T, undefined>;
  + [some](https://bun.com/reference/node/url/URLSearchParamsIterator/some)(

    predicate: (value: T, index: number) => unknown

    ): boolean;

    Determines whether the specified callback function returns true for any element of this iterator.

    @param predicate

    A function that accepts up to two arguments. The some method calls the predicate function for each element in this iterator until the predicate returns a value true, or until the end of the iterator.
  + [take](https://bun.com/reference/node/url/URLSearchParamsIterator/take)(

    limit: number

    ): IteratorObject<T, undefined, unknown>;

    Creates an iterator whose values are the values from this iterator, stopping once the provided limit is reached.

    @param limit

    The maximum number of values to yield.
  + [throw](https://bun.com/reference/node/url/URLSearchParamsIterator/throw)(

    e?: any

    ): IteratorResult<T, undefined>;
  + [toArray](https://bun.com/reference/node/url/URLSearchParamsIterator/toArray)(): T[];

    Creates a new array from the values yielded by this iterator.
* ### interface [UrlWithParsedQuery](https://bun.com/reference/node/url/UrlWithParsedQuery)

  + [auth](https://bun.com/reference/node/url/UrlWithParsedQuery/auth): null | string
  + [hash](https://bun.com/reference/node/url/UrlWithParsedQuery/hash): null | string
  + [host](https://bun.com/reference/node/url/UrlWithParsedQuery/host): null | string
  + [hostname](https://bun.com/reference/node/url/UrlWithParsedQuery/hostname): null | string
  + [href](https://bun.com/reference/node/url/UrlWithParsedQuery/href): string
  + [path](https://bun.com/reference/node/url/UrlWithParsedQuery/path): null | string
  + [pathname](https://bun.com/reference/node/url/UrlWithParsedQuery/pathname): null | string
  + [port](https://bun.com/reference/node/url/UrlWithParsedQuery/port): null | string
  + [query](https://bun.com/reference/node/url/UrlWithParsedQuery/query): [ParsedUrlQuery](https://bun.com/reference/node/querystring/ParsedUrlQuery)
  + [search](https://bun.com/reference/node/url/UrlWithParsedQuery/search): null | string
  + [slashes](https://bun.com/reference/node/url/UrlWithParsedQuery/slashes): null | boolean
* ### interface [UrlWithStringQuery](https://bun.com/reference/node/url/UrlWithStringQuery)

  + [auth](https://bun.com/reference/node/url/UrlWithStringQuery/auth): null | string
  + [hash](https://bun.com/reference/node/url/UrlWithStringQuery/hash): null | string
  + [host](https://bun.com/reference/node/url/UrlWithStringQuery/host): null | string
  + [hostname](https://bun.com/reference/node/url/UrlWithStringQuery/hostname): null | string
  + [href](https://bun.com/reference/node/url/UrlWithStringQuery/href): string
  + [path](https://bun.com/reference/node/url/UrlWithStringQuery/path): null | string
  + [pathname](https://bun.com/reference/node/url/UrlWithStringQuery/pathname): null | string
  + [port](https://bun.com/reference/node/url/UrlWithStringQuery/port): null | string
  + [query](https://bun.com/reference/node/url/UrlWithStringQuery/query): null | string
  + [search](https://bun.com/reference/node/url/UrlWithStringQuery/search): null | string
  + [slashes](https://bun.com/reference/node/url/UrlWithStringQuery/slashes): null | boolean