---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy
title: nix copy - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix copy - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#name)

`nix copy` - copy paths between Nix stores

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#synopsis)

`nix copy` [*option*...] *installables*...

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#examples)

* Copy Firefox from the local store to a binary cache in `/tmp/cache`:

  ```
  # nix copy --to file:///tmp/cache $(type -p firefox)
  ```

  Note the `file://` - without this, the destination is a chroot
  store, not a binary cache.
* Copy all store paths from a local binary cache in `/tmp/cache` to the local store:

  ```
  # nix copy --all --from file:///tmp/cache
  ```
* Copy the entire current NixOS system closure to another machine via
  SSH:

  ```
  # nix copy --substitute-on-destination --to ssh://server /run/current-system
  ```

  The `-s` flag causes the remote machine to try to substitute missing
  store paths, which may be faster if the link between the local and
  remote machines is slower than the link between the remote machine
  and its substituters (e.g. `https://cache.nixos.org`).
* Copy a closure from another machine via SSH:

  ```
  # nix copy --from ssh://server /nix/store/a6cnl93nk1wxnq84brbbwr6hxw9gp2w9-blender-2.79-rc2
  ```
* Copy Hello to a binary cache in an Amazon S3 bucket:

  ```
  # nix copy --to s3://my-bucket?region=eu-west-1 nixpkgs#hello
  ```

  or to an S3-compatible storage system:

  ```
  # nix copy --to s3://my-bucket?region=eu-west-1&endpoint=example.com nixpkgs#hello
  ```

  Note that this only works if Nix is built with AWS support.
* Copy a closure from `/nix/store` to the chroot store `/tmp/nix/nix/store`:

  ```
  # nix copy --to /tmp/nix nixpkgs#hello --no-check-sigs
  ```
* Update the NixOS system profile to point to a closure copied from a
  remote machine:

  ```
  # nix copy --from ssh://server \
      --profile /nix/var/nix/profiles/system \
      /nix/store/r14v3km89zm3prwsa521fab5kgzvfbw4-nixos-system-foobar-24.05.20240925.759537f
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#description)

`nix copy` copies store path closures between two Nix stores. The
source store is specified using `--from` and the destination using
`--to`. If one of these is omitted, it defaults to the local store.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#options)

* [`--from`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-from) *store-uri*

  URL of the source Nix store.
* [`--no-check-sigs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-no-check-sigs)

  Do not require that paths are signed by trusted keys.
* [`--out-link`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-out-link) / `-o` *path*

  Create symlinks prefixed with *path* to the top-level store paths fetched from the source store.
* [`--profile`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-profile) *path*

  The profile to operate on.
* [`--stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-stdin)

  Read installables from the standard input. No default installable applied.
* [`--substitute-on-destination`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-substitute-on-destination) / `-s`

  Whether to try substitutes on the destination store (only supported by SSH stores).
* [`--to`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-to) *store-uri*

  URL of the destination Nix store.

## [Common evaluation options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#common-evaluation-options)

* [`--arg`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-arg) *name* *expr*

  Pass the value *expr* as the argument *name* to Nix functions.
* [`--arg-from-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-arg-from-file) *name* *path*

  Pass the contents of file *path* as the argument *name* to Nix functions.
* [`--arg-from-stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-arg-from-stdin) *name*

  Pass the contents of stdin as the argument *name* to Nix functions.
* [`--argstr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-argstr) *name* *string*

  Pass the string *string* as the argument *name* to Nix functions.
* [`--debugger`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-debugger)

  Start an interactive environment if evaluation fails.
* [`--eval-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-eval-store) *store-url*

  The [URL of the Nix store](https://nix.dev/manual/nix/2.32/store/types/#store-url-format)
  to use for evaluation, i.e. to store derivations (`.drv` files) and inputs referenced by them.
* [`--impure`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-impure)

  Allow access to mutable paths and repositories.
* [`--include`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-include) / `-I` *path*

  Add *path* to search path entries used to resolve [lookup paths](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path)

  This option may be given multiple times.

  Paths added through `-I` take precedence over the [`nix-path` configuration setting](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-nix-path) and the [`NIX_PATH` environment variable](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_PATH).
* [`--override-flake`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-override-flake) *original-ref* *resolved-ref*

  Override the flake registries, redirecting *original-ref* to *resolved-ref*.

## [Common flake-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#common-flake-related-options)

* [`--commit-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-commit-lock-file)

  Commit changes to the flake's lock file.
* [`--inputs-from`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-inputs-from) *flake-url*

  Use the inputs of the specified flake as registry entries.
* [`--no-registries`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-no-registries)

  Don't allow lookups in the flake registries.

  > **DEPRECATED**
  >
  > Use [`--no-use-registries`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-registries) instead.
* [`--no-update-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-no-update-lock-file)

  Do not allow any updates to the flake's lock file.
* [`--no-write-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-no-write-lock-file)

  Do not write the flake's newly generated lock file.
* [`--output-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-output-lock-file) *flake-lock-path*

  Write the given lock file instead of `flake.lock` within the top-level flake.
* [`--override-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-override-input) *input-path* *flake-url*

  Override a specific flake input (e.g. `dwarffs/nixpkgs`). This implies `--no-write-lock-file`.
* [`--recreate-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-recreate-lock-file)

  Recreate the flake's lock file from scratch.

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.
* [`--reference-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-reference-lock-file) *flake-lock-path*

  Read the given lock file instead of `flake.lock` within the top-level flake.
* [`--update-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-update-input) *input-path*

  Update a specific flake input (ignoring its previous entry in the lock file).

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--repair`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-repair)

  During evaluation, rewrite missing or corrupted files in the Nix store. During building, rebuild missing or corrupted store paths.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-version)

  Show version information.

## [Options that change the interpretation of](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#options-that-change-the-interpretation-of-installables) [installables](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables)

* [`--all`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-all)

  Apply the operation to every store path.
* [`--derivation`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-derivation)

  Operate on the [store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation) rather than its outputs.
* [`--expr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-expr) *expr*

  Interpret [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression *expr*.
* [`--file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-file) / `-f` *file*

  Interpret [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression stored in *file*. If *file* is the character -, then a Nix expression is read from standard input. Implies `--impure`.
* [`--no-recursive`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-copy#opt-no-recursive)

  Apply operation to specified paths only.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.