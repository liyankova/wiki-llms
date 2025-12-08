---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show
title: nix derivation show - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix derivation show - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#name)

`nix derivation show` - show the contents of a store derivation

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#synopsis)

`nix derivation show` [*option*...] *installables*...

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#examples)

* Show the [store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation) that results from evaluating the Hello
  package:

  ```
  # nix derivation show nixpkgs#hello
  {
    "/nix/store/s6rn4jz1sin56rf4qj5b5v8jxjm32hlk-hello-2.10.drv": {
      …
    }
  }
  ```
* Show the full derivation graph (if available) that produced your
  NixOS system:

  ```
  # nix derivation show -r /run/current-system
  ```
* Print all files fetched using `fetchurl` by Firefox's dependency
  graph:

  ```
  # nix derivation show -r nixpkgs#firefox \
    | jq -r '.[] | select(.outputs.out.hash and .env.urls) | .env.urls' \
    | uniq | sort
  ```

  Note that `.outputs.out.hash` selects *fixed-output derivations*
  (derivations that produce output with a specified content hash),
  while `.env.urls` selects derivations with a `urls` attribute.

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#description)

This command prints on standard output a JSON representation of the
[store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation)s to which [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) evaluate.

Store derivations are used internally by Nix. They are store paths with
extension `.drv` that represent the build-time dependency graph to which
a Nix expression evaluates.

By default, this command only shows top-level derivations, but with
`--recursive`, it also shows their dependencies.

