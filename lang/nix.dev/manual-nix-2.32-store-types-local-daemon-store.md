---
url: https://nix.dev/manual/nix/2.32/store/types/local-daemon-store
title: Local Daemon Store - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Local Daemon Store - Nix 2.32.2 Reference Manual

# [Local Daemon Store](https://nix.dev/manual/nix/2.32/store/types/local-daemon-store#local-daemon-store)

**Store URL format**: `daemon`, `unix://`*path*

This store type accesses a Nix store by talking to a Nix daemon
listening on the Unix domain socket *path*. The store pseudo-URL
`daemon` is equivalent to `unix:///nix/var/nix/daemon-socket/socket`.

## [Settings](https://nix.dev/manual/nix/2.32/store/types/local-daemon-store#settings)

* [`log`](https://nix.dev/manual/nix/2.32/store/types/local-daemon-store#store-local-daemon-store-log)

  directory where Nix stores log files.

  **Default:** `/nix/var/log/nix`
* [`max-connection-age`](https://nix.dev/manual/nix/2.32/store/types/local-daemon-store#store-local-daemon-store-max-connection-age)

  Maximum age of a connection before it is closed.

  **Default:** `4294967295`
* [`max-connections`](https://nix.dev/manual/nix/2.32/store/types/local-daemon-store#store-local-daemon-store-max-connections)

  Maximum number of concurrent connections to the Nix daemon.

  **Default:** `1`
* [`path-info-cache-size`](https://nix.dev/manual/nix/2.32/store/types/local-daemon-store#store-local-daemon-store-path-info-cache-size)

  Size of the in-memory store path metadata cache.

  **Default:** `65536`
* [`priority`](https://nix.dev/manual/nix/2.32/store/types/local-daemon-store#store-local-daemon-store-priority)

  Priority of this store when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).
  A lower value means a higher priority.

  **Default:** `0`
* [`real`](https://nix.dev/manual/nix/2.32/store/types/local-daemon-store#store-local-daemon-store-real)

  Physical path of the Nix store.

  **Default:** `/nix/store`
* [`root`](https://nix.dev/manual/nix/2.32/store/types/local-daemon-store#store-local-daemon-store-root)

  Directory prefixed to all other paths.

  **Default:** ``
* [`state`](https://nix.dev/manual/nix/2.32/store/types/local-daemon-store#store-local-daemon-store-state)

  Directory where Nix stores state.

  **Default:** `/dummy`
* [`store`](https://nix.dev/manual/nix/2.32/store/types/local-daemon-store#store-local-daemon-store-store)

  Logical location of the Nix store, usually
  `/nix/store`. Note that you can only copy store paths
  between stores if they have the same `store` setting.

  **Default:** `/nix/store`
* [`system-features`](https://nix.dev/manual/nix/2.32/store/types/local-daemon-store#store-local-daemon-store-system-features)

  Optional [system features](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-system-features) available on the system this store uses to build derivations.

  Example: `"kvm"`

  **Default:** *machine-specific*
* [`trusted`](https://nix.dev/manual/nix/2.32/store/types/local-daemon-store#store-local-daemon-store-trusted)

  Whether paths from this store can be used as substitutes
  even if they are not signed by a key listed in the
  [`trusted-public-keys`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-trusted-public-keys)
  setting.

  **Default:** `false`
* [`want-mass-query`](https://nix.dev/manual/nix/2.32/store/types/local-daemon-store#store-local-daemon-store-want-mass-query)

  Whether this store can be queried efficiently for path validity when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).

  **Default:** `false`