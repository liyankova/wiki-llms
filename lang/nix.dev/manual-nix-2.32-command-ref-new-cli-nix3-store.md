---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store
title: nix store - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix store - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store#name)

`nix store` - manipulate a Nix store

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store#synopsis)

`nix store` [*option*...] *subcommand*

where *subcommand* is one of the following:

* [`nix store add`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add) - Add a file or directory to the Nix store
* [`nix store add-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-file) - Deprecated. Use [`nix store add --mode flat`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add) instead.
* [`nix store add-path`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-path) - Deprecated alias to [`nix store add`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add).
* [`nix store cat`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-cat) - print the contents of a file in the Nix store on stdout
* [`nix store copy-log`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-copy-log) - copy build logs between Nix stores
* [`nix store copy-sigs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-copy-sigs) - copy store path signatures from substituters
* [`nix store delete`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-delete) - delete paths from the Nix store
* [`nix store diff-closures`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-diff-closures) - show what packages and versions were added and removed between two closures
* [`nix store dump-path`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-dump-path) - serialise a store path to stdout in NAR format
* [`nix store gc`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-gc) - perform garbage collection on a Nix store
* [`nix store info`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-info) - test whether a store can be accessed
* [`nix store ls`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-ls) - show information about a path in the Nix store
* [`nix store make-content-addressed`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-make-content-addressed) - rewrite a path or closure to content-addressed form
* [`nix store optimise`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-optimise) - replace identical files in the store by hard links
* [`nix store path-from-hash-part`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-path-from-hash-part) - get a store path from its hash part
* [`nix store prefetch-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file) - download a file into the Nix store
* [`nix store repair`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-repair) - repair store paths
* [`nix store sign`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-sign) - sign store paths with a local key
* [`nix store verify`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-verify) - verify the integrity of store paths

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store#options)

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.