---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build
title: nix build - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix build - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#name)

`nix build` - build a derivation or fetch a store path

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#synopsis)

`nix build` [*option*...] *installables*...

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#examples)

* Build the default package from the flake in the current directory:

  ```
  # nix build
  ```
* Build and run GNU Hello from the `nixpkgs` flake:

  ```
  # nix build nixpkgs#hello
  # ./result/bin/hello
  Hello, world!
  ```
* Build GNU Hello and Cowsay, leaving two result symlinks:

  ```
  # nix build nixpkgs#hello nixpkgs#cowsay
  # ls -l result*
  lrwxrwxrwx 1 … result -> /nix/store/v5sv61sszx301i0x6xysaqzla09nksnd-hello-2.10
  lrwxrwxrwx 1 … result-1 -> /nix/store/rkfrm0z6x6jmi7d3gsmma4j53h15mg33-cowsay-3.03+dfsg2
  ```
* Build GNU Hello and print the resulting store path.

  ```
  # nix build nixpkgs#hello --print-out-paths
  /nix/store/v5sv61sszx301i0x6xysaqzla09nksnd-hello-2.10
  ```
* Build a specific output:

  ```
  # nix build nixpkgs#glibc.dev
  # ls -ld ./result-dev
  lrwxrwxrwx 1 … ./result-dev -> /nix/store/dkm3gwl0xrx0wrw6zi5x3px3lpgjhlw4-glibc-2.32-dev
  ```
* Build all outputs:

  ```
  # nix build "nixpkgs#openssl^*" --print-out-paths
  /nix/store/gvad6v0cmq1qccmc4wphsazqbj0xzjsl-openssl-3.0.13-bin
  /nix/store/a07jqdrc8afnk8r6f3lnhh4gvab7chk4-openssl-3.0.13-debug
  /nix/store/yg75achq89wgqn2fi3gglgsd77kjpi03-openssl-3.0.13-dev
  /nix/store/bvdcihi8c88fw31cg6gzzmpnwglpn1jv-openssl-3.0.13-doc
  /nix/store/gjqcvq47cmxazxga0cirspm3jywkmvfv-openssl-3.0.13-man
  /nix/store/7nmrrad8skxr47f9hfl3xc0pfqmwq51b-openssl-3.0.13
  ```
* Build attribute `build.x86_64-linux` from (non-flake) Nix expression
  `release.nix`:

  ```
  # nix build --file release.nix build.x86_64-linux
  ```
* Build a NixOS system configuration from a flake, and make a profile
  point to the result:

  ```
  # nix build --profile /nix/var/nix/profiles/system \
      ~/my-configurations#nixosConfigurations.machine.config.system.build.toplevel
  ```

  (This is essentially what `nixos-rebuild` does.)
* Build an expression specified on the command line:

  ```
  # nix build --impure --expr \
      'with import <nixpkgs> {};
       runCommand "foo" {
         buildInputs = [ hello ];
       }
       "hello > $out"'
  # cat ./result
  Hello, world!
  ```

  Note that `--impure` is needed because we're using `<nixpkgs>`,
  which relies on the `$NIX_PATH` environment variable.
* Fetch a store path from the configured substituters, if it doesn't
  already exist:

  ```
  # nix build /nix/store/rkfrm0z6x6jmi7d3gsmma4j53h15mg33-cowsay-3.03+dfsg2
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#description)

`nix build` builds the specified *installables*. [Installables](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) that
resolve to derivations are built (or substituted if possible). Store
path installables are substituted.

Unless `--no-link` is specified, after a successful build, it creates
symlinks to the store paths of the installables. These symlinks have
the prefix `./result` by default; this can be overridden using the
`--out-link` option. Each symlink has a suffix `-<N>-<outname>`, where
*N* is the index of the installable (with the left-most installable
having index 0), and *outname* is the symbolic derivation output name
(e.g. `bin`, `dev` or `lib`). `-<N>` is omitted if *N* = 0, and
`-<outname>` is omitted if *outname* = `out` (denoting the default
output).

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#options)

* [`--dry-run`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-dry-run)

  Show what this command would do without doing it.
* [`--json`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-json)

  Produce output in JSON format, suitable for consumption by another program.
* [`--no-link`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-no-link)

  Do not create symlinks to the build results.
* [`--no-pretty`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-no-pretty)

  Print compact JSON output on a single line, even when the output is a terminal.
  Some commands may print multiple JSON objects on separate lines.

  ```
                See `--pretty`.
  ```
* [`--out-link`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-out-link) / `-o` *path*

  Use *path* as prefix for the symlinks to the build results. It defaults to `result`.
* [`--pretty`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-pretty)

  Print multi-line, indented JSON output for readability.

  ```
                Default: indent if output is to a terminal.

                This option is only effective when `--json` is also specified.
  ```
* [`--print-out-paths`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-print-out-paths)

  Print the resulting output paths
* [`--profile`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-profile) *path*

  The profile to operate on.
* [`--rebuild`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-rebuild)

  Rebuild an already built package and compare the result to the existing store paths.
* [`--stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-stdin)

  Read installables from the standard input. No default installable applied.

