---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-diff-closures
title: nix profile diff-closures - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix profile diff-closures - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-diff-closures#name)

`nix profile diff-closures` - show the closure difference between each version of a profile

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-diff-closures#synopsis)

`nix profile diff-closures` [*option*...]

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-diff-closures#examples)

* Show what changed between each version of the NixOS system
  profile:

  ```
  # nix profile diff-closures --profile /nix/var/nix/profiles/system
  Version 13 -> 14:
    acpi-call: 2020-04-07-5.8.13 → 2020-04-07-5.8.14
    aws-sdk-cpp: -6723.1 KiB
    …

  Version 14 -> 15:
    acpi-call: 2020-04-07-5.8.14 → 2020-04-07-5.8.16
    attica: -996.2 KiB
    breeze-icons: -78713.5 KiB
    brotli: 1.0.7 → 1.0.9, +44.2 KiB
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-diff-closures#description)

This command shows the difference between the closures of subsequent
versions of a profile. See [`nix store diff-closures`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures) for details.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-diff-closures#options)

* [`--profile`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-diff-closures#opt-profile) *path*

  The profile to operate on.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-diff-closures#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-diff-closures#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-diff-closures#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-diff-closures#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-diff-closures#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-diff-closures#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-diff-closures#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-diff-closures#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-diff-closures#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-diff-closures#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-diff-closures#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-diff-closures#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.