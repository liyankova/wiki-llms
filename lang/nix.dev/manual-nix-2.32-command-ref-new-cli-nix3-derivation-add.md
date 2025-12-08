---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-add
title: nix derivation add - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix derivation add - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-add#name)

`nix derivation add` - Add a store derivation

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-add#synopsis)

`nix derivation add` [*option*...]

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-add#description)

This command reads from standard input a JSON representation of a
[store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation).

Store derivations are used internally by Nix. They are store paths with
extension `.drv` that represent the build-time dependency graph to which
a Nix expression evaluates.

`nix derivation add` takes a single derivation in the following format:

# [Derivation JSON Format](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-add#derivation-json-format)

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

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-add#options)

* [`--dry-run`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-add#opt-dry-run)

  Show what this command would do without doing it.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-add#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-add#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-add#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-add#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-add#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-add#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-add#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-add#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-add#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-add#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-add#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-derivation-add#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.