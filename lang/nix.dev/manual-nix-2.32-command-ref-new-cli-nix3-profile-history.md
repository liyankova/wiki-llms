---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history
title: nix profile history - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix profile history - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#name)

`nix profile history` - show all versions of a profile

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#synopsis)

`nix profile history` [*option*...]

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#examples)

* Show the changes between each version of your default profile:

  ```
  # nix profile history
  Version 508 (2020-04-10):
    flake:nixpkgs#legacyPackages.x86_64-linux.awscli: ∅ -> 1.17.13

  Version 509 (2020-05-16) <- 508:
    flake:nixpkgs#legacyPackages.x86_64-linux.awscli: 1.17.13 -> 1.18.211
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#description)

This command shows what packages were added, removed or upgraded
between subsequent versions of a profile. It only shows top-level
packages, not dependencies; for that, use [`nix profile diff-closures`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-diff-closures).

The addition of a package to a profile is denoted by the string `∅ ->`
*version*, whereas the removal is denoted by *version* `-> ∅`.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#options)

* [`--profile`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#opt-profile) *path*

  The profile to operate on.

## [Common evaluation options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#common-evaluation-options)

* [`--arg`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#opt-arg) *name* *expr*

  Pass the value *expr* as the argument *name* to Nix functions.
* [`--arg-from-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#opt-arg-from-file) *name* *path*

  Pass the contents of file *path* as the argument *name* to Nix functions.
* [`--arg-from-stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#opt-arg-from-stdin) *name*

  Pass the contents of stdin as the argument *name* to Nix functions.
* [`--argstr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#opt-argstr) *name* *string*

  Pass the string *string* as the argument *name* to Nix functions.
* [`--debugger`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#opt-debugger)

  Start an interactive environment if evaluation fails.
* [`--eval-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#opt-eval-store) *store-url*

  The [URL of the Nix store](https://nix.dev/manual/nix/2.32/store/types/#store-url-format)
  to use for evaluation, i.e. to store derivations (`.drv` files) and inputs referenced by them.
* [`--impure`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#opt-impure)

  Allow access to mutable paths and repositories.
* [`--include`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#opt-include) / `-I` *path*

  Add *path* to search path entries used to resolve [lookup paths](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path)

  This option may be given multiple times.

  Paths added through `-I` take precedence over the [`nix-path` configuration setting](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-nix-path) and the [`NIX_PATH` environment variable](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_PATH).
* [`--override-flake`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#opt-override-flake) *original-ref* *resolved-ref*

  Override the flake registries, redirecting *original-ref* to *resolved-ref*.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--repair`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#opt-repair)

  During evaluation, rewrite missing or corrupted files in the Nix store. During building, rebuild missing or corrupted store paths.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-profile-history#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.