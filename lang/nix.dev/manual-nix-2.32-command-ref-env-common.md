---
url: https://nix.dev/manual/nix/2.32/command-ref/env-common
title: Common Environment Variables - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Common Environment Variables - Nix 2.32.2 Reference Manual

# [Common Environment Variables](https://nix.dev/manual/nix/2.32/command-ref/env-common#common-environment-variables)

Most Nix commands interpret the following environment variables:

* [`IN_NIX_SHELL`](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-IN_NIX_SHELL)

  Indicator that tells if the current environment was set up by
  `nix-shell`. It can have the values `pure` or `impure`.
* [`NIX_PATH`](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_PATH)

  A colon-separated list of search path entries used to resolve [lookup paths](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path).

  This environment variable overrides the value of the [`nix-path` configuration setting](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-nix-path).

  It can be extended using the [`-I` option](https://nix.dev/manual/nix/2.32/command-ref/opt-common#opt-I).

  > **Example**
  >
  > ```
  > $ export NIX_PATH=`/home/eelco/Dev:nixos-config=/etc/nixos
  > ```

  If `NIX_PATH` is set to an empty string, resolving search paths will always fail.

  > **Example**
  >
  > ```
  > $ NIX_PATH= nix-instantiate --eval '<nixpkgs>'
  > error: file 'nixpkgs' was not found in the Nix search path (add it using $NIX_PATH or -I)
  > ```
* [`NIX_IGNORE_SYMLINK_STORE`](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_IGNORE_SYMLINK_STORE)

  Normally, the Nix store directory (typically `/nix/store`) is not
  allowed to contain any symlink components. This is to prevent
  “impure” builds. Builders sometimes “canonicalise” paths by
  resolving all symlink components. Thus, builds on different machines
  (with `/nix/store` resolving to different locations) could yield
  different results. This is generally not a problem, except when
  builds are deployed to machines where `/nix/store` resolves
  differently. If you are sure that you’re not going to do that, you
  can set `NIX_IGNORE_SYMLINK_STORE` to `1`.

  Note that if you’re symlinking the Nix store so that you can put it
  on another file system than the root file system, on Linux you’re
  better off using `bind` mount points, e.g.,

  ```
  $ mkdir /nix
  $ mount -o bind /mnt/otherdisk/nix /nix
  ```

  Consult the mount 8 manual page for details.
* [`NIX_STORE_DIR`](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_STORE_DIR)

  Overrides the location of the Nix store (default `prefix/store`).
* [`NIX_DATA_DIR`](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_DATA_DIR)

  Overrides the location of the Nix static data directory (default
  `prefix/share`).
* [`NIX_LOG_DIR`](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_LOG_DIR)

  Overrides the location of the Nix log directory (default
  `prefix/var/log/nix`).
* [`NIX_STATE_DIR`](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_STATE_DIR)

  Overrides the location of the Nix state directory (default
  `prefix/var/nix`).
* [`NIX_CONF_DIR`](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_CONF_DIR)

  Overrides the location of the system Nix configuration directory
  (default `sysconfdir/nix`, i.e. `/etc/nix` on most systems).
* [`NIX_CONFIG`](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_CONFIG)

  Applies settings from Nix configuration from the environment.
  The content is treated as if it was read from a Nix configuration file.
  Settings are separated by the newline character.
* [`NIX_USER_CONF_FILES`](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_USER_CONF_FILES)

  Overrides the location of the Nix user configuration files to load from.

  The default are the locations according to the [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html).
  See the [XDG Base Directories](https://nix.dev/manual/nix/2.32/command-ref/env-common#xdg-base-directories) sub-section for details.

  The variable is treated as a list separated by the `:` token.
* [`TMPDIR`](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-TMPDIR)

  Use the specified directory to store temporary files. In particular,
  this includes temporary build directories; these can take up
  substantial amounts of disk space. The default is `/tmp`.
* [`NIX_REMOTE`](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_REMOTE)

  This variable should be set to `daemon` if you want to use the Nix
  daemon to execute Nix operations. This is necessary in [multi-user
  Nix installations](https://nix.dev/manual/nix/2.32/installation/multi-user). If the Nix
  daemon's Unix socket is at some non-standard path, this variable
  should be set to `unix://path/to/socket`. Otherwise, it should be
  left unset.
* [`NIX_SHOW_STATS`](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_SHOW_STATS)

  If set to `1`, Nix will print some evaluation statistics, such as
  the number of values allocated.
* [`NIX_COUNT_CALLS`](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_COUNT_CALLS)

  If set to `1`, Nix will print how often functions were called during
  Nix expression evaluation. This is useful for profiling your Nix
  expressions.
* [`GC_INITIAL_HEAP_SIZE`](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-GC_INITIAL_HEAP_SIZE)

  If Nix has been configured to use the Boehm garbage collector, this
  variable sets the initial size of the heap in bytes. It defaults to
  384 MiB. Setting it to a low value reduces memory consumption, but
  will increase runtime due to the overhead of garbage collection.

## [XDG Base Directories](https://nix.dev/manual/nix/2.32/command-ref/env-common#xdg-base-directories)

Nix follows the [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html).

For backwards compatibility, Nix commands will follow the standard only when [`use-xdg-base-directories`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-xdg-base-directories) is enabled.
[New Nix commands](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix) (experimental) conform to the standard by default.

The following environment variables are used to determine locations of various state and configuration files:

* [`XDG_CONFIG_HOME`](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-XDG_CONFIG_HOME) (default `~/.config`)
* [`XDG_STATE_HOME`](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-XDG_STATE_HOME) (default `~/.local/state`)
* [`XDG_CACHE_HOME`](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-XDG_CACHE_HOME) (default `~/.cache`)

In addition, setting the following environment variables overrides the XDG base directories:

* [`NIX_CONFIG_HOME`](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_CONFIG_HOME) (default `$XDG_CONFIG_HOME/nix`)
* [`NIX_STATE_HOME`](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_STATE_HOME) (default `$XDG_STATE_HOME/nix`)
* [`NIX_CACHE_HOME`](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_CACHE_HOME) (default `$XDG_CACHE_HOME/nix`)

When [`use-xdg-base-directories`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-xdg-base-directories) is enabled, the configuration directory is:

1. `$NIX_CONFIG_HOME`, if it is defined
2. Otherwise, `$XDG_CONFIG_HOME/nix`, if `XDG_CONFIG_HOME` is defined
3. Otherwise, `~/.config/nix`.

Likewise for the state and cache directories.