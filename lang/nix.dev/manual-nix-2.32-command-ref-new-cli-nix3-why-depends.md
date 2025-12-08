---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends
title: nix why-depends - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix why-depends - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#name)

`nix why-depends` - show why a package has another package in its closure

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#synopsis)

`nix why-depends` [*option*...] *package* *dependency*

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#examples)

* Show one path through the dependency graph leading from Hello to
  Glibc:

  ```
  # nix why-depends nixpkgs#hello nixpkgs#glibc
  /nix/store/v5sv61sszx301i0x6xysaqzla09nksnd-hello-2.10
  └───bin/hello: …...................../nix/store/9l06v7fc38c1x3r2iydl15ksgz0ysb82-glibc-2.32/lib/ld-linux-x86-64.…
      → /nix/store/9l06v7fc38c1x3r2iydl15ksgz0ysb82-glibc-2.32
  ```
* Show all files and paths in the dependency graph leading from
  Thunderbird to libX11:

  ```
  # nix why-depends --all nixpkgs#thunderbird nixpkgs#xorg.libX11
  /nix/store/qfc8729nzpdln1h0hvi1ziclsl3m84sr-thunderbird-78.5.1
  ├───lib/thunderbird/libxul.so: …6wrw-libxcb-1.14/lib:/nix/store/adzfjjh8w25vdr0xdx9x16ah4f5rqrw5-libX11-1.7.0/lib:/nix/store/ssf…
  │   → /nix/store/adzfjjh8w25vdr0xdx9x16ah4f5rqrw5-libX11-1.7.0
  ├───lib/thunderbird/libxul.so: …pxyc-libXt-1.2.0/lib:/nix/store/1qj29ipxl2fyi2b13l39hdircq17gnk0-libXdamage-1.1.5/lib:/nix/store…
  │   → /nix/store/1qj29ipxl2fyi2b13l39hdircq17gnk0-libXdamage-1.1.5
  │   ├───lib/libXdamage.so.1.1.0: …-libXfixes-5.0.3/lib:/nix/store/adzfjjh8w25vdr0xdx9x16ah4f5rqrw5-libX11-1.7.0/lib:/nix/store/9l0…
  │   │   → /nix/store/adzfjjh8w25vdr0xdx9x16ah4f5rqrw5-libX11-1.7.0
  …
  ```
* Show why Glibc depends on itself:

  ```
  # nix why-depends nixpkgs#glibc nixpkgs#glibc
  /nix/store/9df65igwjmf2wbw0gbrrgair6piqjgmi-glibc-2.31
  └───lib/ld-2.31.so: …che       Do not use /nix/store/9df65igwjmf2wbw0gbrrgair6piqjgmi-glibc-2.31/etc/ld.so.cache.  --…
      → /nix/store/9df65igwjmf2wbw0gbrrgair6piqjgmi-glibc-2.31
  ```
* Show why Geeqie has a build-time dependency on `systemd`:

  ```
  # nix why-depends --derivation nixpkgs#geeqie nixpkgs#systemd
  /nix/store/drrpq2fqlrbj98bmazrnww7hm1in3wgj-geeqie-1.4.drv
  └───/: …atch.drv",["out"]),("/nix/store/qzh8dyq3lfbk3i1acbp7x9wh3il2imiv-gtk+3-3.24.21.drv",["dev"]),("/…
      → /nix/store/qzh8dyq3lfbk3i1acbp7x9wh3il2imiv-gtk+3-3.24.21.drv
      └───/: …16.0.drv",["dev"]),("/nix/store/8kp79fyslf3z4m3dpvlh6w46iaadz5c2-cups-2.3.3.drv",["dev"]),("/nix…
          → /nix/store/8kp79fyslf3z4m3dpvlh6w46iaadz5c2-cups-2.3.3.drv
          └───/: ….3.1.drv",["out"]),("/nix/store/yd3ihapyi5wbz1kjacq9dbkaq5v5hqjg-systemd-246.4.drv",["dev"]),("/…
              → /nix/store/yd3ihapyi5wbz1kjacq9dbkaq5v5hqjg-systemd-246.4.drv
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#description)

Nix automatically determines potential runtime dependencies between
store paths by scanning for the *hash parts* of store paths. For
instance, if there exists a store path
`/nix/store/9df65igwjmf2wbw0gbrrgair6piqjgmi-glibc-2.31`, and a file
inside another store path contains the string `9df65igw…`, then the
latter store path *refers* to the former, and thus might need it at
runtime. Nix always maintains the existence of the transitive closure
of a store path under the references relationship; it is therefore not
possible to install a store path without having all of its references
present.

Sometimes Nix packages end up with unexpected runtime dependencies;
for instance, a reference to a compiler might accidentally end up in a
binary, causing the former to be in the latter's closure. This kind of
*closure size bloat* is undesirable.

`nix why-depends` allows you to diagnose the cause of such issues. It
shows why the store path *package* depends on the store path
*dependency*, by showing a shortest sequence in the references graph
from the former to the latter. Also, for each node along this path, it
shows a file fragment containing a reference to the next store path in
the sequence.

To show why derivation *package* has a build-time rather than runtime
dependency on derivation *dependency*, use `--derivation`.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#options)

* [`--all`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-all) / `-a`

  Show all edges in the dependency graph leading from *package* to *dependency*, rather than just a shortest path.
* [`--precise`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-precise)

  For each edge in the dependency graph, show the files in the parent that cause the dependency.

## [Common evaluation options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#common-evaluation-options)

* [`--arg`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-arg) *name* *expr*

  Pass the value *expr* as the argument *name* to Nix functions.
* [`--arg-from-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-arg-from-file) *name* *path*

  Pass the contents of file *path* as the argument *name* to Nix functions.
