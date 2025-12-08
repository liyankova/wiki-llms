---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-wipe-history
title: nix profile wipe-history - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix profile wipe-history - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-wipe-history#name)

`nix profile wipe-history` - delete non-current versions of a profile

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-wipe-history#synopsis)

`nix profile wipe-history` [*option*...]

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-wipe-history#examples)

* Delete all versions of the default profile older than 100 days:

  ```
  # nix profile wipe-history --profile /tmp/profile --older-than 100d
  removing profile version 515
  removing profile version 514
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-wipe-history#description)

This command deletes non-current versions of a profile, making it
impossible to roll back to these versions. By default, all non-current
versions are deleted. With `--older-than` *N*`d`, all non-current
versions older than *N* days are deleted.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-wipe-history#options)

* [`--dry-run`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-wipe-history#opt-dry-run)

  Show what this command would do without doing it.
* [`--older-than`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-wipe-history#opt-older-than) *age*

  Delete versions older than the specified age. *age* must be in the format *N*`d`, where *N* denotes a number of days.
* [`--profile`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-wipe-history#opt-profile) *path*

  The profile to operate on.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-wipe-history#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-wipe-history#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-wipe-history#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-wipe-history#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-wipe-history#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-wipe-history#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-wipe-history#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-wipe-history#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-wipe-history#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-wipe-history#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-wipe-history#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-wipe-history#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.