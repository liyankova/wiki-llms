---
url: https://nix.dev/manual/nix/2.32/store/types/local-binary-cache-store
title: Local Binary Cache Store - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Local Binary Cache Store - Nix 2.32.2 Reference Manual

# [Local Binary Cache Store](https://nix.dev/manual/nix/2.32/store/types/local-binary-cache-store#local-binary-cache-store)

**Store URL format**: `file://`*path*

This store allows reading and writing a binary cache stored in *path*
in the local filesystem. If *path* does not exist, it will be created.

For example, the following builds or downloads `nixpkgs#hello` into
the local store and then copies it to the binary cache in
`/tmp/binary-cache`:

```
# nix copy --to file:///tmp/binary-cache nixpkgs#hello
```

## [Settings](https://nix.dev/manual/nix/2.32/store/types/local-binary-cache-store#settings)

* [`compression`](https://nix.dev/manual/nix/2.32/store/types/local-binary-cache-store#store-local-binary-cache-store-compression)

  NAR compression method (`xz`, `bzip2`, `gzip`, `zstd`, or `none`).

  **Default:** `xz`
* [`compression-level`](https://nix.dev/manual/nix/2.32/store/types/local-binary-cache-store#store-local-binary-cache-store-compression-level)

  The *preset level* to be used when compressing NARs.
  The meaning and accepted values depend on the compression method selected.
  `-1` specifies that the default compression level should be used.

  **Default:** `-1`
* [`index-debug-info`](https://nix.dev/manual/nix/2.32/store/types/local-binary-cache-store#store-local-binary-cache-store-index-debug-info)

  Whether to index DWARF debug info files by build ID. This allows [`dwarffs`](https://github.com/edolstra/dwarffs) to
  fetch debug info on demand

  **Default:** `false`
* [`local-nar-cache`](https://nix.dev/manual/nix/2.32/store/types/local-binary-cache-store#store-local-binary-cache-store-local-nar-cache)

  Path to a local cache of NARs fetched from this binary cache, used by commands such as `nix store cat`.

  **Default:** *empty*
* [`parallel-compression`](https://nix.dev/manual/nix/2.32/store/types/local-binary-cache-store#store-local-binary-cache-store-parallel-compression)

  Enable multi-threaded compression of NARs. This is currently only available for `xz` and `zstd`.

  **Default:** `false`
* [`path-info-cache-size`](https://nix.dev/manual/nix/2.32/store/types/local-binary-cache-store#store-local-binary-cache-store-path-info-cache-size)

  Size of the in-memory store path metadata cache.

  **Default:** `65536`
* [`priority`](https://nix.dev/manual/nix/2.32/store/types/local-binary-cache-store#store-local-binary-cache-store-priority)

  Priority of this store when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).
  A lower value means a higher priority.

  **Default:** `0`
* [`secret-key`](https://nix.dev/manual/nix/2.32/store/types/local-binary-cache-store#store-local-binary-cache-store-secret-key)

  Path to the secret key used to sign the binary cache.

  **Default:** *empty*
* [`secret-keys`](https://nix.dev/manual/nix/2.32/store/types/local-binary-cache-store#store-local-binary-cache-store-secret-keys)

  List of comma-separated paths to the secret keys used to sign the binary cache.

  **Default:** *empty*
* [`store`](https://nix.dev/manual/nix/2.32/store/types/local-binary-cache-store#store-local-binary-cache-store-store)

  Logical location of the Nix store, usually
  `/nix/store`. Note that you can only copy store paths
  between stores if they have the same `store` setting.

  **Default:** `/nix/store`
* [`system-features`](https://nix.dev/manual/nix/2.32/store/types/local-binary-cache-store#store-local-binary-cache-store-system-features)

  Optional [system features](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-system-features) available on the system this store uses to build derivations.

  Example: `"kvm"`

  **Default:** *machine-specific*
* [`trusted`](https://nix.dev/manual/nix/2.32/store/types/local-binary-cache-store#store-local-binary-cache-store-trusted)

  Whether paths from this store can be used as substitutes
  even if they are not signed by a key listed in the
  [`trusted-public-keys`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-trusted-public-keys)
  setting.

  **Default:** `false`
* [`want-mass-query`](https://nix.dev/manual/nix/2.32/store/types/local-binary-cache-store#store-local-binary-cache-store-want-mass-query)

  Whether this store can be queried efficiently for path validity when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).

  **Default:** `false`
* [`write-nar-listing`](https://nix.dev/manual/nix/2.32/store/types/local-binary-cache-store#store-local-binary-cache-store-write-nar-listing)

  Whether to write a JSON file that lists the files in each NAR.

  **Default:** `false`