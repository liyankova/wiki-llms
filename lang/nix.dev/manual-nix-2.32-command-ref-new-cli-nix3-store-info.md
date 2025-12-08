---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info
title: nix store info - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix store info - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info#name)

`nix store info` - test whether a store can be accessed

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info#synopsis)

`nix store info` [*option*...]

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info#examples)

* Test whether connecting to a remote Nix store via SSH works:

  ```
  # nix store info --store ssh://mac1
  ```
* Test whether a URL is a valid binary cache:

  ```
  # nix store info --store https://cache.nixos.org
  ```
* Test whether the Nix daemon is up and running:

  ```
  # nix store info --store daemon
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info#description)

This command tests whether a particular Nix store (specified by the
argument `--store` *url*) can be accessed. What this means is
dependent on the type of the store. For instance, for an SSH store it
means that Nix can connect to the specified machine.

If the command succeeds, Nix returns a exit code of 0 and does not
print any output.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info#options)

* [`--json`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info#opt-json)

  Produce output in JSON format, suitable for consumption by another program.
* [`--no-pretty`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info#opt-no-pretty)

  Print compact JSON output on a single line, even when the output is a terminal.
  Some commands may print multiple JSON objects on separate lines.

  ```
                See `--pretty`.
  ```
* [`--pretty`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info#opt-pretty)

  Print multi-line, indented JSON output for readability.

  ```
                Default: indent if output is to a terminal.

                This option is only effective when `--json` is also specified.
  ```

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.