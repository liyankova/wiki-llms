---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures
title: nix store diff-closures - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix store diff-closures - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#name)

`nix store diff-closures` - show what packages and versions were added and removed between two closures

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#synopsis)

`nix store diff-closures` [*option*...] *before* *after*

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#examples)

* Show what got added and removed between two versions of the NixOS
  system profile:

  ```
  # nix store diff-closures /nix/var/nix/profiles/system-655-link /nix/var/nix/profiles/system-658-link
  acpi-call: 2020-04-07-5.8.16 → 2020-04-07-5.8.18
  baloo-widgets: 20.08.1 → 20.08.2
  bluez-qt: +12.6 KiB
  dolphin: 20.08.1 → 20.08.2, +13.9 KiB
  kdeconnect: 20.08.2 → ∅, -6597.8 KiB
  kdeconnect-kde: ∅ → 20.08.2, +6599.7 KiB
  …
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#description)

This command shows the differences between the two closures *before*
and *after* with respect to the addition, removal, or version change
of packages, as well as changes in store path sizes.

For each package name in the two closures (where a package name is
defined as the name component of a store path excluding the version),
if there is a change in the set of versions of the package, or a
change in the size of the store paths of more than 8 KiB, it prints a
line like this:

```
dolphin: 20.08.1 → 20.08.2, +13.9 KiB
```

No size change is shown if it's below the threshold. If the package
does not exist in either the *before* or *after* closures, it is
represented using `∅` (empty set) on the appropriate side of the
arrow. If a package has an empty version string, the version is
rendered as `ε` (epsilon).

There may be multiple versions of a package in each closure. In that
case, only the changed versions are shown. Thus,

```
libfoo: 1.2, 1.3 → 1.4
```

leaves open the possibility that there are other versions (e.g. `1.1`)
that exist in both closures.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#options)

## [Common evaluation options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#common-evaluation-options)

* [`--arg`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-arg) *name* *expr*

  Pass the value *expr* as the argument *name* to Nix functions.
* [`--arg-from-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-arg-from-file) *name* *path*

  Pass the contents of file *path* as the argument *name* to Nix functions.
* [`--arg-from-stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-arg-from-stdin) *name*

  Pass the contents of stdin as the argument *name* to Nix functions.
* [`--argstr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-argstr) *name* *string*

  Pass the string *string* as the argument *name* to Nix functions.
* [`--debugger`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-debugger)

  Start an interactive environment if evaluation fails.
* [`--eval-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-eval-store) *store-url*

  The [URL of the Nix store](https://nix.dev/manual/nix/2.32/store/types/#store-url-format)
  to use for evaluation, i.e. to store derivations (`.drv` files) and inputs referenced by them.
* [`--impure`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-impure)

  Allow access to mutable paths and repositories.
* [`--include`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-include) / `-I` *path*

  Add *path* to search path entries used to resolve [lookup paths](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path)

  This option may be given multiple times.

  Paths added through `-I` take precedence over the [`nix-path` configuration setting](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-nix-path) and the [`NIX_PATH` environment variable](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_PATH).
* [`--override-flake`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-override-flake) *original-ref* *resolved-ref*

  Override the flake registries, redirecting *original-ref* to *resolved-ref*.

## [Common flake-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#common-flake-related-options)

* [`--commit-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-commit-lock-file)

  Commit changes to the flake's lock file.
* [`--inputs-from`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-inputs-from) *flake-url*

  Use the inputs of the specified flake as registry entries.
* [`--no-registries`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-no-registries)

  Don't allow lookups in the flake registries.

  > **DEPRECATED**
  >
  > Use [`--no-use-registries`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-registries) instead.
* [`--no-update-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-no-update-lock-file)

  Do not allow any updates to the flake's lock file.
* [`--no-write-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-no-write-lock-file)

  Do not write the flake's newly generated lock file.
* [`--output-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-output-lock-file) *flake-lock-path*

  Write the given lock file instead of `flake.lock` within the top-level flake.
* [`--override-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-override-input) *input-path* *flake-url*

  Override a specific flake input (e.g. `dwarffs/nixpkgs`). This implies `--no-write-lock-file`.
* [`--recreate-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-recreate-lock-file)

  Recreate the flake's lock file from scratch.

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.
* [`--reference-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-reference-lock-file) *flake-lock-path*

  Read the given lock file instead of `flake.lock` within the top-level flake.
* [`--update-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-update-input) *input-path*

  Update a specific flake input (ignoring its previous entry in the lock file).

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--repair`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-repair)

  During evaluation, rewrite missing or corrupted files in the Nix store. During building, rebuild missing or corrupted store paths.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-version)

  Show version information.

## [Options that change the interpretation of](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#options-that-change-the-interpretation-of-installables) [installables](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables)

* [`--derivation`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-derivation)

  Operate on the [store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation) rather than its outputs.
* [`--expr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-expr) *expr*

  Interpret [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression *expr*.
* [`--file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures#opt-file) / `-f` *file*

  Interpret [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression stored in *file*. If *file* is the character -, then a Nix expression is read from standard input. Implies `--impure`.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.