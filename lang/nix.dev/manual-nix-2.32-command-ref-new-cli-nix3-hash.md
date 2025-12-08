---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash
title: nix hash - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix hash - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash#name)

`nix hash` - compute and convert cryptographic hashes

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash#synopsis)

`nix hash` [*option*...] *subcommand*

where *subcommand* is one of the following:

**Available commands:**

* [`nix hash file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-file) - print cryptographic hash of a regular file
* [`nix hash path`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path) - print cryptographic hash of the NAR serialisation of a path
* [`nix hash to-base16`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-base16) - convert a hash to base-16 representation (deprecated, use `nix hash convert` instead)
* [`nix hash to-base32`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-base32) - convert a hash to base-32 representation (deprecated, use `nix hash convert` instead)
* [`nix hash to-base64`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-base64) - convert a hash to base-64 representation (deprecated, use `nix hash convert` instead)
* [`nix hash to-sri`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-to-sri) - convert a hash to SRI representation (deprecated, use `nix hash convert` instead)

**:**

* [`nix hash convert`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-convert) - convert between hash formats

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash#options)

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.