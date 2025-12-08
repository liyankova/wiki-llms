---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list
title: nix profile list - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix profile list - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#name)

`nix profile list` - list packages in the profile

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#synopsis)

`nix profile list` [*option*...]

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#examples)

* Show what packages are installed in the default profile:

  ```
  # nix profile list
  Name:               gdb
  Flake attribute:    legacyPackages.x86_64-linux.gdb
  Original flake URL: flake:nixpkgs
  Locked flake URL:   github:NixOS/nixpkgs/7b38b03d76ab71bdc8dc325e3f6338d984cc35ca
  Store paths:        /nix/store/indzcw5wvlhx6vwk7k4iq29q15chvr3d-gdb-11.1

  Name:               blender-bin
  Flake attribute:    packages.x86_64-linux.default
  Original flake URL: flake:blender-bin
  Locked flake URL:   github:edolstra/nix-warez/91f2ffee657bf834e4475865ae336e2379282d34?dir=blender
  Store paths:        /nix/store/i798sxl3j40wpdi1rgf391id1b5klw7g-blender-bin-3.1.2
  ```

  Note that you can unambiguously rebuild a package from a profile
  through its locked flake URL and flake attribute, e.g.

  ```
  # nix build github:edolstra/nix-warez/91f2ffee657bf834e4475865ae336e2379282d34?dir=blender#packages.x86_64-linux.default
  ```

  will build the package `blender-bin` shown above.

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#description)

This command shows what packages are currently installed in a
profile. For each installed package, it shows the following
information:

* `Name`: A unique name used to unambiguously identify the
  package in invocations of `nix profile remove` and `nix profile upgrade`.
* `Index`: An integer that can be used to unambiguously identify the
  package in invocations of `nix profile remove` and `nix profile upgrade`.
  (*Deprecated, will be removed in a future version in favor of `Name`.*)
* `Flake attribute`: The flake output attribute path that provides the
  package (e.g. `packages.x86_64-linux.hello`).
* `Original flake URL`: The original ("unlocked") flake reference
  specified by the user when the package was first installed via `nix profile install`.
* `Locked flake URL`: The locked flake reference to which the original
  flake reference was resolved.
* `Store paths`: The store path(s) of the package.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#options)

* [`--json`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-json)

  Produce output in JSON format, suitable for consumption by another program.
* [`--no-pretty`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-no-pretty)

  Print compact JSON output on a single line, even when the output is a terminal.
  Some commands may print multiple JSON objects on separate lines.

  ```
                See `--pretty`.
  ```
* [`--pretty`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-pretty)

  Print multi-line, indented JSON output for readability.

  ```
                Default: indent if output is to a terminal.

                This option is only effective when `--json` is also specified.
  ```
* [`--profile`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-profile) *path*

  The profile to operate on.

## [Common evaluation options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#common-evaluation-options)

* [`--arg`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-arg) *name* *expr*

  Pass the value *expr* as the argument *name* to Nix functions.
* [`--arg-from-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-arg-from-file) *name* *path*

  Pass the contents of file *path* as the argument *name* to Nix functions.
* [`--arg-from-stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-arg-from-stdin) *name*

  Pass the contents of stdin as the argument *name* to Nix functions.
* [`--argstr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-argstr) *name* *string*

  Pass the string *string* as the argument *name* to Nix functions.
* [`--debugger`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-debugger)

  Start an interactive environment if evaluation fails.
* [`--eval-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-eval-store) *store-url*

  The [URL of the Nix store](https://nix.dev/manual/nix/2.32/store/types/#store-url-format)
  to use for evaluation, i.e. to store derivations (`.drv` files) and inputs referenced by them.
* [`--impure`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-impure)

  Allow access to mutable paths and repositories.
* [`--include`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-include) / `-I` *path*

  Add *path* to search path entries used to resolve [lookup paths](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path)

  This option may be given multiple times.

  Paths added through `-I` take precedence over the [`nix-path` configuration setting](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-nix-path) and the [`NIX_PATH` environment variable](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_PATH).
* [`--override-flake`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-override-flake) *original-ref* *resolved-ref*

  Override the flake registries, redirecting *original-ref* to *resolved-ref*.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--repair`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-repair)

  During evaluation, rewrite missing or corrupted files in the Nix store. During building, rebuild missing or corrupted store paths.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-list#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.