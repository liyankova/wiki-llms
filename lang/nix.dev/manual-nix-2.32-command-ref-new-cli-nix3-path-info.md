---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info
title: nix path-info - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix path-info - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#name)

`nix path-info` - query information about store paths

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#synopsis)

`nix path-info` [*option*...] *installables*...

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#examples)

* Print the store path produced by `nixpkgs#hello`:

  ```
  # nix path-info nixpkgs#hello
  /nix/store/v5sv61sszx301i0x6xysaqzla09nksnd-hello-2.10
  ```
* Show the closure sizes of every path in the current NixOS system
  closure, sorted by size:

  ```
  # nix path-info --recursive --closure-size /run/current-system | sort -nk2
  /nix/store/hl5xwp9kdrd1zkm0idm3kkby9q66z404-empty                                                96
  /nix/store/27324qvqhnxj3rncazmxc4mwy79kz8ha-nameservers                                         112
  …
  /nix/store/539jkw9a8dyry7clcv60gk6na816j7y8-etc                                          5783255504
  /nix/store/zqamz3cz4dbzfihki2mk7a63mbkxz9xq-nixos-system-machine-20.09.20201112.3090c65  5887562256
  ```
* Show a package's closure size and all its dependencies with human
  readable sizes:

  ```
  # nix path-info --recursive --size --closure-size --human-readable nixpkgs#rustc
  /nix/store/01rrgsg5zk3cds0xgdsq40zpk6g51dz9-ncurses-6.2-dev      386.7 KiB   69.1 MiB
  /nix/store/0q783wnvixpqz6dxjp16nw296avgczam-libpfm-4.11.0          5.9 MiB   37.4 MiB
  …
  ```
* Check the existence of a path in a binary cache:

  ```
  # nix path-info --recursive /nix/store/blzxgyvrk32ki6xga10phr4sby2xf25q-geeqie-1.5.1 --store https://cache.nixos.org/
  path '/nix/store/blzxgyvrk32ki6xga10phr4sby2xf25q-geeqie-1.5.1' is not valid
  ```
* Print the 10 most recently added paths (using --json and the jq(1)
  command):

  ```
  # nix path-info --json --all | jq -r 'to_entries | sort_by(.value.registrationTime) | .[-11:-1][] | .key'
  ```
* Show the size of the entire Nix store:

  ```
  # nix path-info --json --all | jq 'map(.narSize) | add'
  49812020936
  ```
* Show every path whose closure is bigger than 1 GB, sorted by closure
  size:

  ```
  # nix path-info --json --all --closure-size \
    | jq 'map_values(.closureSize | select(. < 1e9)) | to_entries | sort_by(.value)'
  [
    …,
    {
      .key = "/nix/store/zqamz3cz4dbzfihki2mk7a63mbkxz9xq-nixos-system-machine-20.09.20201112.3090c65",
      .value = 5887562256,
    }
  ]
  ```
* Print the path of the [store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation) produced by `nixpkgs#hello`:

  ```
  # nix path-info --derivation nixpkgs#hello
  /nix/store/s6rn4jz1sin56rf4qj5b5v8jxjm32hlk-hello-2.10.drv
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#description)

This command shows information about the store paths produced by
[*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables), or about all paths in the store if you pass `--all`.

By default, this command only prints the store paths. You can get
additional information by passing flags such as `--closure-size`,
`--size`, `--sigs` or `--json`.

> **Warning**
>
> Note that `nix path-info` does not build or substitute the
> *installables* you specify. Thus, if the corresponding store paths
> don't already exist, this command will fail. You can use `nix build`
> to ensure that they exist.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#options)

* [`--closure-size`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-closure-size) / `-S`

  Print the sum of the sizes of the NAR serialisations of the closure of each path.
* [`--human-readable`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-human-readable) / `-h`

  With `-s` and `-S`, print sizes in a human-friendly format such as `5.67G`.
* [`--json`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-json)

  Produce output in JSON format, suitable for consumption by another program.
* [`--no-pretty`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-no-pretty)

  Print compact JSON output on a single line, even when the output is a terminal.
  Some commands may print multiple JSON objects on separate lines.

  ```
                See `--pretty`.
  ```
* [`--pretty`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-pretty)

  Print multi-line, indented JSON output for readability.

  ```
                Default: indent if output is to a terminal.

                This option is only effective when `--json` is also specified.
  ```
* [`--sigs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-sigs)

  Show signatures.