`nix derivation show` outputs a JSON map of [store path](https://nix.dev/manual/nix/2.32/store/store-path)s to derivations in the following format:

# [Derivation JSON Format](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#derivation-json-format)

> **Warning**
>
> This JSON format is currently
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and subject to change.

The JSON serialization of a
[derivations](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation)
is a JSON object with the following fields:

* `name`:
  The name of the derivation.
  This is used when calculating the store paths of the derivation's outputs.
* `version`:
  Must be `3`.
  This is a guard that allows us to continue evolving this format.
  The choice of `3` is fairly arbitrary, but corresponds to this informal version:

  + Version 0: A-Term format
  + Version 1: Original JSON format, with ugly `"r:sha256"` inherited from A-Term format.
  + Version 2: Separate `method` and `hashAlgo` fields in output specs
  + Verison 3: Drop store dir from store paths, just include base name.

  Note that while this format is experimental, the maintenance of versions is best-effort, and not promised to identify every change.
* `outputs`:
  Information about the output paths of the derivation.
  This is a JSON object with one member per output, where the key is the output name and the value is a JSON object with these fields:

  + `path`:
    The output path, if it is known in advanced.
    Otherwise, `null`.
  + `method`:
    For an output which will be [content addressed], a string representing the [method](https://nix.dev/manual/nix/2.32/store/store-object/content-address) of content addressing that is chosen.
    Valid method strings are:

    - [`flat`](https://nix.dev/manual/nix/2.32/store/store-object/content-address#method-flat)
    - [`nar`](https://nix.dev/manual/nix/2.32/store/store-object/content-address#method-nix-archive)
    - [`text`](https://nix.dev/manual/nix/2.32/store/store-object/content-address#method-text)
    - [`git`](https://nix.dev/manual/nix/2.32/store/store-object/content-address#method-git)

    Otherwise, `null`.
  + `hashAlgo`:
    For an output which will be [content addressed], the name of the hash algorithm used.
    Valid algorithm strings are:

    - `blake3`
    - `md5`
    - `sha1`
    - `sha256`
    - `sha512`
  + `hash`:
    For fixed-output derivations, the expected content hash in base-16.
  > **Example**
  >
  > ```
  > "outputs": {
  >   "out": {
  >     "method": "nar",
  >     "hashAlgo": "sha256",
  >     "hash": "6fc80dcc62179dbc12fc0b5881275898f93444833d21b89dfe5f7fbcbb1d0d62"
  >   }
  > }
  > ```
* `inputSrcs`:
  A list of store paths on which this derivation depends.

  > **Example**
  >
  > ```
  > "inputSrcs": [
  >   "47y241wqdhac3jm5l7nv0x4975mb1975-separate-debug-info.sh",
  >   "56d0w71pjj9bdr363ym3wj1zkwyqq97j-fix-pop-var-context-error.patch"
  > ]
  > ```
* `inputDrvs`:
  A JSON object specifying the derivations on which this derivation depends, and what outputs of those derivations.

  > **Example**
  >
  > ```
  > "inputDrvs": {
  >   "6lkh5yi7nlb7l6dr8fljlli5zfd9hq58-curl-7.73.0.drv": ["dev"],
  >   "fn3kgnfzl5dzym26j8g907gq3kbm8bfh-unzip-6.0.drv": ["out"]
  > }
  > ```

  specifies that this derivation depends on the `dev` output of `curl`, and the `out` output of `unzip`.
* `system`:
  The system type on which this derivation is to be built
  (e.g. `x86_64-linux`).
* `builder`:
  The absolute path of the program to be executed to run the build.
  Typically this is the `bash` shell
  (e.g. `/nix/store/r3j288vpmczbl500w6zz89gyfa4nr0b1-bash-4.4-p23/bin/bash`).
* `args`:
  The command-line arguments passed to the `builder`.
* `env`:
  The environment passed to the `builder`.
* `structuredAttrs`:
  [Strucutured Attributes](https://nix.dev/manual/nix/2.32/store/derivation/#structured-attrs), only defined if the derivation contains them.
  Structured attributes are JSON, and thus embedded as-is.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#options)

* [`--no-pretty`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-no-pretty)

  Print compact JSON output on a single line, even when the output is a terminal.
  Some commands may print multiple JSON objects on separate lines.

  ```
                See `--pretty`.
  ```
* [`--pretty`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-pretty)

  Print multi-line, indented JSON output for readability.

  ```
                Default: indent if output is to a terminal.

                This option is only effective when `--json` is also specified.
  ```
* [`--recursive`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-recursive) / `-r`

  Include the dependencies of the specified derivations.
* [`--stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-stdin)

  Read installables from the standard input. No default installable applied.

## [Common evaluation options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#common-evaluation-options)

* [`--arg`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-arg) *name* *expr*

  Pass the value *expr* as the argument *name* to Nix functions.
* [`--arg-from-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-arg-from-file) *name* *path*

  Pass the contents of file *path* as the argument *name* to Nix functions.
* [`--arg-from-stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-arg-from-stdin) *name*

  Pass the contents of stdin as the argument *name* to Nix functions.
* [`--argstr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-argstr) *name* *string*

  Pass the string *string* as the argument *name* to Nix functions.
* [`--debugger`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-debugger)

  Start an interactive environment if evaluation fails.
* [`--eval-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-eval-store) *store-url*

  The [URL of the Nix store](https://nix.dev/manual/nix/2.32/store/types/#store-url-format)
  to use for evaluation, i.e. to store derivations (`.drv` files) and inputs referenced by them.
* [`--impure`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-impure)

  Allow access to mutable paths and repositories.
* [`--include`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-include) / `-I` *path*

  Add *path* to search path entries used to resolve [lookup paths](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path)

  This option may be given multiple times.

  Paths added through `-I` take precedence over the [`nix-path` configuration setting](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-nix-path) and the [`NIX_PATH` environment variable](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_PATH).
* [`--override-flake`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-override-flake) *original-ref* *resolved-ref*

  Override the flake registries, redirecting *original-ref* to *resolved-ref*.

## [Common flake-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#common-flake-related-options)

* [`--commit-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-commit-lock-file)

  Commit changes to the flake's lock file.
* [`--inputs-from`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-inputs-from) *flake-url*

  Use the inputs of the specified flake as registry entries.
* [`--no-registries`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-no-registries)

  Don't allow lookups in the flake registries.

  > **DEPRECATED**
  >
  > Use [`--no-use-registries`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-registries) instead.
* [`--no-update-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-no-update-lock-file)

  Do not allow any updates to the flake's lock file.
* [`--no-write-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-no-write-lock-file)

  Do not write the flake's newly generated lock file.
* [`--output-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-output-lock-file) *flake-lock-path*

  Write the given lock file instead of `flake.lock` within the top-level flake.
* [`--override-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-override-input) *input-path* *flake-url*

  Override a specific flake input (e.g. `dwarffs/nixpkgs`). This implies `--no-write-lock-file`.
* [`--recreate-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-recreate-lock-file)

  Recreate the flake's lock file from scratch.

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.
* [`--reference-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-reference-lock-file) *flake-lock-path*

  Read the given lock file instead of `flake.lock` within the top-level flake.
* [`--update-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-update-input) *input-path*

  Update a specific flake input (ignoring its previous entry in the lock file).

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--repair`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-repair)

  During evaluation, rewrite missing or corrupted files in the Nix store. During building, rebuild missing or corrupted store paths.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-version)

  Show version information.

## [Options that change the interpretation of](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#options-that-change-the-interpretation-of-installables) [installables](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables)

* [`--expr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-expr) *expr*

  Interpret [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression *expr*.
* [`--file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-show#opt-file) / `-f` *file*

  Interpret [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression stored in *file*. If *file* is the character -, then a Nix expression is read from standard input. Implies `--impure`.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.