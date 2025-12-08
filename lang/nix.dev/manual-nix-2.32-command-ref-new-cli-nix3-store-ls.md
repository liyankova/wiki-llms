---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls
title: nix store ls - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix store ls - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#name)

`nix store ls` - show information about a path in the Nix store

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#synopsis)

`nix store ls` [*option*...] *path*

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#examples)

* To list the contents of a store path in a binary cache:

  ```
  # nix store ls --store https://cache.nixos.org/ --long --recursive /nix/store/0i2jd68mp5g6h2sa5k9c85rb80sn8hi9-hello-2.10
  dr-xr-xr-x                    0 ./bin
  -r-xr-xr-x                38184 ./bin/hello
  dr-xr-xr-x                    0 ./share
  …
  ```
* To show information about a specific file in a binary cache:

  ```
  # nix store ls --store https://cache.nixos.org/ --long /nix/store/0i2jd68mp5g6h2sa5k9c85rb80sn8hi9-hello-2.10/bin/hello
  -r-xr-xr-x                38184 hello
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#description)

This command shows information about *path* in a Nix store. *path* can
be a top-level store path or any file inside a store path.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#options)

* [`--directory`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#opt-directory) / `-d`

  Show directories rather than their contents.
* [`--json`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#opt-json)

  Produce output in JSON format, suitable for consumption by another program.
* [`--long`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#opt-long) / `-l`

  Show detailed file information.
* [`--no-pretty`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#opt-no-pretty)

  Print compact JSON output on a single line, even when the output is a terminal.
  Some commands may print multiple JSON objects on separate lines.

  ```
                See `--pretty`.
  ```
* [`--pretty`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#opt-pretty)

  Print multi-line, indented JSON output for readability.

  ```
                Default: indent if output is to a terminal.

                This option is only effective when `--json` is also specified.
  ```
* [`--recursive`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#opt-recursive) / `-R`

  List subdirectories recursively.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.