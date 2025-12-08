---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-remove
title: nix registry remove - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix registry remove - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-remove#name)

`nix registry remove` - remove flake from user flake registry

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-remove#synopsis)

`nix registry remove` [*option*...] *url*

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-remove#examples)

* Remove the entry `nixpkgs` from the user registry:

  ```
  # nix registry remove nixpkgs
  ```
* Remove the entry `nixpkgs` from a custom registry:

  ```
  # nix registry remove --registry ./custom-flake-registry.json nixpkgs
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-remove#description)

This command removes from the user registry any entry for flake
reference *url*.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-remove#options)

* [`--registry`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-remove#opt-registry) *registry*

  The registry to operate on.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-remove#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-remove#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-remove#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-remove#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-remove#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-remove#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-remove#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-remove#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-remove#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-remove#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-remove#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-remove#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.