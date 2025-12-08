---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-path-from-hash-part
title: nix store path-from-hash-part - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix store path-from-hash-part - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-path-from-hash-part#name)

`nix store path-from-hash-part` - get a store path from its hash part

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-path-from-hash-part#synopsis)

`nix store path-from-hash-part` [*option*...] *hash-part*

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-path-from-hash-part#examples)

* Return the full store path with the given hash part:

  ```
  # nix store path-from-hash-part --store https://cache.nixos.org/ 0i2jd68mp5g6h2sa5k9c85rb80sn8hi9
  /nix/store/0i2jd68mp5g6h2sa5k9c85rb80sn8hi9-hello-2.10
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-path-from-hash-part#description)

Given the hash part of a store path (that is, the 32 characters
following `/nix/store/`), return the full store path. This is
primarily useful in the implementation of binary caches, where a
request for a `.narinfo` file only supplies the hash part
(e.g. `https://cache.nixos.org/0i2jd68mp5g6h2sa5k9c85rb80sn8hi9.narinfo`).

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-path-from-hash-part#options)

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-path-from-hash-part#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-path-from-hash-part#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-path-from-hash-part#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-path-from-hash-part#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-path-from-hash-part#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-path-from-hash-part#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-path-from-hash-part#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-path-from-hash-part#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-path-from-hash-part#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-path-from-hash-part#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-path-from-hash-part#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-path-from-hash-part#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.