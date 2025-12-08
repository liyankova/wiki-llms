---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-base32
title: nix hash to-base32 - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix hash to-base32 - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-base32#name)

`nix hash to-base32` - convert a hash to base-32 representation (deprecated, use `nix hash convert` instead)

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-base32#synopsis)

`nix hash to-base32` [*option*...] *strings*...

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-base32#options)

* [`--type`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-base32#opt-type) *hash-algo*

  Hash algorithm (`blake3`, `md5`, `sha1`, `sha256`, or `sha512`). Can be omitted for SRI hashes.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-base32#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-base32#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-base32#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-base32#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-base32#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-base32#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-base32#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-base32#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-base32#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-base32#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-base32#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-base32#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.