## [Common evaluation options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#common-evaluation-options)

* [`--arg`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-arg) *name* *expr*

  Pass the value *expr* as the argument *name* to Nix functions.
* [`--arg-from-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-arg-from-file) *name* *path*

  Pass the contents of file *path* as the argument *name* to Nix functions.
* [`--arg-from-stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-arg-from-stdin) *name*

  Pass the contents of stdin as the argument *name* to Nix functions.
* [`--argstr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-argstr) *name* *string*

  Pass the string *string* as the argument *name* to Nix functions.
* [`--debugger`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-debugger)

  Start an interactive environment if evaluation fails.
* [`--eval-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-eval-store) *store-url*

  The [URL of the Nix store](https://nix.dev/manual/nix/2.32/store/types/#store-url-format)
  to use for evaluation, i.e. to store derivations (`.drv` files) and inputs referenced by them.
* [`--impure`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-impure)

  Allow access to mutable paths and repositories.
* [`--include`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-include) / `-I` *path*

  Add *path* to search path entries used to resolve [lookup paths](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path)

  This option may be given multiple times.

  Paths added through `-I` take precedence over the [`nix-path` configuration setting](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-nix-path) and the [`NIX_PATH` environment variable](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_PATH).
* [`--override-flake`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-override-flake) *original-ref* *resolved-ref*

  Override the flake registries, redirecting *original-ref* to *resolved-ref*.

## [Common flake-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#common-flake-related-options)

* [`--commit-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-commit-lock-file)

  Commit changes to the flake's lock file.
* [`--inputs-from`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-inputs-from) *flake-url*

  Use the inputs of the specified flake as registry entries.
* [`--no-registries`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-no-registries)

  Don't allow lookups in the flake registries.

  > **DEPRECATED**
  >
  > Use [`--no-use-registries`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-registries) instead.
* [`--no-update-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-no-update-lock-file)

  Do not allow any updates to the flake's lock file.
* [`--no-write-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-no-write-lock-file)

  Do not write the flake's newly generated lock file.
* [`--output-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-output-lock-file) *flake-lock-path*

  Write the given lock file instead of `flake.lock` within the top-level flake.
* [`--override-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-override-input) *input-path* *flake-url*

  Override a specific flake input (e.g. `dwarffs/nixpkgs`). This implies `--no-write-lock-file`.
* [`--recreate-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-recreate-lock-file)

  Recreate the flake's lock file from scratch.

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.
* [`--reference-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-reference-lock-file) *flake-lock-path*

  Read the given lock file instead of `flake.lock` within the top-level flake.
* [`--update-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-update-input) *input-path*

  Update a specific flake input (ignoring its previous entry in the lock file).

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--repair`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-repair)

  During evaluation, rewrite missing or corrupted files in the Nix store. During building, rebuild missing or corrupted store paths.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-version)

  Show version information.

## [Options that change the interpretation of](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#options-that-change-the-interpretation-of-installables) [installables](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables)

* [`--expr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-expr) *expr*

  Interpret [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression *expr*.
* [`--file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build#opt-file) / `-f` *file*

  Interpret [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression stored in *file*. If *file* is the character -, then a Nix expression is read from standard input. Implies `--impure`.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.