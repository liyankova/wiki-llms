---
url: https://bun.com/docs/runtime/cookies
title: Cookies - Bun
source_domain: bun.com
---

# Cookies - Bun

Bun provides native APIs for working with HTTP cookies through `Bun.Cookie` and `Bun.CookieMap`. These APIs offer fast, easy-to-use methods for parsing, generating, and manipulating cookies in HTTP requests and responses.

## [​](https://bun.com/docs/runtime/cookies#cookiemap-class) CookieMap class

`Bun.CookieMap` provides a Map-like interface for working with collections of cookies. It implements the `Iterable` interface, allowing you to use it with `for...of` loops and other iteration methods.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)cookies.ts

Copy

```
// Empty cookie map
const cookies = new Bun.CookieMap();

// From a cookie string
const cookies1 = new Bun.CookieMap("name=value; foo=bar");

// From an object
const cookies2 = new Bun.CookieMap({
  session: "abc123",
  theme: "dark",
});

// From an array of name/value pairs
const cookies3 = new Bun.CookieMap([
  ["session", "abc123"],
  ["theme", "dark"],
]);
```

### [​](https://bun.com/docs/runtime/cookies#in-http-servers) In HTTP servers

In Bun’s HTTP server, the `cookies` property on the request object (in `routes`) is an instance of `CookieMap`:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)server.ts

Copy

```
const server = Bun.serve({
  routes: {
    "/": req => {
      // Access request cookies
      const cookies = req.cookies;

      // Get a specific cookie
      const sessionCookie = cookies.get("session");
      if (sessionCookie != null) {
        console.log(sessionCookie);
      }

      // Check if a cookie exists
      if (cookies.has("theme")) {
        // ...
      }

      // Set a cookie, it will be automatically applied to the response
      cookies.set("visited", "true");

      return new Response("Hello");
    },
  },
});

console.log("Server listening at: " + server.url);
```

### [​](https://bun.com/docs/runtime/cookies#methods) Methods

#### [​](https://bun.com/docs/runtime/cookies#get-name:-string-:-string-|-null) `get(name: string): string | null`

Retrieves a cookie by name. Returns `null` if the cookie doesn’t exist.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)get-cookie.ts

Copy

```
// Get by name
const cookie = cookies.get("session");

if (cookie != null) {
  console.log(cookie);
}
```

#### [​](https://bun.com/docs/runtime/cookies#has-name:-string-:-boolean) `has(name: string): boolean`

Checks if a cookie with the given name exists.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)has-cookie.ts

Copy

```
// Check if cookie exists
if (cookies.has("session")) {
  // Cookie exists
}
```

#### [​](https://bun.com/docs/runtime/cookies#set-name:-string,-value:-string-:-void) `set(name: string, value: string): void`

#### [​](https://bun.com/docs/runtime/cookies#set-options:-cookieinit-:-void) `set(options: CookieInit): void`

#### [​](https://bun.com/docs/runtime/cookies#set-cookie:-cookie-:-void) `set(cookie: Cookie): void`

Adds or updates a cookie in the map. Cookies default to `{ path: "/", sameSite: "lax" }`.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)set-cookie.ts

Copy

```
// Set by name and value
cookies.set("session", "abc123");

// Set using options object
cookies.set({
  name: "theme",
  value: "dark",
  maxAge: 3600,
  secure: true,
});

// Set using Cookie instance
const cookie = new Bun.Cookie("visited", "true");
cookies.set(cookie);
```

#### [​](https://bun.com/docs/runtime/cookies#delete-name:-string-:-void) `delete(name: string): void`

#### [​](https://bun.com/docs/runtime/cookies#delete-options:-cookiestoredeleteoptions-:-void) `delete(options: CookieStoreDeleteOptions): void`

Removes a cookie from the map. When applied to a Response, this adds a cookie with an empty string value and an expiry date in the past. A cookie will only delete successfully on the browser if the domain and path is the same as it was when the cookie was created.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)delete-cookie.ts

Copy

```
// Delete by name using default domain and path.
cookies.delete("session");

// Delete with domain/path options.
cookies.delete({
  name: "session",
  domain: "example.com",
  path: "/admin",
});
```

#### [​](https://bun.com/docs/runtime/cookies#tojson-:-record<string,-string>) `toJSON(): Record<string, string>`

Converts the cookie map to a serializable format.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)cookie-to-json.ts

Copy

```
const json = cookies.toJSON();
```

#### [​](https://bun.com/docs/runtime/cookies#tosetcookieheaders-:-string[]) `toSetCookieHeaders(): string[]`

Returns an array of values for Set-Cookie headers that can be used to apply all cookie changes.
When using `Bun.serve()`, you don’t need to call this method explicitly. Any changes made to the `req.cookies` map are automatically applied to the response headers. This method is primarily useful when working with other HTTP server implementations.

