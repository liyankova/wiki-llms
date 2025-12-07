---
url: https://bun.com/blog/bun-v0.1.10
title: Bun v0.1.10 | Bun Blog
source_domain: bun.com
---

# Bun v0.1.10 | Bun Blog

# Bun v0.1.10

---

[Jarred Sumner](https://twitter.com/jarredsumner) · August 19, 2022

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

## [What's new](https://bun.com/blog/bun-v0.1.10#what-s-new)

* Fix a regression causing `bun dev` to not send HTTP bodies
* Fix console.log printing `[native code]` for too many things 5eeb704f25200af7ad8819c35bcfd16b8b1bff49
* Fix crash in `bun dev` when used with Next.js e45ddc086fe6b3e7a32aa45607f5e3d570998137
* Fix bug with `Buffer.compare` https://github.com/oven-sh/bun/commit/d150a2f4ddc10597e4531fd3c55b62bb0ecbf02c
* Make `TextDecoder` 2.5x faster e3c2a95e5ff4e6c6b63839f4773cc3f5aeadddc8
* Fix memory leak in `WebSocket` bdf733973c72b8e156cd1cf1c6c8a8b4649fedbe
* Make `Request`, `Response` and `TextDecoder` globals not read-only 0f45386673fbf4f33b6e61b17ea49b69697ec79a

[**Full Changelog**](https://github.com/oven-sh/bun/compare/bun-v0.1.9...bun-v0.1.10)

---

[#### Bun v0.1.9](https://bun.com/blog/bun-v0.1.9)[#### Bun v0.1.11](https://bun.com/blog/bun-v0.1.11)