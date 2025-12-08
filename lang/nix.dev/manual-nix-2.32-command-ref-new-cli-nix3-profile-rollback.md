---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-rollback
title: nix profile rollback - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix profile rollback - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-rollback#name)

`nix profile rollback` - roll back to the previous version or a specified version of a profile

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-rollback#synopsis)

`nix profile rollback` [*option*...]

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-rollback#examples)

* Roll back your default profile to the previous version:

  ```
  # nix profile rollback
  switching profile from version 519 to 518
  ```
* Switch your default profile to version 510:

  ```
  # nix profile rollback --to 510
  switching profile from version 518 to 510
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-rollback#description)

This command switches a profile to the most recent version older
than the currently active version, or if `--to` *N* is given, to
version *N* of the profile. To see the available versions of a
profile, use `nix profile history`.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-rollback#options)

* [`--dry-run`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-rollback#opt-dry-run)

  Show what this command would do without doing it.
* [`--profile`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-rollback#opt-profile) *path*

  The profile to operate on.
* [`--to`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-rollback#opt-to) *version*

  The profile version to roll back to.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-rollback#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-rollback#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-rollback#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-rollback#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-rollback#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-rollback#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-rollback#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-rollback#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-rollback#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-rollback#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-rollback#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-rollback#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.