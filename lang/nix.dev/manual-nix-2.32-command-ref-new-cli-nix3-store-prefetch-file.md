---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file
title: nix store prefetch-file - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix store prefetch-file - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#name)

`nix store prefetch-file` - download a file into the Nix store

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#synopsis)

`nix store prefetch-file` [*option*...] *url*

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#examples)

* Download a file to the Nix store:

  ```
  # nix store prefetch-file https://releases.nixos.org/nix/nix-2.3.10/nix-2.3.10.tar.xz
  Downloaded 'https://releases.nixos.org/nix/nix-2.3.10/nix-2.3.10.tar.xz' to
  '/nix/store/vbdbi42hgnc4h7pyqzp6h2yf77kw93aw-source' (hash
  'sha256-qKheVd5D0BervxMDbt+1hnTKE2aRWC8XCAwc0SeHt6s=').
  ```
* Download a file and get the SHA-512 hash:

  ```
  # nix store prefetch-file --json --hash-type sha512 \
      https://releases.nixos.org/nix/nix-2.3.10/nix-2.3.10.tar.xz \
    | jq -r .hash
  sha512-6XJxfym0TNH9knxeH4ZOvns6wElFy3uahunl2hJgovACCMEMXSy42s69zWVyGJALXTI+86tpDJGlIcAySEKBbA==
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#description)

This command downloads the file *url* to the Nix store. It prints out
the resulting store path and the cryptographic hash of the contents of
the file.

The name component of the store path defaults to the last component of
*url*, but this can be overridden using `--name`.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#options)

* [`--executable`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#opt-executable)

  Make the resulting file executable. Note that this causes the resulting hash to be a NAR hash rather than a flat file hash.
* [`--expected-hash`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#opt-expected-hash) *hash*

  The expected hash of the file.
* [`--hash-type`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#opt-hash-type) *hash-algo*

  Hash algorithm (`blake3`, `md5`, `sha1`, `sha256`, or `sha512`).
* [`--json`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#opt-json)

  Produce output in JSON format, suitable for consumption by another program.
* [`--name`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#opt-name) *name*

  Override the name component of the resulting store path. It defaults to the base name of *url*.
* [`--no-pretty`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#opt-no-pretty)

  Print compact JSON output on a single line, even when the output is a terminal.
  Some commands may print multiple JSON objects on separate lines.

  ```
                See `--pretty`.
  ```
* [`--pretty`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#opt-pretty)

  Print multi-line, indented JSON output for readability.

  ```
                Default: indent if output is to a terminal.

                This option is only effective when `--json` is also specified.
  ```
* [`--unpack`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#opt-unpack)

  Unpack the archive (which must be a tarball or zip file) and add the result to the Nix store.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-store-prefetch-file#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.