---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update
title: nix flake update - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix flake update - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#name)

`nix flake update` - update flake lock file

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#synopsis)

`nix flake update` [*option*...] *inputs*...

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#examples)

* Update all inputs (i.e. recreate the lock file from scratch):

  ```
  # nix flake update
  warning: updating lock file '/home/myself/repos/testflake/flake.lock':
  • Updated input 'nix':
      'github:NixOS/nix/9fab14adbc3810d5cc1f88672fde1eee4358405c' (2023-06-28)
    → 'github:NixOS/nix/8927cba62f5afb33b01016d5c4f7f8b7d0adde3c' (2023-07-11)
  • Updated input 'nixpkgs':
      'github:NixOS/nixpkgs/3d2d8f281a27d466fa54b469b5993f7dde198375' (2023-06-30)
    → 'github:NixOS/nixpkgs/a3a3dda3bacf61e8a39258a0ed9c924eeca8e293' (2023-07-05)
  ```
* Update only a single input:

  ```
  # nix flake update nixpkgs
  warning: updating lock file '/home/myself/repos/testflake/flake.lock':
  • Updated input 'nixpkgs':
      'github:NixOS/nixpkgs/3d2d8f281a27d466fa54b469b5993f7dde198375' (2023-06-30)
    → 'github:NixOS/nixpkgs/a3a3dda3bacf61e8a39258a0ed9c924eeca8e293' (2023-07-05)
  ```
* Update multiple inputs:

  ```
  # nix flake update nixpkgs nixpkgs-unstable
  warning: updating lock file '/home/myself/repos/testflake/flake.lock':
  • Updated input 'nixpkgs':
      'github:nixos/nixpkgs/8f7492cce28977fbf8bd12c72af08b1f6c7c3e49' (2024-09-14)
    → 'github:nixos/nixpkgs/086b448a5d54fd117f4dc2dee55c9f0ff461bdc1' (2024-09-16)
  • Updated input 'nixpkgs-unstable':
      'github:nixos/nixpkgs/345c263f2f53a3710abe117f28a5cb86d0ba4059' (2024-09-13)
    → 'github:nixos/nixpkgs/99dc8785f6a0adac95f5e2ab05cc2e1bf666d172' (2024-09-16)
  ```
* Update only a single input of a flake in a different directory:

  ```
  # nix flake update nixpkgs --flake ~/repos/another
  warning: updating lock file '/home/myself/repos/another/flake.lock':
  • Updated input 'nixpkgs':
      'github:NixOS/nixpkgs/3d2d8f281a27d466fa54b469b5993f7dde198375' (2023-06-30)
    → 'github:NixOS/nixpkgs/a3a3dda3bacf61e8a39258a0ed9c924eeca8e293' (2023-07-05)
  ```

  > **Note**
  >
  > When trying to refer to a flake in a subdirectory, write `./another`
  > instead of `another`.
  > Otherwise Nix will try to look up the flake in the registry.

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#description)

This command updates the inputs in a lock file (`flake.lock`).
**By default, all inputs are updated**. If the lock file doesn't exist
yet, it will be created. If inputs are not in the lock file yet, they will be added.

Unlike other `nix flake` commands, `nix flake update` takes a list of names of inputs
to update as its positional arguments and operates on the flake in the current directory.
You can pass a different flake-url with `--flake` to override that default.

The related command [`nix flake lock`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-lock)
also creates lock files and adds missing inputs, but is safer as it
will never update inputs already in the lock file.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#options)

* [`--flake`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-flake) *flake-url*

  The flake to operate on. Default is the current directory.

## [Common evaluation options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#common-evaluation-options)

* [`--arg`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-arg) *name* *expr*

  Pass the value *expr* as the argument *name* to Nix functions.
* [`--arg-from-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-arg-from-file) *name* *path*

  Pass the contents of file *path* as the argument *name* to Nix functions.
* [`--arg-from-stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-arg-from-stdin) *name*

  Pass the contents of stdin as the argument *name* to Nix functions.
* [`--argstr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-argstr) *name* *string*

  Pass the string *string* as the argument *name* to Nix functions.
* [`--debugger`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-debugger)

  Start an interactive environment if evaluation fails.
* [`--eval-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-eval-store) *store-url*

  The [URL of the Nix store](https://nix.dev/manual/nix/2.32/store/types/#store-url-format)
  to use for evaluation, i.e. to store derivations (`.drv` files) and inputs referenced by them.
* [`--impure`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-impure)

  Allow access to mutable paths and repositories.
* [`--include`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-include) / `-I` *path*

  Add *path* to search path entries used to resolve [lookup paths](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path)

  This option may be given multiple times.

  Paths added through `-I` take precedence over the [`nix-path` configuration setting](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-nix-path) and the [`NIX_PATH` environment variable](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_PATH).
* [`--override-flake`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-override-flake) *original-ref* *resolved-ref*

  Override the flake registries, redirecting *original-ref* to *resolved-ref*.

## [Common flake-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#common-flake-related-options)

* [`--commit-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-commit-lock-file)

  Commit changes to the flake's lock file.
* [`--inputs-from`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-inputs-from) *flake-url*

  Use the inputs of the specified flake as registry entries.
* [`--no-registries`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-no-registries)

  Don't allow lookups in the flake registries.

  > **DEPRECATED**
  >
  > Use [`--no-use-registries`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-registries) instead.
* [`--output-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-output-lock-file) *flake-lock-path*

  Write the given lock file instead of `flake.lock` within the top-level flake.
* [`--override-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-override-input) *input-path* *flake-url*

  Override a specific flake input (e.g. `dwarffs/nixpkgs`). This implies `--no-write-lock-file`.
* [`--recreate-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-recreate-lock-file)

  Recreate the flake's lock file from scratch.

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.
* [`--reference-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-reference-lock-file) *flake-lock-path*

  Read the given lock file instead of `flake.lock` within the top-level flake.
* [`--update-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-update-input) *input-path*

  Update a specific flake input (ignoring its previous entry in the lock file).

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--repair`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-repair)

  During evaluation, rewrite missing or corrupted files in the Nix store. During building, rebuild missing or corrupted store paths.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.