* [`--size`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-size) / `-s`

  Print the size of the NAR serialisation of each path.
* [`--stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-stdin)

  Read installables from the standard input. No default installable applied.

## [Common evaluation options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#common-evaluation-options)

* [`--arg`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-arg) *name* *expr*

  Pass the value *expr* as the argument *name* to Nix functions.
* [`--arg-from-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-arg-from-file) *name* *path*

  Pass the contents of file *path* as the argument *name* to Nix functions.
* [`--arg-from-stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-arg-from-stdin) *name*

  Pass the contents of stdin as the argument *name* to Nix functions.
* [`--argstr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-argstr) *name* *string*

  Pass the string *string* as the argument *name* to Nix functions.
* [`--debugger`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-debugger)

  Start an interactive environment if evaluation fails.
* [`--eval-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-eval-store) *store-url*

  The [URL of the Nix store](https://nix.dev/manual/nix/2.32/store/types/#store-url-format)
  to use for evaluation, i.e. to store derivations (`.drv` files) and inputs referenced by them.
* [`--impure`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-impure)

  Allow access to mutable paths and repositories.
* [`--include`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-include) / `-I` *path*

  Add *path* to search path entries used to resolve [lookup paths](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path)

  This option may be given multiple times.

  Paths added through `-I` take precedence over the [`nix-path` configuration setting](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-nix-path) and the [`NIX_PATH` environment variable](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_PATH).
* [`--override-flake`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-override-flake) *original-ref* *resolved-ref*

  Override the flake registries, redirecting *original-ref* to *resolved-ref*.

## [Common flake-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#common-flake-related-options)

* [`--commit-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-commit-lock-file)

  Commit changes to the flake's lock file.
* [`--inputs-from`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-inputs-from) *flake-url*

  Use the inputs of the specified flake as registry entries.
* [`--no-registries`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-no-registries)

  Don't allow lookups in the flake registries.

  > **DEPRECATED**
  >
  > Use [`--no-use-registries`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-registries) instead.
* [`--no-update-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-no-update-lock-file)

  Do not allow any updates to the flake's lock file.
* [`--no-write-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-no-write-lock-file)

  Do not write the flake's newly generated lock file.
* [`--output-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-output-lock-file) *flake-lock-path*

  Write the given lock file instead of `flake.lock` within the top-level flake.
* [`--override-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-override-input) *input-path* *flake-url*

  Override a specific flake input (e.g. `dwarffs/nixpkgs`). This implies `--no-write-lock-file`.
* [`--recreate-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-recreate-lock-file)

  Recreate the flake's lock file from scratch.

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.
* [`--reference-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-reference-lock-file) *flake-lock-path*

  Read the given lock file instead of `flake.lock` within the top-level flake.
* [`--update-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-update-input) *input-path*

  Update a specific flake input (ignoring its previous entry in the lock file).

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--repair`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-repair)

  During evaluation, rewrite missing or corrupted files in the Nix store. During building, rebuild missing or corrupted store paths.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-version)

  Show version information.

## [Options that change the interpretation of](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#options-that-change-the-interpretation-of-installables) [installables](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables)

* [`--all`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-all)

  Apply the operation to every store path.
* [`--derivation`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-derivation)

  Operate on the [store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation) rather than its outputs.
* [`--expr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-expr) *expr*

  Interpret [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression *expr*.
* [`--file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-file) / `-f` *file*

  Interpret [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression stored in *file*. If *file* is the character -, then a Nix expression is read from standard input. Implies `--impure`.
* [`--recursive`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-path-info#opt-recursive) / `-r`

  Apply operation to closure of the specified paths.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.