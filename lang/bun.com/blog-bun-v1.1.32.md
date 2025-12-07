---
url: https://bun.com/blog/bun-v1.1.32
title: Bun v1.1.32 | Bun Blog
source_domain: bun.com
---

# Bun v1.1.32 | Bun Blog

# Bun v1.1.32

---

[Jarred Sumner](https://twitter.com/jarredsumner) · October 21, 2024

We're hiring [systems engineers](https://bun.com/careers) in San Francisco to build the future of JavaScript!

This release fixes 7 bugs and adds crypto.hash() in node:crypto. Warnings in Next.js 15 are fixed. A regression in ESM <> CJS interop impacting Vite config objects is fixed. A crash in Bun.serve() when passing invalid TLS certificates at start is fixed.

#### To install Bun

curl

npm

powershell

scoop

brew

docker

curl

```
curl -fsSL https://bun.sh/install | bash
```

npm

```
npm install -g bun
```

powershell

```
powershell -c "irm bun.sh/install.ps1|iex"
```

scoop

```
scoop install bun
```

brew

```
brew tap oven-sh/bun
```

```
brew install bun
```

docker

```
docker pull oven/bun
```

```
docker run --rm --init --ulimit memlock=-1:-1 oven/bun
```

#### To upgrade Bun

```
bun upgrade
```

## [crypto.hash()](https://bun.com/blog/bun-v1.1.32#crypto-hash)

The Node.js [`crypto.hash()`](https://nodejs.org/api/crypto.html#cryptohashalgorithm-data-outputencoding) method is now available in Bun. This is a one-shot method that returns a `buffer`, `hex`, `base64`, or `base64url` representation of the hash algorithm of your choosing.

```
import { hash } from "crypto";

const hex = hash("sha256", "hello", "hex");
console.log(hex); // "2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824"
```

Internally, this calls `Bun.CryptoHasher.hash()`.

## [Bugfixes](https://bun.com/blog/bun-v1.1.32#bugfixes)

### [Fixed: Debugger regression in v1.1.31](https://bun.com/blog/bun-v1.1.32#fixed-debugger-regression-in-v1-1-31)

A regression in v1.1.31 caused the debugger to stop connecting. This is now fixed. Thanks to [@nektro](https://github.com/nektro) for the fix.

### [Fixed: CJS <> ESM bug impacting Vite](https://bun.com/blog/bun-v1.1.32#fixed-cjs-esm-bug-impacting-vite)

In Bun v1.1.30, we made a small change to our `require(esm)` implementation that caused projects with `"type": "module"` to not set `__esModule` when requiring ESM modules.

The intent of that change was to avoid adding an extra wrapper object around module namespace objects, but it caused a regression in Vite when reading from the Vite config object.

Before Bun v1.1.30, the wrapper essentially did this:

```
const namespace = Loader.getModuleNamespaceObject(esm!.module);
module.exports =
  namespace.__esModule ? namespace : Object.create(namespace, { __esModule: { value: true } });
```

This had the downside of adding an extra wrapper object around module namespace objects, which also meant that the `...spread` operator and JSON.stringify would be missing the exported values.

In Bun v1.1.30 - Bun v1.1.31, to fix that issue, we simplified it to directly return the namespace object (which matches Node.js behavior more closely):

```
module.exports = Loader.getModuleNamespaceObject(esm!.module);
```

But, this led to a regression in Vite when reading from the Vite config object when the package.json `"type"` was `"module"`.

To fix this without reintroducing the extra wrapper object, we've made a change to module namespace objects in JavaScriptCore to specifically allow the `__esModule` property to be set to `true` or `undefined` without needing an `__esModule` export. It won't appear as an own property, and will only be writable this way if it's not already an own property.

Now, we do this:

```
const namespace = Loader.getModuleNamespaceObject(esm!.module);
if (namespace.__esModule === undefined) {
    namespace.__esModule = true;
}
module.exports = namespace;
```

### [Fixed: Warnings in Next.js 15](https://bun.com/blog/bun-v1.1.32#fixed-warnings-in-next-js-15)

Previously, the following warnings were logged in Next.js 15 on startup:

```
Failed to install `require('node:crypto').randomUUID()` extension. When using `experimental.dynamicIO` calling this function will not correctly trigger dynamic behavior.
Failed to install `require('node:crypto').randomBytes(size)` extension. When using `experimental.dynamicIO` calling this function without a callback argument will not correctly trigger dynamic behavior.
Failed to install `require('node:crypto').randomUUID()` extension. When using `experimental.dynamicIO` calling this function will not correctly trigger dynamic behavior.
Failed to install `require('node:crypto').randomBytes(size)` extension. When using `experimental.dynamicIO` calling this function without a callback argument will not correctly trigger dynamic behavior.
Failed to install `require('node:crypto').randomUUID()` extension. When using `experimental.dynamicIO` calling this function will not correctly trigger dynamic behavior.
Failed to install `require('node:crypto').randomBytes(size)` extension. When using `experimental.dynamicIO` calling this function without a callback argument will not correctly trigger dynamic behavior.
```

This is now fixed. The bug was because some properties in `node:crypto` were set to read-only on the module.exports object. Those properties are no longer set to read-only.

### [Fixed: Crash in CryptoHasher with HMAC for unsupported algorithms](https://bun.com/blog/bun-v1.1.32#fixed-crash-in-cryptohasher-with-hmac-for-unsupported-algorithms)

In Bun v1.1.30, we introduced support for HMAC in `Bun.CryptoHasher`.

However, if you passed an algorithm recognized by Bun but unsupported by BoringSSL, it would crash. This is now fixed, we throw a TODO error instead.

### [Fixed: Crash with invalid TLS certificate in Bun.serve()](https://bun.com/blog/bun-v1.1.32#fixed-crash-with-invalid-tls-certificate-in-bun-serve)

A bug in our error-handling code caused TLS configuration errors in `Bun.serve()` to crash the process (before starting the server) when it should've thrown a JavaScript exception.

### [Fixed: `Bun.color` argument validation mismatch](https://bun.com/blog/bun-v1.1.32#fixed-bun-color-argument-validation-mismatch)

The `Bun.color` method printed enum values for the "format" argument in the error message that were not valid. This is now fixed, thanks to [@nektro](https://github.com/nektro).

## [Thanks to 5 contributors!](https://bun.com/blog/bun-v1.1.32#thanks-to-5-contributors)

* [@cirospaciari](https://github.com/cirospaciari)
* [@dylan-conway](https://github.com/dylan-conway)
* [@Electroid](https://github.com/Electroid)
* [@Jarred-Sumner](https://github.com/Jarred-Sumner)
* [@Nanome203](https://github.com/Nanome203)
* [@nektro](https://github.com/nektro)

---

[#### Bun v1.1.31](https://bun.com/blog/bun-v1.1.31)[#### Bun v1.1.33](https://bun.com/blog/bun-v1.1.33)