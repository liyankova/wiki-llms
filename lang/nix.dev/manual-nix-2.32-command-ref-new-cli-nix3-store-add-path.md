---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-path
title: nix store add-path - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix store add-path - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-path#name)

`nix store add-path` - Deprecated alias to [`nix store add`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add).

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-path#synopsis)

`nix store add-path` [*option*...] *path*

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-path#options)

* [`--dry-run`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-path#opt-dry-run)

  Show what this command would do without doing it.
* [`--hash-algo`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-path#opt-hash-algo) *hash-algo*

  Hash algorithm (`blake3`, `md5`, `sha1`, `sha256`, or `sha512`).
* [`--mode`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-path#opt-mode) *content-address-method*

  How to compute the content-address of the store object.
  One of:

  + [`nar`](https://nix.dev/manual/nix/2.32/store/store-object/content-address#method-nix-archive)
    (the default):
    Serialises the input as a
    [Nix Archive](https://nix.dev/manual/nix/2.32/store/file-system-object/content-address#serial-nix-archive)
    and passes that to the hash function.
  + [`flat`](https://nix.dev/manual/nix/2.32/store/store-object/content-address#method-flat):
    Assumes that the input is a single file and
    [directly passes](https://nix.dev/manual/nix/2.32/store/file-system-object/content-address#serial-flat)
    it to the hash function.
  + [`text`](https://nix.dev/manual/nix/2.32/store/store-object/content-address#method-text):
    Like `flat`, but used for
    [derivations](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation) serialized in store object and
    [`builtins.toFile`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-toFile).
    For advanced use-cases only;
    for regular usage prefer `nar` and `flat`.
* [`--name`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-path#opt-name) / `-n` *name*

  Override the name component of the store path. It defaults to the base name of *path*.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-path#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-path#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-path#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-path#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-path#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-path#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-path#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-path#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-path#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-path#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-path#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-add-path#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.