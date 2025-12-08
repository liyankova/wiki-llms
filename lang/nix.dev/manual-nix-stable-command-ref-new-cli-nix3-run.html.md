---
url: https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html
title: nix run - Nix 2.28.6 Reference Manual
source_domain: nix.dev
---

# nix run - Nix 2.28.6 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.28/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#name)

`nix run` - run a Nix application

# [Synopsis](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#synopsis)

`nix run` [*option*...] *installable* *args*...

# [Examples](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#examples)

* Run the default app from the `blender-bin` flake:

  ```
  # nix run blender-bin
  ```
* Run a non-default app from the `blender-bin` flake:

  ```
  # nix run blender-bin#blender_2_83
  ```

  Tip: you can find apps provided by this flake by running `nix flake show blender-bin`.
* Run `vim` from the `nixpkgs` flake:

  ```
  # nix run nixpkgs#vim
  ```

  Note that `vim` (as of the time of writing of this page) is not an
  app but a package. Thus, Nix runs the eponymous file from the `vim`
  package.
* Run `vim` with arguments:

  ```
  # nix run nixpkgs#vim -- --help
  ```

# [Description](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#description)

`nix run` builds and runs [*installable*](https://nix.dev/manual/nix/2.28/command-ref/new-cli/nix#installables), which must evaluate to an
*app* or a regular Nix derivation.

If *installable* evaluates to an *app* (see below), it executes the
program specified by the app definition.

If *installable* evaluates to a derivation, it will try to execute the
program `<out>/bin/<name>`, where *out* is the primary output store
path of the derivation, and *name* is the first of the following that
exists:

* The `meta.mainProgram` attribute of the derivation.
* The `pname` attribute of the derivation.
* The name part of the value of the `name` attribute of the derivation.

For instance, if `name` is set to `hello-1.10`, `nix run` will run
`$out/bin/hello`.

# [Flake output attributes](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#flake-output-attributes)

If no flake output attribute is given, `nix run` tries the following
flake output attributes:

* `apps.<system>.default`
* `packages.<system>.default`

If an attribute *name* is given, `nix run` tries the following flake
output attributes:

* `apps.<system>.<name>`
* `packages.<system>.<name>`
* `legacyPackages.<system>.<name>`

# [Apps](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#apps)

An app is specified by a flake output attribute named
`apps.<system>.<name>`. It looks like this:

```
apps.x86_64-linux.blender_2_79 = {
  type = "app";
  program = "${self.packages.x86_64-linux.blender_2_79}/bin/blender";
  meta.description = "Run Blender, a free and open-source 3D creation suite.";
};
```

The only supported attributes are:

* `type` (required): Must be set to `app`.
* `program` (required): The full path of the executable to run. It
  must reside in the Nix store.
* `meta.description` (optional): A description of the app.

# [Options](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#options)

## [Common evaluation options](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#common-evaluation-options)

* [`--arg`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-arg) *name* *expr*

  Pass the value *expr* as the argument *name* to Nix functions.
* [`--arg-from-file`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-arg-from-file) *name* *path*

  Pass the contents of file *path* as the argument *name* to Nix functions.
* [`--arg-from-stdin`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-arg-from-stdin) *name*

  Pass the contents of stdin as the argument *name* to Nix functions.
* [`--argstr`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-argstr) *name* *string*

  Pass the string *string* as the argument *name* to Nix functions.
* [`--debugger`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-debugger)

  Start an interactive environment if evaluation fails.
* [`--eval-store`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-eval-store) *store-url*

  The [URL of the Nix store](https://nix.dev/manual/nix/2.28/store/types/#store-url-format)
  to use for evaluation, i.e. to store derivations (`.drv` files) and inputs referenced by them.
* [`--impure`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-impure)

  Allow access to mutable paths and repositories.
* [`--include`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-include) / `-I` *path*

  Add *path* to search path entries used to resolve [lookup paths](https://nix.dev/manual/nix/2.28/language/constructs/lookup-path)

  This option may be given multiple times.

  Paths added through `-I` take precedence over the [`nix-path` configuration setting](https://nix.dev/manual/nix/2.28/command-ref/conf-file#conf-nix-path) and the [`NIX_PATH` environment variable](https://nix.dev/manual/nix/2.28/command-ref/env-common#env-NIX_PATH).
* [`--override-flake`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-override-flake) *original-ref* *resolved-ref*

  Override the flake registries, redirecting *original-ref* to *resolved-ref*.

## [Common flake-related options](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#common-flake-related-options)

* [`--commit-lock-file`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-commit-lock-file)

  Commit changes to the flake's lock file.
* [`--inputs-from`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-inputs-from) *flake-url*

  Use the inputs of the specified flake as registry entries.
* [`--no-registries`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-no-registries)

  Don't allow lookups in the flake registries.

  > **DEPRECATED**
  >
  > Use [`--no-use-registries`](https://nix.dev/manual/nix/2.28/command-ref/conf-file#conf-use-registries) instead.
* [`--no-update-lock-file`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-no-update-lock-file)

  Do not allow any updates to the flake's lock file.
* [`--no-write-lock-file`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-no-write-lock-file)

  Do not write the flake's newly generated lock file.
* [`--output-lock-file`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-output-lock-file) *flake-lock-path*

  Write the given lock file instead of `flake.lock` within the top-level flake.
* [`--override-input`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-override-input) *input-path* *flake-url*

  Override a specific flake input (e.g. `dwarffs/nixpkgs`). This implies `--no-write-lock-file`.
* [`--recreate-lock-file`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-recreate-lock-file)

  Recreate the flake's lock file from scratch.

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.28/command-ref/new-cli/nix3-flake-update) instead.
* [`--reference-lock-file`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-reference-lock-file) *flake-lock-path*

  Read the given lock file instead of `flake.lock` within the top-level flake.
* [`--update-input`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-update-input) *input-path*

  Update a specific flake input (ignoring its previous entry in the lock file).

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.28/command-ref/new-cli/nix3-flake-update) instead.

## [Logging-related options](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--repair`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-repair)

  During evaluation, rewrite missing or corrupted files in the Nix store. During building, rebuild missing or corrupted store paths.
* [`--version`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-version)

  Show version information.

## [Options that change environment variables](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#options-that-change-environment-variables)

* [`--ignore-env`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-ignore-env) / `-i`

  Clear the entire environment, except for those specified with `--keep-env-var`.
* [`--keep-env-var`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-keep-env-var) / `-k` *name*

  Keep the environment variable *name*, when using `--ignore-env`.
* [`--set-env-var`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-set-env-var) / `-s` *name* *value*

  Sets an environment variable *name* with *value*.
* [`--unset-env-var`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-unset-env-var) / `-u` *name*

  Unset the environment variable *name*.

## [Options that change the interpretation of](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#options-that-change-the-interpretation-of-installables) [installables](https://nix.dev/manual/nix/2.28/command-ref/new-cli/nix#installables)

* [`--expr`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-expr) *expr*

  Interpret [*installables*](https://nix.dev/manual/nix/2.28/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression *expr*.
* [`--file`](https://nix.dev/manual/nix/stable/command-ref/new-cli/nix3-run.html#opt-file) / `-f` *file*

  Interpret [*installables*](https://nix.dev/manual/nix/2.28/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression stored in *file*. If *file* is the character -, then a Nix expression will be read from standard input. Implies `--impure`.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.28/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.