---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation
title: nix derivation - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix derivation - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation#name)

`nix derivation` - Work with derivations, Nix's notion of a build plan.

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation#synopsis)

`nix derivation` [*option*...] *subcommand*

where *subcommand* is one of the following:

* [`nix derivation add`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-add) - Add a store derivation
* [`nix derivation show`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show) - show the contents of a store derivation

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation#options)

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.