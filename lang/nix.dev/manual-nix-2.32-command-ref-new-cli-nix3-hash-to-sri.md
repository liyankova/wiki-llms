---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-sri
title: nix hash to-sri - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix hash to-sri - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-sri#name)

`nix hash to-sri` - convert a hash to SRI representation (deprecated, use `nix hash convert` instead)

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-sri#synopsis)

`nix hash to-sri` [*option*...] *strings*...

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-sri#options)

* [`--type`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-sri#opt-type) *hash-algo*

  Hash algorithm (`blake3`, `md5`, `sha1`, `sha256`, or `sha512`). Can be omitted for SRI hashes.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-sri#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-sri#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-sri#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-sri#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-sri#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-sri#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-sri#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-sri#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-sri#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-sri#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-sri#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-sri#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.