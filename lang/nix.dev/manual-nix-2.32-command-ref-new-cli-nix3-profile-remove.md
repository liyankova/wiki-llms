---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove
title: nix profile remove - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix profile remove - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#name)

`nix profile remove` - remove packages from a profile

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#synopsis)

`nix profile remove` [*option*...] *elements*...

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#examples)

* Remove a package by name:

  ```
  # nix profile remove hello
  ```
* Remove all packages:

  ```
  # nix profile remove --all
  ```
* Remove packages by regular expression:

  ```
  # nix profile remove --regex '.*vim.*'
  ```
* Remove a package by store path:

  ```
  # nix profile remove /nix/store/rr3y0c6zyk7kjjl8y19s4lsrhn4aiq1z-hello-2.10
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#description)

This command removes a package from a profile.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#options)

* [`--all`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-all)

  Match all packages in the profile.
* [`--profile`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-profile) *path*

  The profile to operate on.
* [`--regex`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-regex) *pattern*

  A regular expression to match one or more packages in the profile.

## [Common evaluation options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#common-evaluation-options)

* [`--arg`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-arg) *name* *expr*

  Pass the value *expr* as the argument *name* to Nix functions.
* [`--arg-from-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-arg-from-file) *name* *path*

  Pass the contents of file *path* as the argument *name* to Nix functions.
* [`--arg-from-stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-arg-from-stdin) *name*

  Pass the contents of stdin as the argument *name* to Nix functions.
* [`--argstr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-argstr) *name* *string*

  Pass the string *string* as the argument *name* to Nix functions.
* [`--debugger`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-debugger)

  Start an interactive environment if evaluation fails.
* [`--eval-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-eval-store) *store-url*

  The [URL of the Nix store](https://nix.dev/manual/nix/2.32/store/types/#store-url-format)
  to use for evaluation, i.e. to store derivations (`.drv` files) and inputs referenced by them.
* [`--impure`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-impure)

  Allow access to mutable paths and repositories.
* [`--include`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-include) / `-I` *path*

  Add *path* to search path entries used to resolve [lookup paths](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path)

  This option may be given multiple times.

  Paths added through `-I` take precedence over the [`nix-path` configuration setting](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-nix-path) and the [`NIX_PATH` environment variable](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_PATH).
* [`--override-flake`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-override-flake) *original-ref* *resolved-ref*

  Override the flake registries, redirecting *original-ref* to *resolved-ref*.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--repair`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-repair)

  During evaluation, rewrite missing or corrupted files in the Nix store. During building, rebuild missing or corrupted store paths.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-remove#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.