---
url: https://nix.dev/manual/nix/2.32/store/types/ssh-store
title: SSH Store - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# SSH Store - Nix 2.32.2 Reference Manual

# [SSH Store](https://nix.dev/manual/nix/2.32/store/types/ssh-store#ssh-store)

**Store URL format**: `ssh://[username@]hostname[:port]`

This store type allows limited access to a remote store on another
machine via SSH.

## [Settings](https://nix.dev/manual/nix/2.32/store/types/ssh-store#settings)

* [`base64-ssh-public-host-key`](https://nix.dev/manual/nix/2.32/store/types/ssh-store#store-ssh-store-base64-ssh-public-host-key)

  The public host key of the remote machine.

  **Default:** *empty*
* [`compress`](https://nix.dev/manual/nix/2.32/store/types/ssh-store#store-ssh-store-compress)

  Whether to enable SSH compression.

  **Default:** `false`
* [`log-fd`](https://nix.dev/manual/nix/2.32/store/types/ssh-store#store-ssh-store-log-fd)

  file descriptor to which SSH's stderr is connected

  **Default:** `-1`
* [`max-connections`](https://nix.dev/manual/nix/2.32/store/types/ssh-store#store-ssh-store-max-connections)

  Maximum number of concurrent SSH connections.

  **Default:** `1`
* [`path-info-cache-size`](https://nix.dev/manual/nix/2.32/store/types/ssh-store#store-ssh-store-path-info-cache-size)

  Size of the in-memory store path metadata cache.

  **Default:** `65536`
* [`priority`](https://nix.dev/manual/nix/2.32/store/types/ssh-store#store-ssh-store-priority)

  Priority of this store when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).
  A lower value means a higher priority.

  **Default:** `0`
* [`remote-program`](https://nix.dev/manual/nix/2.32/store/types/ssh-store#store-ssh-store-remote-program)

  Path to the `nix-store` executable on the remote machine.

  **Default:** `nix-store`
* [`remote-store`](https://nix.dev/manual/nix/2.32/store/types/ssh-store#store-ssh-store-remote-store)

  [Store URL](https://nix.dev/manual/nix/2.32/store/types/#store-url-format)
  to be used on the remote machine. The default is `auto`
  (i.e. use the Nix daemon or `/nix/store` directly).

  **Default:** *empty*
* [`ssh-key`](https://nix.dev/manual/nix/2.32/store/types/ssh-store#store-ssh-store-ssh-key)

  Path to the SSH private key used to authenticate to the remote machine.

  **Default:** *empty*
* [`store`](https://nix.dev/manual/nix/2.32/store/types/ssh-store#store-ssh-store-store)

  Logical location of the Nix store, usually
  `/nix/store`. Note that you can only copy store paths
  between stores if they have the same `store` setting.

  **Default:** `/nix/store`
* [`system-features`](https://nix.dev/manual/nix/2.32/store/types/ssh-store#store-ssh-store-system-features)

  Optional [system features](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-system-features) available on the system this store uses to build derivations.

  Example: `"kvm"`

  **Default:** *machine-specific*
* [`trusted`](https://nix.dev/manual/nix/2.32/store/types/ssh-store#store-ssh-store-trusted)

  Whether paths from this store can be used as substitutes
  even if they are not signed by a key listed in the
  [`trusted-public-keys`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-trusted-public-keys)
  setting.

  **Default:** `false`
* [`want-mass-query`](https://nix.dev/manual/nix/2.32/store/types/ssh-store#store-ssh-store-want-mass-query)

  Whether this store can be queried efficiently for path validity when used as a [substituter](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters).

  **Default:** `false`