---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-upgrade-nix
title: nix upgrade-nix - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix upgrade-nix - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-upgrade-nix#name)

`nix upgrade-nix` - upgrade Nix to the latest stable version

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-upgrade-nix#synopsis)

`nix upgrade-nix` [*option*...]

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-upgrade-nix#examples)

* Upgrade Nix to the stable version declared in Nixpkgs:

  ```
  # nix upgrade-nix
  ```
* Upgrade Nix in a specific profile:

  ```
  # nix upgrade-nix --profile ~alice/.local/state/nix/profiles/profile
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-upgrade-nix#description)

This command upgrades Nix to the stable version.

By default, the latest stable version is defined by Nixpkgs, in
[nix-fallback-paths.nix](https://github.com/NixOS/nixpkgs/raw/master/nixos/modules/installer/tools/nix-fallback-paths.nix)
and updated manually. It may not always be the latest tagged release.

By default, it locates the directory containing the `nix` binary in the `$PATH`
environment variable. If that directory is a Nix profile, it will
upgrade the `nix` package in that profile to the latest stable binary
release.

You cannot use this command to upgrade Nix in the system profile of a
NixOS system (that is, if `nix` is found in `/run/current-system`).

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-upgrade-nix#options)

* [`--dry-run`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-upgrade-nix#opt-dry-run)

  Show what this command would do without doing it.
* [`--nix-store-paths-url`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-upgrade-nix#opt-nix-store-paths-url) *url*

  The URL of the file that contains the store paths of the latest Nix release.
* [`--profile`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-upgrade-nix#opt-profile) / `-p` *profile-dir*

  The path to the Nix profile to upgrade.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-upgrade-nix#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-upgrade-nix#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-upgrade-nix#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-upgrade-nix#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-upgrade-nix#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-upgrade-nix#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-upgrade-nix#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-upgrade-nix#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-upgrade-nix#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-upgrade-nix#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-upgrade-nix#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-upgrade-nix#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.