* [`--arg-from-stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-arg-from-stdin) *name*

  Pass the contents of stdin as the argument *name* to Nix functions.
* [`--argstr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-argstr) *name* *string*

  Pass the string *string* as the argument *name* to Nix functions.
* [`--debugger`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-debugger)

  Start an interactive environment if evaluation fails.
* [`--eval-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-eval-store) *store-url*

  The [URL of the Nix store](https://nix.dev/manual/nix/2.32/store/types/#store-url-format)
  to use for evaluation, i.e. to store derivations (`.drv` files) and inputs referenced by them.
* [`--impure`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-impure)

  Allow access to mutable paths and repositories.
* [`--include`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-include) / `-I` *path*

  Add *path* to search path entries used to resolve [lookup paths](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path)

  This option may be given multiple times.

  Paths added through `-I` take precedence over the [`nix-path` configuration setting](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-nix-path) and the [`NIX_PATH` environment variable](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_PATH).
* [`--override-flake`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-override-flake) *original-ref* *resolved-ref*

  Override the flake registries, redirecting *original-ref* to *resolved-ref*.

## [Common flake-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#common-flake-related-options)

* [`--commit-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-commit-lock-file)

  Commit changes to the flake's lock file.
* [`--inputs-from`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-inputs-from) *flake-url*

  Use the inputs of the specified flake as registry entries.
* [`--no-registries`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-no-registries)

  Don't allow lookups in the flake registries.

  > **DEPRECATED**
  >
  > Use [`--no-use-registries`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-registries) instead.
* [`--no-update-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-no-update-lock-file)

  Do not allow any updates to the flake's lock file.
* [`--no-write-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-no-write-lock-file)

  Do not write the flake's newly generated lock file.
* [`--output-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-output-lock-file) *flake-lock-path*

  Write the given lock file instead of `flake.lock` within the top-level flake.
* [`--override-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-override-input) *input-path* *flake-url*

  Override a specific flake input (e.g. `dwarffs/nixpkgs`). This implies `--no-write-lock-file`.
* [`--recreate-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-recreate-lock-file)

  Recreate the flake's lock file from scratch.

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.
* [`--reference-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-reference-lock-file) *flake-lock-path*

  Read the given lock file instead of `flake.lock` within the top-level flake.
* [`--update-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-update-input) *input-path*

  Update a specific flake input (ignoring its previous entry in the lock file).

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--repair`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-repair)

  During evaluation, rewrite missing or corrupted files in the Nix store. During building, rebuild missing or corrupted store paths.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-version)

  Show version information.

## [Options that change the interpretation of](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#options-that-change-the-interpretation-of-installables) [installables](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables)

* [`--derivation`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-derivation)

  Operate on the [store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation) rather than its outputs.
* [`--expr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-expr) *expr*

  Interpret [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression *expr*.
* [`--file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-why-depends#opt-file) / `-f` *file*

  Interpret [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression stored in *file*. If *file* is the character -, then a Nix expression is read from standard input. Implies `--impure`.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.