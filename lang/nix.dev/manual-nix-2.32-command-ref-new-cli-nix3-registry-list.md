---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-list
title: nix registry list - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix registry list - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-list#name)

`nix registry list` - list available Nix flakes

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-list#synopsis)

`nix registry list` [*option*...]

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-list#examples)

* Show the contents of all registries:

  ```
  # nix registry list
  user   flake:dwarffs github:edolstra/dwarffs/d181d714fd36eb06f4992a1997cd5601e26db8f5
  system flake:nixpkgs path:/nix/store/fxl9mrm5xvzam0lxi9ygdmksskx4qq8s-source?lastModified=1605220118&narHash=sha256-Und10ixH1WuW0XHYMxxuHRohKYb45R%2fT8CwZuLd2D2Q=&rev=3090c65041104931adda7625d37fa874b2b5c124
  global flake:blender-bin github:edolstra/nix-warez?dir=blender
  global flake:dwarffs github:edolstra/dwarffs
  …
  ```

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-list#description)

This command displays the contents of all registries on standard
output. Each line represents one registry entry in the format *type*
*from* *to*, where *type* denotes the registry containing the entry:

* `flags`: entries specified on the command line using `--override-flake`.
* `user`: the user registry.
* `system`: the system registry.
* `global`: the global registry.

See the [`nix registry` manual page](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry) for more details.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-list#options)

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-list#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-list#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-list#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-list#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-list#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-list#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-list#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-list#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-list#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-list#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-list#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-registry-list#opt-version)

  Show version information.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.