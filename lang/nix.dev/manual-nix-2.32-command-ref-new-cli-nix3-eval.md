---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval
title: nix eval - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix eval - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#name)

`nix eval` - evaluate a Nix expression

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#synopsis)

`nix eval` [*option*...] *installable*

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#examples)

* Evaluate a Nix expression given on the command line:

  ```
  # nix eval --expr '1 + 2'
  ```
* Evaluate a Nix expression to JSON:

  ```
  # nix eval --json --expr '{ x = 1; }'
  {"x":1}
  ```
* Evaluate a Nix expression from a file:

  ```
  # nix eval --file ./my-nixpkgs hello.name
  ```
* Get the current version of the `nixpkgs` flake:

  ```
  # nix eval --raw nixpkgs#lib.version
  ```
* Print the store path of the Hello package:

  ```
  # nix eval --raw nixpkgs#hello
  ```
* Get a list of checks in the `nix` flake:

  ```
  # nix eval nix#checks.x86_64-linux --apply builtins.attrNames
  ```
* Generate a directory with the specified contents:

  ```
  # nix eval --write-to ./out --expr '{ foo = "bar"; subdir.bla = "123"; }'
  # cat ./out/foo
  bar
  # cat ./out/subdir/bla
  123
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#description)

This command evaluates the given Nix expression, and prints the result on standard output.

It also evaluates any nested attribute values and list items.

# [Output format](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#output-format)

`nix eval` can produce output in several formats:

* By default, the evaluation result is printed as a Nix expression.
* With `--json`, the evaluation result is printed in JSON format. Note
  that this fails if the result contains values that are not
  representable as JSON, such as functions.
* With `--raw`, the evaluation result must be a string, which is
  printed verbatim, without any quoting.
* With `--write-to` *path*, the evaluation result must be a string or
  a nested attribute set whose leaf values are strings. These strings
  are written to files named *path*/*attrpath*. *path* must not
  already exist.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#options)

* [`--apply`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-apply) *expr*

  Apply the function *expr* to each argument.
* [`--json`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-json)

  Produce output in JSON format, suitable for consumption by another program.
* [`--no-pretty`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-no-pretty)

  Print compact JSON output on a single line, even when the output is a terminal.
  Some commands may print multiple JSON objects on separate lines.

  ```
                See `--pretty`.
  ```
* [`--pretty`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-pretty)

  Print multi-line, indented JSON output for readability.

  ```
                Default: indent if output is to a terminal.

                This option is only effective when `--json` is also specified.
  ```
* [`--raw`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-raw)

  Print strings without quotes or escaping.
* [`--read-only`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-read-only)

  Do not instantiate each evaluated derivation. This improves performance, but can cause errors when accessing store paths of derivations during evaluation.
* [`--write-to`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-write-to) *path*

  Write a string or attrset of strings to *path*.

## [Common evaluation options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#common-evaluation-options)

* [`--arg`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-arg) *name* *expr*

  Pass the value *expr* as the argument *name* to Nix functions.
* [`--arg-from-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-arg-from-file) *name* *path*

  Pass the contents of file *path* as the argument *name* to Nix functions.
* [`--arg-from-stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-arg-from-stdin) *name*

  Pass the contents of stdin as the argument *name* to Nix functions.
* [`--argstr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-argstr) *name* *string*

  Pass the string *string* as the argument *name* to Nix functions.
* [`--debugger`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-debugger)

  Start an interactive environment if evaluation fails.
* [`--eval-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-eval-store) *store-url*

  The [URL of the Nix store](https://nix.dev/manual/nix/2.32/store/types/#store-url-format)
  to use for evaluation, i.e. to store derivations (`.drv` files) and inputs referenced by them.
* [`--impure`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-impure)

  Allow access to mutable paths and repositories.
* [`--include`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-include) / `-I` *path*

  Add *path* to search path entries used to resolve [lookup paths](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path)

  This option may be given multiple times.

  Paths added through `-I` take precedence over the [`nix-path` configuration setting](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-nix-path) and the [`NIX_PATH` environment variable](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_PATH).
* [`--override-flake`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-override-flake) *original-ref* *resolved-ref*

  Override the flake registries, redirecting *original-ref* to *resolved-ref*.

## [Common flake-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#common-flake-related-options)

* [`--commit-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-commit-lock-file)

  Commit changes to the flake's lock file.
* [`--inputs-from`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-inputs-from) *flake-url*

  Use the inputs of the specified flake as registry entries.
* [`--no-registries`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-no-registries)

  Don't allow lookups in the flake registries.

  > **DEPRECATED**
  >
  > Use [`--no-use-registries`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-registries) instead.
* [`--no-update-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-no-update-lock-file)

  Do not allow any updates to the flake's lock file.
* [`--no-write-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-no-write-lock-file)

  Do not write the flake's newly generated lock file.
* [`--output-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-output-lock-file) *flake-lock-path*

  Write the given lock file instead of `flake.lock` within the top-level flake.
* [`--override-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-override-input) *input-path* *flake-url*

  Override a specific flake input (e.g. `dwarffs/nixpkgs`). This implies `--no-write-lock-file`.
* [`--recreate-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-recreate-lock-file)

  Recreate the flake's lock file from scratch.

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.
* [`--reference-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-reference-lock-file) *flake-lock-path*

  Read the given lock file instead of `flake.lock` within the top-level flake.
* [`--update-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-update-input) *input-path*

  Update a specific flake input (ignoring its previous entry in the lock file).

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--repair`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-repair)

  During evaluation, rewrite missing or corrupted files in the Nix store. During building, rebuild missing or corrupted store paths.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-version)

  Show version information.

## [Options that change the interpretation of](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#options-that-change-the-interpretation-of-installables) [installables](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables)

* [`--expr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-expr) *expr*

  Interpret [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression *expr*.
* [`--file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-eval#opt-file) / `-f` *file*

  Interpret [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression stored in *file*. If *file* is the character -, then a Nix expression is read from standard input. Implies `--impure`.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.