node-server.js

Copy

```
import { createServer } from "node:http";
import { CookieMap } from "bun";

const server = createServer((req, res) => {
  const cookieHeader = req.headers.cookie || "";
  const cookies = new CookieMap(cookieHeader);

  cookies.set("view-count", Number(cookies.get("view-count") || "0") + 1);
  cookies.delete("session");

  res.writeHead(200, {
    "Content-Type": "text/plain",
    "Set-Cookie": cookies.toSetCookieHeaders(),
  });
  res.end(`Found ${cookies.size} cookies`);
});

server.listen(3000, () => {
  console.log("Server running at http://localhost:3000/");
});
```

### [​](https://bun.com/docs/runtime/cookies#iteration) Iteration

`CookieMap` provides several methods for iteration:

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)iterate-cookies.ts

Copy

```
// Iterate over [name, cookie] entries
for (const [name, value] of cookies) {
  console.log(`${name}: ${value}`);
}

// Using entries()
for (const [name, value] of cookies.entries()) {
  console.log(`${name}: ${value}`);
}

// Using keys()
for (const name of cookies.keys()) {
  console.log(name);
}

// Using values()
for (const value of cookies.values()) {
  console.log(value);
}

// Using forEach
cookies.forEach((value, name) => {
  console.log(`${name}: ${value}`);
});
```

### [​](https://bun.com/docs/runtime/cookies#properties) Properties

#### [​](https://bun.com/docs/runtime/cookies#size:-number) `size: number`

Returns the number of cookies in the map.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)cookie-size.ts

Copy

```
console.log(cookies.size); // Number of cookies
```

## [​](https://bun.com/docs/runtime/cookies#cookie-class) Cookie class

`Bun.Cookie` represents an HTTP cookie with its name, value, and attributes.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)cookie-class.ts

Copy

```
import { Cookie } from "bun";

// Create a basic cookie
const cookie = new Bun.Cookie("name", "value");

// Create a cookie with options
const secureSessionCookie = new Bun.Cookie("session", "abc123", {
  domain: "example.com",
  path: "/admin",
  expires: new Date(Date.now() + 86400000), // 1 day
  httpOnly: true,
  secure: true,
  sameSite: "strict",
});

// Parse from a cookie string
const parsedCookie = new Bun.Cookie("name=value; Path=/; HttpOnly");

// Create from an options object
const objCookie = new Bun.Cookie({
  name: "theme",
  value: "dark",
  maxAge: 3600,
  secure: true,
});
```

### [​](https://bun.com/docs/runtime/cookies#constructors) Constructors

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)constructors.ts

Copy

```
// Basic constructor with name/value
new Bun.Cookie(name: string, value: string);

// Constructor with name, value, and options
new Bun.Cookie(name: string, value: string, options: CookieInit);

// Constructor from cookie string
new Bun.Cookie(cookieString: string);

// Constructor from cookie object
new Bun.Cookie(options: CookieInit);
```

### [​](https://bun.com/docs/runtime/cookies#properties-2) Properties

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)cookie-properties.ts

Copy

```
cookie.name; // string - Cookie name
cookie.value; // string - Cookie value
cookie.domain; // string | null - Domain scope (null if not specified)
cookie.path; // string - URL path scope (defaults to "/")
cookie.expires; // number | undefined - Expiration timestamp (ms since epoch)
cookie.secure; // boolean - Require HTTPS
cookie.sameSite; // "strict" | "lax" | "none" - SameSite setting
cookie.partitioned; // boolean - Whether the cookie is partitioned (CHIPS)
cookie.maxAge; // number | undefined - Max age in seconds
cookie.httpOnly; // boolean - Accessible only via HTTP (not JavaScript)
```

### [​](https://bun.com/docs/runtime/cookies#methods-2) Methods

#### [​](https://bun.com/docs/runtime/cookies#isexpired-:-boolean) `isExpired(): boolean`

Checks if the cookie has expired.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)is-expired.ts

Copy

```
// Expired cookie (Date in the past)
const expiredCookie = new Bun.Cookie("name", "value", {
  expires: new Date(Date.now() - 1000),
});
console.log(expiredCookie.isExpired()); // true

// Valid cookie (Using maxAge instead of expires)
const validCookie = new Bun.Cookie("name", "value", {
  maxAge: 3600, // 1 hour in seconds
});
console.log(validCookie.isExpired()); // false

// Session cookie (no expiration)
const sessionCookie = new Bun.Cookie("name", "value");
console.log(sessionCookie.isExpired()); // false
```

#### [​](https://bun.com/docs/runtime/cookies#serialize-:-string) `serialize(): string`

#### [​](https://bun.com/docs/runtime/cookies#tostring-:-string) `toString(): string`

