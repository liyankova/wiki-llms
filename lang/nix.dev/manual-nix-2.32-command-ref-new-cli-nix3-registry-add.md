---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add
title: nix registry add - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix registry add - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#name)

`nix registry add` - add/replace flake in user flake registry

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#synopsis)

`nix registry add` [*option*...] *from-url* *to-url*

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#examples)

* Set the `nixpkgs` flake identifier to a specific branch of Nixpkgs:

  ```
  # nix registry add nixpkgs github:NixOS/nixpkgs/nixos-20.03
  ```
* Pin `nixpkgs` to a specific revision:

  ```
  # nix registry add nixpkgs github:NixOS/nixpkgs/925b70cd964ceaedee26fde9b19cc4c4f081196a
  ```
* Add an entry that redirects a specific branch of `nixpkgs` to
  another fork:

  ```
  # nix registry add nixpkgs/nixos-20.03 ~/Dev/nixpkgs
  ```
* Add `nixpkgs` pointing to `github:nixos/nixpkgs` to your custom flake
  registry:

  ```
  nix registry add --registry ./custom-flake-registry.json nixpkgs github:nixos/nixpkgs
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#description)

This command adds an entry to the user registry that maps flake
reference *from-url* to flake reference *to-url*. If an entry for
*from-url* already exists, it is overwritten.

Entries can be removed using [`nix registry remove`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-remove).

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#options)

* [`--registry`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#opt-registry) *registry*

  The registry to operate on.

## [Common evaluation options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#common-evaluation-options)

* [`--arg`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#opt-arg) *name* *expr*

  Pass the value *expr* as the argument *name* to Nix functions.
* [`--arg-from-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#opt-arg-from-file) *name* *path*

  Pass the contents of file *path* as the argument *name* to Nix functions.
* [`--arg-from-stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#opt-arg-from-stdin) *name*

  Pass the contents of stdin as the argument *name* to Nix functions.
* [`--argstr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#opt-argstr) *name* *string*

  Pass the string *string* as the argument *name* to Nix functions.
* [`--eval-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#opt-eval-store) *store-url*

  The [URL of the Nix store](https://nix.dev/manual/nix/2.32/store/types/#store-url-format)
  to use for evaluation, i.e. to store derivations (`.drv` files) and inputs referenced by them.
* [`--impure`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#opt-impure)

  Allow access to mutable paths and repositories.
* [`--include`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#opt-include) / `-I` *path*

  Add *path* to search path entries used to resolve [lookup paths](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path)

  This option may be given multiple times.

  Paths added through `-I` take precedence over the [`nix-path` configuration setting](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-nix-path) and the [`NIX_PATH` environment variable](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_PATH).
* [`--override-flake`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#opt-override-flake) *original-ref* *resolved-ref*

  Override the flake registries, redirecting *original-ref* to *resolved-ref*.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--repair`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#opt-repair)

  During evaluation, rewrite missing or corrupted files in the Nix store. During building, rebuild missing or corrupted store paths.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-add#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.