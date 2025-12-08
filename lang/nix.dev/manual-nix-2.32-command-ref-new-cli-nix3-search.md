---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search
title: nix search - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix search - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#name)

`nix search` - search for packages

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#synopsis)

`nix search` [*option*...] *installable* *regex*...

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#examples)

* Show all packages in the `nixpkgs` flake:

  ```
  # nix search nixpkgs ^
  * legacyPackages.x86_64-linux.AMB-plugins (0.8.1)
    A set of ambisonics ladspa plugins

  * legacyPackages.x86_64-linux.ArchiSteamFarm (4.3.1.0)
    Application with primary purpose of idling Steam cards from multiple accounts simultaneously
  …
  ```
* Show packages in the `nixpkgs` flake containing `blender` in its
  name or description:

  ```
  # nix search nixpkgs blender
  * legacyPackages.x86_64-linux.blender (2.91.0)
    3D Creation/Animation/Publishing System
  ```
* Search for packages underneath the attribute `gnome3` in Nixpkgs:

  ```
  # nix search nixpkgs#gnome3 vala
  * legacyPackages.x86_64-linux.gnome3.vala (0.48.9)
    Compiler for GObject type system
  ```
* Show all packages in the flake in the current directory:

  ```
  # nix search . ^
  ```
* Search for Firefox or Chromium:

  ```
  # nix search nixpkgs 'firefox|chromium'
  ```
* Search for packages containing `git` and either `frontend` or `gui`:

  ```
  # nix search nixpkgs git 'frontend|gui'
  ```
* Search for packages containing `neovim` but hide ones containing either `gui` or `python`:

  ```
  # nix search nixpkgs neovim --exclude 'python|gui'
  ```

  or

  ```
  # nix search nixpkgs neovim --exclude 'python' --exclude 'gui'
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#description)

`nix search` searches [*installable*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) that can be evaluated, that is, a
flake or Nix expression, but not a [store path](https://nix.dev/manual/nix/2.32/glossary#gloss-store-path) or [deriving path](https://nix.dev/manual/nix/2.32/glossary#gloss-deriving-path)) for packages whose name or description matches all of the
regular expressions *regex*. For each matching package, It prints the
full attribute name (from the root of the [installable](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables)), the version
and the `meta.description` field, highlighting the substrings that
were matched by the regular expressions.

To show all packages, use the regular expression `^`. In contrast to `.*`,
it avoids highlighting the entire name and description of every package.

> Note that in this context, `^` is the regex character to match the beginning of a string, *not* the delimiter for
> [selecting a derivation output](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#derivation-output-selection).

# [Flake output attributes](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#flake-output-attributes)

If no flake output attribute is given, `nix search` searches for
packages:

* Directly underneath `packages.<system>`.
* Underneath `legacyPackages.<system>`, recursing into attribute sets
  that contain an attribute `recurseForDerivations = true`.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#options)

* [`--exclude`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-exclude) / `-e` *regex*

  Hide packages whose attribute path, name or description contain *regex*.
* [`--json`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-json)

  Produce output in JSON format, suitable for consumption by another program.
* [`--no-pretty`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-no-pretty)

  Print compact JSON output on a single line, even when the output is a terminal.
  Some commands may print multiple JSON objects on separate lines.

  ```
                See `--pretty`.
  ```
* [`--pretty`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-pretty)

  Print multi-line, indented JSON output for readability.

  ```
                Default: indent if output is to a terminal.

                This option is only effective when `--json` is also specified.
  ```

## [Common evaluation options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#common-evaluation-options)

* [`--arg`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-arg) *name* *expr*

  Pass the value *expr* as the argument *name* to Nix functions.
* [`--arg-from-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-arg-from-file) *name* *path*

  Pass the contents of file *path* as the argument *name* to Nix functions.
* [`--arg-from-stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-arg-from-stdin) *name*

  Pass the contents of stdin as the argument *name* to Nix functions.
* [`--argstr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-argstr) *name* *string*

  Pass the string *string* as the argument *name* to Nix functions.
* [`--debugger`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-debugger)

  Start an interactive environment if evaluation fails.
* [`--eval-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-eval-store) *store-url*

  The [URL of the Nix store](https://nix.dev/manual/nix/2.32/store/types/#store-url-format)
  to use for evaluation, i.e. to store derivations (`.drv` files) and inputs referenced by them.
* [`--impure`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-impure)

  Allow access to mutable paths and repositories.
* [`--include`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-include) / `-I` *path*

  Add *path* to search path entries used to resolve [lookup paths](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path)

  This option may be given multiple times.

  Paths added through `-I` take precedence over the [`nix-path` configuration setting](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-nix-path) and the [`NIX_PATH` environment variable](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_PATH).
* [`--override-flake`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-override-flake) *original-ref* *resolved-ref*

  Override the flake registries, redirecting *original-ref* to *resolved-ref*.

## [Common flake-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#common-flake-related-options)

* [`--commit-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-commit-lock-file)

  Commit changes to the flake's lock file.
* [`--inputs-from`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-inputs-from) *flake-url*

  Use the inputs of the specified flake as registry entries.
* [`--no-registries`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-no-registries)

  Don't allow lookups in the flake registries.

  > **DEPRECATED**
  >
  > Use [`--no-use-registries`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-registries) instead.
* [`--no-update-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-no-update-lock-file)

  Do not allow any updates to the flake's lock file.
* [`--no-write-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-no-write-lock-file)

  Do not write the flake's newly generated lock file.
* [`--output-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-output-lock-file) *flake-lock-path*

  Write the given lock file instead of `flake.lock` within the top-level flake.
* [`--override-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-override-input) *input-path* *flake-url*

  Override a specific flake input (e.g. `dwarffs/nixpkgs`). This implies `--no-write-lock-file`.
* [`--recreate-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-recreate-lock-file)

  Recreate the flake's lock file from scratch.

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.
* [`--reference-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-reference-lock-file) *flake-lock-path*

  Read the given lock file instead of `flake.lock` within the top-level flake.
* [`--update-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-update-input) *input-path*

  Update a specific flake input (ignoring its previous entry in the lock file).

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--repair`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-repair)

  During evaluation, rewrite missing or corrupted files in the Nix store. During building, rebuild missing or corrupted store paths.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-version)

  Show version information.

## [Options that change the interpretation of](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#options-that-change-the-interpretation-of-installables) [installables](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables)

* [`--expr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-expr) *expr*

  Interpret [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression *expr*.
* [`--file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-search#opt-file) / `-f` *file*

  Interpret [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression stored in *file*. If *file* is the character -, then a Nix expression is read from standard input. Implies `--impure`.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.