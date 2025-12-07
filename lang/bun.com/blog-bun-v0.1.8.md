---
url: https://bun.com/blog/bun-v0.1.8
title: Bun v0.1.8 | Bun Blog
source_domain: bun.com
---

# Bun v0.1.8 | Bun Blog

# Bun v0.1.8

---

[Jarred Sumner](https://twitter.com/jarredsumner) · August 11, 2022

To upgrade:

```
bun upgrade
```

To install:

```
curl https://bun.sh/install | bash
```

If you have any problems upgrading

Run the install script (you can run it multiple times):

```
curl https://bun.sh/install | bash
```

## [What's new](https://bun.com/blog/bun-v0.1.8#what-s-new)

A huge thank you to [@zhuzilin](https://github.com/zhuzilin) for all their help on this release. @zhuzilin fixed 4 crashes!

**`bun link`** lets you symlink a folder to node\_modules. It works like npm link.

[![](https://user-images.githubusercontent.com/709451/184067798-47a3f596-fc58-42d7-8fd6-51e085b99ceb.png)](https://user-images.githubusercontent.com/709451/184067798-47a3f596-fc58-42d7-8fd6-51e085b99ceb.png)

**`fs.copyFileSync`** gets 2x to 10x faster:

[![](https://user-images.githubusercontent.com/709451/184067848-071d266c-34e2-4527-9109-506c3998bdc0.png)](https://user-images.githubusercontent.com/709451/184067848-071d266c-34e2-4527-9109-506c3998bdc0.png)

`require.resolve` works at runtime now instead of only build-time

[![image](https://user-images.githubusercontent.com/709451/184080105-933acd43-7db5-4ee0-84ee-12cb364236c7.png)](https://user-images.githubusercontent.com/709451/184080105-933acd43-7db5-4ee0-84ee-12cb364236c7.png)

`WebSocket` is more reliable now. Previously the garbage collector would attempt to free it when the socket was still open 🙉

`bun:ffi`'s `toBuffer` and `toArrayBuffer` functions now support a function pointer to a destructor so that native code can perform cleanup without needing to go through a `FinalizationRegistry`.

#### console.log

`TypedArray` logs the value for the type (instead of in bytes 🙈)

[![image](https://user-images.githubusercontent.com/709451/184079844-feb408f1-30f5-402f-a479-647df879a6e6.png)](https://user-images.githubusercontent.com/709451/184079844-feb408f1-30f5-402f-a479-647df879a6e6.png)

console.log(`MessageEvent` ) is more useful now

[![image](https://user-images.githubusercontent.com/709451/184079813-bb30f902-af8d-4042-b8bb-f069e0535587.png)](https://user-images.githubusercontent.com/709451/184079813-bb30f902-af8d-4042-b8bb-f069e0535587.png)

More:

* `setInterval` wouldn't cause the process to stay alive 😢 and now that is fixed thanks to [@zhuzilin](https://github.com/zhuzilin)
* Log error on unhandled rejected promises by [@zhuzilin](https://github.com/zhuzilin) in https://github.com/oven-sh/bun/pull/1010
* Log error on uncaught exceptions in event loop
* `bun install` gets a `symlink` backend, which you probably don't want to use in most cases. It's used internally if you do `file:./` as a dependency, which some packages do
* `process.revision` returns the git sha used to build bun

## [Bug fixes](https://bun.com/blog/bun-v0.1.8#bug-fixes)

* build issue caused "Illegal instruction" error to return - that is fixed now
* [wiptest] fix calling toBe in describe by [@zhuzilin](https://github.com/zhuzilin) in https://github.com/oven-sh/bun/pull/1000
* Re-register setInterval to VM after completion by [@zhuzilin](https://github.com/zhuzilin) in https://github.com/oven-sh/bun/pull/1014
* Fix segfault for query().all() with more than 64 properties by [@zhuzilin](https://github.com/zhuzilin) in https://github.com/oven-sh/bun/pull/1025
* Update example Next app to 12.2 by [@TiKevin83](https://github.com/TiKevin83) in https://github.com/oven-sh/bun/pull/1033
* Fix static require by setting the state machine manually by [@zhuzilin](https://github.com/zhuzilin) in https://github.com/oven-sh/bun/pull/1034
* #941 fix by [@JL102](https://github.com/JL102) in https://github.com/oven-sh/bun/pull/998

Typos:

* refactor(src/install): clap readability fixes by [@ryanrussell](https://github.com/ryanrussell) in https://github.com/oven-sh/bun/pull/1024

Misc:

* fix compiling error on linux by [@zhuzilin](https://github.com/zhuzilin) in https://github.com/oven-sh/bun/pull/1027

**Full Changelog**: https://github.com/oven-sh/bun/compare/bun-v0.1.7...bun-v0.1.8

---

[#### Bun v0.1.7](https://bun.com/blog/bun-v0.1.7)[#### Bun v0.1.9](https://bun.com/blog/bun-v0.1.9)