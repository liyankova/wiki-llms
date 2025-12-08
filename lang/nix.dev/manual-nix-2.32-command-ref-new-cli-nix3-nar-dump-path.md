---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-dump-path
title: nix nar dump-path - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix nar dump-path - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-dump-path#name)

`nix nar dump-path` - serialise a path to stdout in NAR format

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-dump-path#synopsis)

`nix nar dump-path` [*option*...] *path*

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-dump-path#examples)

* To serialise directory `foo` as a [Nix Archive (NAR)](https://nix.dev/manual/nix/2.32/store/file-system-object/content-address#serial-nix-archive):

  ```
  # nix nar pack ./foo > foo.nar
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-dump-path#description)

This command generates a [Nix Archive (NAR)](https://nix.dev/manual/nix/2.32/store/file-system-object/content-address#serial-nix-archive) file containing the serialisation of
*path*, which must contain only regular files, directories and
symbolic links. The NAR is written to standard output.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-dump-path#options)

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-dump-path#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-dump-path#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-dump-path#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-dump-path#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-dump-path#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-dump-path#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-dump-path#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-dump-path#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-dump-path#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-dump-path#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-dump-path#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-dump-path#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.