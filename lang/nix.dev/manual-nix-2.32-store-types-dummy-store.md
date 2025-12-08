---
url: https://nix.dev/manual/nix/2.32/store/types/dummy-store
title: Dummy Store - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Dummy Store - Nix 2.32.2 Reference Manual

# [Dummy Store](https://nix.dev/manual/nix/2.32/store/types/dummy-store#dummy-store)

**Store URL format**: `dummy://`

This store type represents a store in memory.
Store objects can be read and written, but only so long as the store is open.
Once the store is closed, all data will be discarded.

It's useful when you want to use the Nix evaluator when no actual Nix store exists, e.g.

```
# nix eval --store dummy:// --expr '1 + 2'
```

## [Settings](https://nix.dev/manual/nix/2.32/store/types/dummy-store#settings)

* [`path-info-cache-size`](https://nix.dev/manual/nix/2.32/store/types/dummy-store#store-dummy-store-path-info-cache-size)

  Size of the in-memory store path metadata cache.

  **Default:** `65536`
* [`priority`](https://nix.dev/manual/nix/2.32/store/types/dummy-store#store-dummy-store-priority)

  Priority of this store when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).
  A lower value means a higher priority.

  **Default:** `0`
* [`read-only`](https://nix.dev/manual/nix/2.32/store/types/dummy-store#store-dummy-store-read-only)

  Make any sort of write fail instead of succeeding.
  No additional memory will be used, because no information needs to be stored.

  **Default:** `true`
* [`store`](https://nix.dev/manual/nix/2.32/store/types/dummy-store#store-dummy-store-store)

  Logical location of the Nix store, usually
  `/nix/store`. Note that you can only copy store paths
  between stores if they have the same `store` setting.

  **Default:** `/nix/store`
* [`system-features`](https://nix.dev/manual/nix/2.32/store/types/dummy-store#store-dummy-store-system-features)

  Optional [system features](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-system-features) available on the system this store uses to build derivations.

  Example: `"kvm"`

  **Default:** *machine-specific*
* [`trusted`](https://nix.dev/manual/nix/2.32/store/types/dummy-store#store-dummy-store-trusted)

  Whether paths from this store can be used as substitutes
  even if they are not signed by a key listed in the
  [`trusted-public-keys`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-trusted-public-keys)
  setting.

  **Default:** `false`
* [`want-mass-query`](https://nix.dev/manual/nix/2.32/store/types/dummy-store#store-dummy-store-want-mass-query)

  Whether this store can be queried efficiently for path validity when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).

  **Default:** `false`