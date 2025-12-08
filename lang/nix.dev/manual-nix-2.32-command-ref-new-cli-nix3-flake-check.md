---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check
title: nix flake check - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix flake check - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#name)

`nix flake check` - check whether the flake evaluates and run its tests

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#synopsis)

`nix flake check` [*option*...] *flake-url*

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#examples)

* Evaluate the flake in the current directory, and build its checks:

  ```
  # nix flake check
  ```
* Verify that the `patchelf` flake evaluates, but don't build its
  checks:

  ```
  # nix flake check --no-build github:NixOS/patchelf
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#description)

This command verifies that the flake specified by flake reference
*flake-url* can be evaluated successfully (as detailed below), and
that the derivations specified by the flake's `checks` output can be
built successfully.

If the `keep-going` option is set to `true`, Nix will keep evaluating as much
as it can and report the errors as it encounters them. Otherwise it will stop
at the first error.

# [Evaluation checks](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#evaluation-checks)

The following flake output attributes must be derivations:

* `checks.`*system*`.`*name*
* `devShells.`*system*`.default`
* `devShells.`*system*`.`*name*
* `nixosConfigurations.`*name*`.config.system.build.toplevel`
* `packages.`*system*`.default`
* `packages.`*system*`.`*name*

The following flake output attributes must be [app
definitions](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-run):

* `apps.`*system*`.default`
* `apps.`*system*`.`*name*

The following flake output attributes must be [template
definitions](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-init):

* `templates.default`
* `templates.`*name*

The following flake output attributes must be *Nixpkgs overlays*:

* `overlays.default`
* `overlays.`*name*

The following flake output attributes must be *NixOS modules*:

* `nixosModules.default`
* `nixosModules.`*name*

The following flake output attributes must be
[bundlers](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-bundle):

* `bundlers.default`
* `bundlers.`*name*

Old default attributes are renamed, they will work but will emit a warning:

* `defaultPackage.<system>` → `packages.`*system*`.default`
* `defaultApps.<system>` → `apps.`*system*`.default`
* `defaultTemplate` → `templates.default`
* `defaultBundler.<system>` → `bundlers.`*system*`.default`
* `overlay` → `overlays.default`
* `devShell.<system>` → `devShells.`*system*`.default`
* `nixosModule` → `nixosModules.default`

In addition, the `hydraJobs` output is evaluated in the same way as
Hydra's `hydra-eval-jobs` (i.e. as a arbitrarily deeply nested
attribute set of derivations). Similarly, the
`legacyPackages`.*system* output is evaluated like `nix-env --query --available` .

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#options)

* [`--all-systems`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-all-systems)

  Check the outputs for all systems.
* [`--no-build`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-no-build)

  Do not build checks.

## [Common evaluation options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#common-evaluation-options)

* [`--arg`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-arg) *name* *expr*

  Pass the value *expr* as the argument *name* to Nix functions.
* [`--arg-from-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-arg-from-file) *name* *path*

  Pass the contents of file *path* as the argument *name* to Nix functions.
* [`--arg-from-stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-arg-from-stdin) *name*

  Pass the contents of stdin as the argument *name* to Nix functions.
* [`--argstr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-argstr) *name* *string*

  Pass the string *string* as the argument *name* to Nix functions.
* [`--debugger`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-debugger)

  Start an interactive environment if evaluation fails.
* [`--eval-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-eval-store) *store-url*

  The [URL of the Nix store](https://nix.dev/manual/nix/2.32/store/types/#store-url-format)
  to use for evaluation, i.e. to store derivations (`.drv` files) and inputs referenced by them.
* [`--impure`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-impure)

  Allow access to mutable paths and repositories.
* [`--include`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-include) / `-I` *path*

  Add *path* to search path entries used to resolve [lookup paths](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path)

  This option may be given multiple times.

  Paths added through `-I` take precedence over the [`nix-path` configuration setting](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-nix-path) and the [`NIX_PATH` environment variable](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_PATH).
* [`--override-flake`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-override-flake) *original-ref* *resolved-ref*

  Override the flake registries, redirecting *original-ref* to *resolved-ref*.

## [Common flake-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#common-flake-related-options)

* [`--commit-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-commit-lock-file)

  Commit changes to the flake's lock file.
* [`--inputs-from`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-inputs-from) *flake-url*

  Use the inputs of the specified flake as registry entries.
* [`--no-registries`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-no-registries)

  Don't allow lookups in the flake registries.

  > **DEPRECATED**
  >
  > Use [`--no-use-registries`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-registries) instead.
* [`--no-update-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-no-update-lock-file)

  Do not allow any updates to the flake's lock file.
* [`--no-write-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-no-write-lock-file)

  Do not write the flake's newly generated lock file.
* [`--output-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-output-lock-file) *flake-lock-path*

  Write the given lock file instead of `flake.lock` within the top-level flake.
* [`--override-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-override-input) *input-path* *flake-url*

  Override a specific flake input (e.g. `dwarffs/nixpkgs`). This implies `--no-write-lock-file`.
* [`--recreate-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-recreate-lock-file)

  Recreate the flake's lock file from scratch.

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.
* [`--reference-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-reference-lock-file) *flake-lock-path*

  Read the given lock file instead of `flake.lock` within the top-level flake.
* [`--update-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-update-input) *input-path*

  Update a specific flake input (ignoring its previous entry in the lock file).

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--repair`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-repair)

  During evaluation, rewrite missing or corrupted files in the Nix store. During building, rebuild missing or corrupted store paths.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-check#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.