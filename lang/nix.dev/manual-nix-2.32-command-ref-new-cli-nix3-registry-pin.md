---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin
title: nix registry pin - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix registry pin - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#name)

`nix registry pin` - pin a flake to its current version or to the current version of a flake URL

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#synopsis)

`nix registry pin` [*option*...] *url* *locked*

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#examples)

* Pin `nixpkgs` to its most recent Git revision:

  ```
  # nix registry pin nixpkgs
  ```

  Afterwards the user registry will have an entry like this:

  ```
  nix registry list | grep '^user '
  user   flake:nixpkgs github:NixOS/nixpkgs/925b70cd964ceaedee26fde9b19cc4c4f081196a
  ```

  and `nix flake metadata` will say:

  ```
  # nix flake metadata nixpkgs
  Resolved URL:  github:NixOS/nixpkgs/925b70cd964ceaedee26fde9b19cc4c4f081196a
  Locked URL:    github:NixOS/nixpkgs/925b70cd964ceaedee26fde9b19cc4c4f081196a
  …
  ```
* Pin `nixpkgs` in a custom registry to its most recent Git revision:

  ```
  # nix registry pin --registry ./custom-flake-registry.json nixpkgs
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#description)

This command adds an entry to the user registry that maps flake
reference *url* to the corresponding *locked* flake reference, that
is, a flake reference that specifies an exact revision or content
hash. This ensures that until this registry entry is removed, all uses
of *url* will resolve to exactly the same flake.

Entries can be removed using [`nix registry remove`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-remove).

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#options)

* [`--registry`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#opt-registry) *registry*

  The registry to operate on.

## [Common evaluation options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#common-evaluation-options)

* [`--arg`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#opt-arg) *name* *expr*

  Pass the value *expr* as the argument *name* to Nix functions.
* [`--arg-from-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#opt-arg-from-file) *name* *path*

  Pass the contents of file *path* as the argument *name* to Nix functions.
* [`--arg-from-stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#opt-arg-from-stdin) *name*

  Pass the contents of stdin as the argument *name* to Nix functions.
* [`--argstr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#opt-argstr) *name* *string*

  Pass the string *string* as the argument *name* to Nix functions.
* [`--debugger`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#opt-debugger)

  Start an interactive environment if evaluation fails.
* [`--eval-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#opt-eval-store) *store-url*

  The [URL of the Nix store](https://nix.dev/manual/nix/2.32/store/types/#store-url-format)
  to use for evaluation, i.e. to store derivations (`.drv` files) and inputs referenced by them.
* [`--impure`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#opt-impure)

  Allow access to mutable paths and repositories.
* [`--include`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#opt-include) / `-I` *path*

  Add *path* to search path entries used to resolve [lookup paths](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path)

  This option may be given multiple times.

  Paths added through `-I` take precedence over the [`nix-path` configuration setting](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-nix-path) and the [`NIX_PATH` environment variable](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_PATH).
* [`--override-flake`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#opt-override-flake) *original-ref* *resolved-ref*

  Override the flake registries, redirecting *original-ref* to *resolved-ref*.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--repair`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#opt-repair)

  During evaluation, rewrite missing or corrupted files in the Nix store. During building, rebuild missing or corrupted store paths.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-pin#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.