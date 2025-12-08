---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar
title: nix nar - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix nar - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar#name)

`nix nar` - create or inspect NAR files

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar#synopsis)

`nix nar` [*option*...] *subcommand*

where *subcommand* is one of the following:

* [`nix nar cat`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-cat) - print the contents of a file inside a NAR file on stdout
* [`nix nar dump-path`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-dump-path) - serialise a path to stdout in NAR format
* [`nix nar ls`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls) - show information about a path inside a NAR file
* [`nix nar pack`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-pack) - serialise a path to stdout in NAR format

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar#description)

`nix nar` provides several subcommands for creating and inspecting
[*Nix Archives* (NARs)](https://nix.dev/manual/nix/2.32/store/file-system-object/content-address#serial-nix-archive).

# [File format](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar#file-format)

For the definition of the Nix Archive file format, see
[within the protocols chapter](https://nix.dev/manual/nix/2.32/protocols/nix-archive)
of the manual.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar#options)

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.