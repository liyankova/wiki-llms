---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-optimise
title: nix store optimise - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix store optimise - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-optimise#name)

`nix store optimise` - replace identical files in the store by hard links

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-optimise#synopsis)

`nix store optimise` [*option*...]

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-optimise#examples)

* Optimise the Nix store:

  ```
  nix store optimise
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-optimise#description)

This command deduplicates the Nix store: it scans the store for
regular files with identical contents, and replaces them with hard
links to a single instance.

Note that you can also set `auto-optimise-store` to `true` in
`nix.conf` to perform this optimisation incrementally whenever a new
path is added to the Nix store. To make this efficient, Nix maintains
a content-addressed index of all the files in the Nix store in the
directory `/nix/store/.links/`.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-optimise#options)

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-optimise#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-optimise#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-optimise#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-optimise#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-optimise#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-optimise#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-optimise#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-optimise#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-optimise#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-optimise#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-optimise#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-optimise#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.