---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file
title: nix hash file - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix hash file - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file#name)

`nix hash file` - print cryptographic hash of a regular file

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file#synopsis)

`nix hash file` [*option*...] *paths*...

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file#options)

* [`--base16`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file#opt-base16)

  Print the hash in base-16 format.
* [`--base32`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file#opt-base32)

  Print the hash in base-32 (Nix-specific) format.
* [`--base64`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file#opt-base64)

  Print the hash in base-64 format.
* [`--sri`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file#opt-sri)

  Print the hash in SRI format.
* [`--type`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file#opt-type) *hash-algo*

  Hash algorithm (`blake3`, `md5`, `sha1`, `sha256`, or `sha512`).

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.