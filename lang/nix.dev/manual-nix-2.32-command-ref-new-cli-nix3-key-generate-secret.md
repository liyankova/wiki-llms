---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-generate-secret
title: nix key generate-secret - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix key generate-secret - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-generate-secret#name)

`nix key generate-secret` - generate a secret key for signing store paths

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-generate-secret#synopsis)

`nix key generate-secret` [*option*...]

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-generate-secret#examples)

* Generate a new secret key:

  ```
  # nix key generate-secret --key-name cache.example.org-1 > ./secret-key
  ```

  We can then use this key to sign the closure of the Hello package:

  ```
  # nix build nixpkgs#hello
  # nix store sign --key-file ./secret-key --recursive ./result
  ```

  Finally, we can verify the store paths using the corresponding
  public key:

  ```
  # nix store verify --trusted-public-keys $(nix key convert-secret-to-public < ./secret-key) ./result
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-generate-secret#description)

This command generates a new Ed25519 secret key for signing store
paths and prints it on standard output. Use `nix key convert-secret-to-public` to get the corresponding public key for
verifying signed store paths.

The mandatory argument `--key-name` specifies a key name (such as
`cache.example.org-1`). It is used to look up keys on the client when
it verifies signatures. It can be anything, but it’s suggested to use
the host name of your cache (e.g. `cache.example.org`) with a suffix
denoting the number of the key (to be incremented every time you need
to revoke a key).

# [Format](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-generate-secret#format)

Both secret and public keys are represented as the key name followed
by a base-64 encoding of the Ed25519 key data, e.g.

```
cache.example.org-0:E7lAO+MsPwTFfPXsdPtW8GKui/5ho4KQHVcAGnX+Tti1V4dUxoVoqLyWJ4YESuZJwQ67GVIksDt47og+tPVUZw==
```

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-generate-secret#options)

* [`--key-name`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-generate-secret#opt-key-name) *name*

  Identifier of the key (e.g. `cache.example.org-1`).

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-generate-secret#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-generate-secret#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-generate-secret#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-generate-secret#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-generate-secret#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-generate-secret#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-generate-secret#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-generate-secret#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-generate-secret#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-generate-secret#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-generate-secret#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-key-generate-secret#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.