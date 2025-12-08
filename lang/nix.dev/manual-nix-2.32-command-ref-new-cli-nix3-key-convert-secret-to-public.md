---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-convert-secret-to-public
title: nix key convert-secret-to-public - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix key convert-secret-to-public - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-convert-secret-to-public#name)

`nix key convert-secret-to-public` - generate a public key for verifying store paths from a secret key read from standard input

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-convert-secret-to-public#synopsis)

`nix key convert-secret-to-public` [*option*...]

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-convert-secret-to-public#examples)

* Convert a secret key to a public key:

  ```
  # echo cache.example.org-0:E7lAO+MsPwTFfPXsdPtW8GKui/5ho4KQHVcAGnX+Tti1V4dUxoVoqLyWJ4YESuZJwQ67GVIksDt47og+tPVUZw== \
    | nix key convert-secret-to-public
  cache.example.org-0:tVeHVMaFaKi8lieGBErmScEOuxlSJLA7eO6IPrT1VGc=
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-convert-secret-to-public#description)

This command reads a Ed25519 secret key from standard input, and
writes the corresponding public key to standard output. For more
details, see [nix key generate-secret](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-generate-secret).

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-convert-secret-to-public#options)

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-convert-secret-to-public#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-convert-secret-to-public#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-convert-secret-to-public#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-convert-secret-to-public#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-convert-secret-to-public#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-convert-secret-to-public#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-convert-secret-to-public#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-convert-secret-to-public#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-convert-secret-to-public#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-convert-secret-to-public#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-convert-secret-to-public#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-convert-secret-to-public#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.