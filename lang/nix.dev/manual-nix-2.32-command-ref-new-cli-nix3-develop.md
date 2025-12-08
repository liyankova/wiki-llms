---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop
title: nix develop - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix develop - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#name)

`nix develop` - run a bash shell that provides the build environment of a derivation

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#synopsis)

`nix develop` [*option*...] *installable*

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#examples)

* Start a shell with the build environment of the default package of
  the flake in the current directory:

  ```
  # nix develop
  ```

  Typical commands to run inside this shell are:

  ```
  # configurePhase
  # buildPhase
  # installPhase
  ```

  Alternatively, you can run whatever build tools your project uses
  directly, e.g. for a typical Unix project:

  ```
  # ./configure --prefix=$out
  # make
  # make install
  ```
* Run a particular build phase directly:

  ```
  # nix develop --unpack
  # nix develop --configure
  # nix develop --build
  # nix develop --check
  # nix develop --install
  # nix develop --installcheck
  ```
* Start a shell with the build environment of GNU Hello:

  ```
  # nix develop nixpkgs#hello
  ```
* Record a build environment in a profile:

  ```
  # nix develop --profile /tmp/my-build-env nixpkgs#hello
  ```
* Use a build environment previously recorded in a profile:

  ```
  # nix develop /tmp/my-build-env
  ```
* Replace all occurrences of the store path corresponding to
  `glibc.dev` with a writable directory:

  ```
  # nix develop --redirect nixpkgs#glibc.dev ~/my-glibc/outputs/dev
  ```

  Note that this is useful if you're running a `nix develop` shell for
  `nixpkgs#glibc` in `~/my-glibc` and want to compile another package
  against it.
* Run a series of script commands:

  ```
  # nix develop --command bash -c "mkdir build && cmake .. && make"
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#description)

`nix develop` starts a `bash` shell that provides an interactive build
environment nearly identical to what Nix would use to build
[*installable*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables). Inside this shell, environment variables and shell
functions are set up so that you can interactively and incrementally
build your package.

Nix determines the build environment by building a modified version of
the derivation *installable* that just records the environment
initialised by `stdenv` and exits. This build environment can be
recorded into a profile using `--profile`.

The prompt used by the `bash` shell can be customised by setting the
`bash-prompt`, `bash-prompt-prefix`, and `bash-prompt-suffix` settings in
`nix.conf` or in the flake's `nixConfig` attribute.

# [Flake output attributes](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#flake-output-attributes)

If no flake output attribute is given, `nix develop` tries the following
flake output attributes:

* `devShells.<system>.default`
* `packages.<system>.default`

If a flake output *name* is given, `nix develop` tries the following flake
output attributes:

* `devShells.<system>.<name>`
* `packages.<system>.<name>`
* `legacyPackages.<system>.<name>`

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#options)

* [`--build`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-build)

  Run the `build` phase.
* [`--check`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-check)

  Run the `check` phase.
* [`--command`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-command) / `-c` *command* *args*

  Instead of starting an interactive shell, start the specified command and arguments.
* [`--configure`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-configure)

  Run the `configure` phase.
* [`--install`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-install)

  Run the `install` phase.
* [`--installcheck`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-installcheck)

  Run the `installcheck` phase.
* [`--phase`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-phase) *phase-name*

  The stdenv phase to run (e.g. `build` or `configure`).
* [`--profile`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-profile) *path*

  The profile to operate on.
* [`--redirect`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-redirect) *installable* *outputs-dir*

  Redirect a store path to a mutable location.
* [`--unpack`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-unpack)

  Run the `unpack` phase.

## [Common evaluation options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#common-evaluation-options)

* [`--arg`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-arg) *name* *expr*

  Pass the value *expr* as the argument *name* to Nix functions.
* [`--arg-from-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-arg-from-file) *name* *path*

  Pass the contents of file *path* as the argument *name* to Nix functions.
* [`--arg-from-stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-arg-from-stdin) *name*

  Pass the contents of stdin as the argument *name* to Nix functions.
* [`--argstr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-argstr) *name* *string*

  Pass the string *string* as the argument *name* to Nix functions.
* [`--debugger`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-debugger)

  Start an interactive environment if evaluation fails.
* [`--eval-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-eval-store) *store-url*

  The [URL of the Nix store](https://nix.dev/manual/nix/2.32/store/types/#store-url-format)
  to use for evaluation, i.e. to store derivations (`.drv` files) and inputs referenced by them.
* [`--impure`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-impure)

  Allow access to mutable paths and repositories.
* [`--include`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-include) / `-I` *path*

  Add *path* to search path entries used to resolve [lookup paths](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path)

  This option may be given multiple times.

  Paths added through `-I` take precedence over the [`nix-path` configuration setting](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-nix-path) and the [`NIX_PATH` environment variable](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_PATH).
* [`--override-flake`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-override-flake) *original-ref* *resolved-ref*

  Override the flake registries, redirecting *original-ref* to *resolved-ref*.

## [Common flake-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#common-flake-related-options)

* [`--commit-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-commit-lock-file)

  Commit changes to the flake's lock file.
* [`--inputs-from`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-inputs-from) *flake-url*

  Use the inputs of the specified flake as registry entries.
* [`--no-registries`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-no-registries)

  Don't allow lookups in the flake registries.

  > **DEPRECATED**
  >
  > Use [`--no-use-registries`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-registries) instead.
* [`--no-update-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-no-update-lock-file)

  Do not allow any updates to the flake's lock file.
* [`--no-write-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-no-write-lock-file)

  Do not write the flake's newly generated lock file.
* [`--output-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-output-lock-file) *flake-lock-path*

  Write the given lock file instead of `flake.lock` within the top-level flake.
* [`--override-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-override-input) *input-path* *flake-url*

  Override a specific flake input (e.g. `dwarffs/nixpkgs`). This implies `--no-write-lock-file`.
* [`--recreate-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-recreate-lock-file)

  Recreate the flake's lock file from scratch.

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.
* [`--reference-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-reference-lock-file) *flake-lock-path*

  Read the given lock file instead of `flake.lock` within the top-level flake.
* [`--update-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-update-input) *input-path*

  Update a specific flake input (ignoring its previous entry in the lock file).

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--repair`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-repair)

  During evaluation, rewrite missing or corrupted files in the Nix store. During building, rebuild missing or corrupted store paths.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-version)

  Show version information.

## [Options that change environment variables](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#options-that-change-environment-variables)

* [`--ignore-env`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-ignore-env) / `-i`

  Clear the entire environment, except for those specified with `--keep-env-var`.
* [`--keep-env-var`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-keep-env-var) / `-k` *name*

  Keep the environment variable *name*, when using `--ignore-env`.
* [`--set-env-var`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-set-env-var) / `-s` *name* *value*

  Sets an environment variable *name* with *value*.
* [`--unset-env-var`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-unset-env-var) / `-u` *name*

  Unset the environment variable *name*.

## [Options that change the interpretation of](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#options-that-change-the-interpretation-of-installables) [installables](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables)

* [`--expr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-expr) *expr*

  Interpret [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression *expr*.
* [`--file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-develop#opt-file) / `-f` *file*

  Interpret [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression stored in *file*. If *file* is the character -, then a Nix expression is read from standard input. Implies `--impure`.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.