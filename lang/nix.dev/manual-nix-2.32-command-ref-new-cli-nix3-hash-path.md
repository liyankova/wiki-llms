---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path
title: nix hash path - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix hash path - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#name)

`nix hash path` - print cryptographic hash of the NAR serialisation of a path

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#synopsis)

`nix hash path` [*option*...] *paths*...

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#options)

* [`--algo`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#opt-algo) *hash-algo*

  Hash algorithm (`blake3`, `md5`, `sha1`, `sha256`, or `sha512`).
* [`--base16`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#opt-base16)

  Print the hash in base-16 format.
* [`--base32`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#opt-base32)

  Print the hash in base-32 (Nix-specific) format.
* [`--base64`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#opt-base64)

  Print the hash in base-64 format.
* [`--format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#opt-format) *hash-format*

  Hash format (`base16`, `nix32`, `base64`, `sri`). Default: `sri`.
* [`--mode`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#opt-mode) *file-ingestion-method*

  How to compute the hash of the input.
  One of:

  + `nar` (the default):
    Serialises the input as a
    [Nix Archive](https://nix.dev/manual/nix/2.32/store/file-system-object/content-address#serial-nix-archive)
    and passes that to the hash function.
  + `flat`:
    Assumes that the input is a single file and
    [directly passes](https://nix.dev/manual/nix/2.32/store/file-system-object/content-address#serial-flat)
    it to the hash function.
* [`--sri`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#opt-sri)

  Print the hash in SRI format.
* [`--type`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#opt-type) *hash-algo*

  Hash algorithm (`blake3`, `md5`, `sha1`, `sha256`, or `sha512`).

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-hash-path#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.