Returns a string representation of the cookie suitable for a `Set-Cookie` header.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)serialize-cookie.ts

Copy

```
const cookie = new Bun.Cookie("session", "abc123", {
  domain: "example.com",
  path: "/admin",
  expires: new Date(Date.now() + 86400000),
  secure: true,
  httpOnly: true,
  sameSite: "strict",
});

console.log(cookie.serialize());
// => "session=abc123; Domain=example.com; Path=/admin; Expires=Sun, 19 Mar 2025 15:03:26 GMT; Secure; HttpOnly; SameSite=strict"
console.log(cookie.toString());
// => "session=abc123; Domain=example.com; Path=/admin; Expires=Sun, 19 Mar 2025 15:03:26 GMT; Secure; HttpOnly; SameSite=strict"
```

#### [​](https://bun.com/docs/runtime/cookies#tojson-:-cookieinit) `toJSON(): CookieInit`

Converts the cookie to a plain object suitable for JSON serialization.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)cookie-json.ts

Copy

```
const cookie = new Bun.Cookie("session", "abc123", {
  secure: true,
  httpOnly: true,
});

const json = cookie.toJSON();
// => {
//   name: "session",
//   value: "abc123",
//   path: "/",
//   secure: true,
//   httpOnly: true,
//   sameSite: "lax",
//   partitioned: false
// }

// Works with JSON.stringify
const jsonString = JSON.stringify(cookie);
```

### [​](https://bun.com/docs/runtime/cookies#static-methods) Static methods

#### [​](https://bun.com/docs/runtime/cookies#cookie-parse-cookiestring:-string-:-cookie) `Cookie.parse(cookieString: string): Cookie`

Parses a cookie string into a `Cookie` instance.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)parse-cookie.ts

Copy

```
const cookie = Bun.Cookie.parse("name=value; Path=/; Secure; SameSite=Lax");

console.log(cookie.name); // "name"
console.log(cookie.value); // "value"
console.log(cookie.path); // "/"
console.log(cookie.secure); // true
console.log(cookie.sameSite); // "lax"
```

#### [​](https://bun.com/docs/runtime/cookies#cookie-from-name:-string,-value:-string,-options:-cookieinit-:-cookie) `Cookie.from(name: string, value: string, options?: CookieInit): Cookie`

Factory method to create a cookie.

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)cookie-from.ts

Copy

```
const cookie = Bun.Cookie.from("session", "abc123", {
  httpOnly: true,
  secure: true,
  maxAge: 3600,
});
```

## [​](https://bun.com/docs/runtime/cookies#types) Types

![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/typescript.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=c6cceedec8f82d2cc803d7c6ec82b240)types.ts

Copy

```
interface CookieInit {
  name?: string;
  value?: string;
  domain?: string;
  /** Defaults to '/'. To allow the browser to set the path, use an empty string. */
  path?: string;
  expires?: number | Date | string;
  secure?: boolean;
  /** Defaults to `lax`. */
  sameSite?: CookieSameSite;
  httpOnly?: boolean;
  partitioned?: boolean;
  maxAge?: number;
}

interface CookieStoreDeleteOptions {
  name: string;
  domain?: string | null;
  path?: string;
}

interface CookieStoreGetOptions {
  name?: string;
  url?: string;
}

type CookieSameSite = "strict" | "lax" | "none";

class Cookie {
  constructor(name: string, value: string, options?: CookieInit);
  constructor(cookieString: string);
  constructor(cookieObject?: CookieInit);

  readonly name: string;
  value: string;
  domain?: string;
  path: string;
  expires?: Date;
  secure: boolean;
  sameSite: CookieSameSite;
  partitioned: boolean;
  maxAge?: number;
  httpOnly: boolean;

  isExpired(): boolean;

  serialize(): string;
  toString(): string;
  toJSON(): CookieInit;

  static parse(cookieString: string): Cookie;
  static from(name: string, value: string, options?: CookieInit): Cookie;
}

class CookieMap implements Iterable<[string, string]> {
  constructor(init?: string[][] | Record<string, string> | string);

  get(name: string): string | null;

  toSetCookieHeaders(): string[];

  has(name: string): boolean;
  set(name: string, value: string, options?: CookieInit): void;
  set(options: CookieInit): void;
  delete(name: string): void;
  delete(options: CookieStoreDeleteOptions): void;
  delete(name: string, options: Omit<CookieStoreDeleteOptions, "name">): void;
  toJSON(): Record<string, string>;

  readonly size: number;

  entries(): IterableIterator<[string, string]>;
  keys(): IterableIterator<string>;
  values(): IterableIterator<string>;
  forEach(callback: (value: string, key: string, map: CookieMap) => void): void;
  [Symbol.iterator](): IterableIterator<[string, string]>;
}
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/runtime/cookies.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /runtime/cookies)

⌘I