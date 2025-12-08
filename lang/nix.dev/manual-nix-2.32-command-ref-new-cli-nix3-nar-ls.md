---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls
title: nix nar ls - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix nar ls - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#name)

`nix nar ls` - show information about a path inside a NAR file

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#synopsis)

`nix nar ls` [*option*...] *nar* *path*

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#examples)

* To list a specific file in a [NAR](https://nix.dev/manual/nix/2.32/store/file-system-object/content-address#serial-nix-archive):

  ```
  # nix nar ls --long ./hello.nar /bin/hello
  -r-xr-xr-x                38184 hello
  ```
* To recursively list the contents of a directory inside a NAR, in JSON
  format:

  ```
  # nix nar ls --json --recursive ./hello.nar /bin
  {"type":"directory","entries":{"hello":{"type":"regular","size":38184,"executable":true,"narOffset":400}}}
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#description)

This command shows information about a *path* inside [Nix Archive (NAR)](https://nix.dev/manual/nix/2.32/store/file-system-object/content-address#serial-nix-archive) file *nar*.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#options)

* [`--directory`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#opt-directory) / `-d`

  Show directories rather than their contents.
* [`--json`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#opt-json)

  Produce output in JSON format, suitable for consumption by another program.
* [`--long`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#opt-long) / `-l`

  Show detailed file information.
* [`--no-pretty`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#opt-no-pretty)

  Print compact JSON output on a single line, even when the output is a terminal.
  Some commands may print multiple JSON objects on separate lines.

  ```
                See `--pretty`.
  ```
* [`--pretty`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#opt-pretty)

  Print multi-line, indented JSON output for readability.

  ```
                Default: indent if output is to a terminal.

                This option is only effective when `--json` is also specified.
  ```
* [`--recursive`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#opt-recursive) / `-R`

  List subdirectories recursively.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-nar-ls#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.