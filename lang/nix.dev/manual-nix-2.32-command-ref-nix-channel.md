---
url: https://nix.dev/manual/nix/2.32/command-ref/nix-channel
title: nix-channel - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix-channel - Nix 2.32.2 Reference Manual

# [Name](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#name)

`nix-channel` - manage Nix channels

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#synopsis)

`nix-channel` {`--add` url [*name*] | `--remove` *name* | `--list` | `--update` [*names…*] | `--list-generations` | `--rollback` [*generation*] }

# [Description](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#description)

Channels are a mechanism for referencing remote Nix expressions and conveniently retrieving their latest version.

The moving parts of channels are:

* The official channels listed at <https://nixos.org/channels>
* The user-specific list of [subscribed channels](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#subscribed-channels)
* The [downloaded channel contents](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#channels)
* The [Nix expression search path](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-nix-path), set with the [`-I` option](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-i) or the [`NIX_PATH` environment variable](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-NIX_PATH)

> **Note**
>
> The state of a subscribed channel is external to the Nix expressions relying on it.
> This may limit reproducibility.
>
> Dependencies on other Nix expressions can be declared explicitly with:
>
> * [`fetchurl`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-fetchurl), [`fetchTarball`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-fetchTarball), or [`fetchGit`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-fetchGit) in Nix expressions
> * the [`-I` option](https://nix.dev/manual/nix/2.32/command-ref/opt-common#opt-I) in command line invocations

This command has the following operations:

* `--add` *url* [*name*]

  Add a channel *name* located at *url* to the list of subscribed channels.
  If *name* is omitted, default to the last component of *url*, with the suffixes `-stable` or `-unstable` removed.

  > **Note**
  >
  > `--add` does not automatically perform an update.
  > Use `--update` explicitly.

  A channel URL must point to a directory containing a file `nixexprs.tar.gz`.
  At the top level, that tarball must contain a single directory with a `default.nix` file that serves as the channel’s entry point.
* `--remove` *name*

  Remove the channel *name* from the list of subscribed channels.
* `--list`

  Print the names and URLs of all subscribed channels on standard output.
* `--update` [*names*…]

  Download the Nix expressions of subscribed channels and create a new generation.
  Update all channels if none is specified, and only those included in *names* otherwise.

  > **Note**
  >
  > Downloaded channel contents are cached.
  > Use `--tarball-ttl` or the [`tarball-ttl` configuration option](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-tarball-ttl) to change the validity period of cached downloads.
* `--list-generations`

  Prints a list of all the current existing generations for the
  channel profile.

  Works the same way as

  ```
  nix-env --profile /nix/var/nix/profiles/per-user/$USER/channels --list-generations
  ```
* `--rollback` [*generation*]

  Revert channels to the state before the last call to `nix-channel --update`.
  Optionally, you can specify a specific channel *generation* number to restore.

# [Common Options](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#common-options)

Most Nix commands accept the following command-line options:

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-help)

  Prints out a summary of the command syntax and exits.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-version)

  Prints out the Nix version number on standard output and exits.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-verbose) / `-v`

  Increases the level of verbosity of diagnostic messages printed on standard error.
  For each Nix operation, the information printed on standard output is well-defined;
  any diagnostic information is printed on standard error, never on standard output.

  This option may be specified repeatedly.
  Currently, the following verbosity levels exist:

  + `0` “Errors only”

    Only print messages explaining why the Nix invocation failed.
  + `1` “Informational”

    Print *useful* messages about what Nix is doing.
    This is the default.
  + `2` “Talkative”

    Print more informational messages.
  + `3` “Chatty”

    Print even more informational messages.
  + `4` “Debug”

    Print debug information.
  + `5` “Vomit”

    Print vast amounts of debug information.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-quiet)

  Decreases the level of verbosity of diagnostic messages printed on standard error.
  This is the inverse option to `-v` / `--verbose`.

  This option may be specified repeatedly.
  See the previous verbosity levels list.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-log-format) *format*

  This option can be used to change the output of the log format, with *format* being one of:

  + `raw`

    This is the raw format, as outputted by nix-build.
  + `internal-json`

    Outputs the logs in a structured manner.

    > **Warning**
    >
    > While the schema itself is relatively stable, the format of
    > the error-messages (namely of the `msg`-field) can change
    > between releases.
  + `bar`

    Only display a progress bar during the builds.
  + `bar-with-logs`

    Display the raw logs, with the progress bar at the bottom.
* [`--no-build-output`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-no-build-output) / `-Q`

  By default, output written by builders to standard output and standard error is echoed to the Nix command's standard error.
  This option suppresses this behaviour.
  Note that the builder's standard output and error are always written to a log file in `prefix/nix/var/log/nix`.
* [`--max-jobs`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-max-jobs) / `-j` *number*

  Sets the maximum number of build jobs that Nix will perform in parallel to the specified number.
  Specify `auto` to use the number of CPUs in the system.
  The default is specified by the `max-jobs` configuration setting, which itself defaults to `1`.
  A higher value is useful on SMP systems or to exploit I/O latency.

  Setting it to `0` disallows building on the local machine, which is useful when you want builds to happen only on remote builders.
* [`--cores`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-cores)

  Sets the value of the `NIX_BUILD_CORES` environment variable in the invocation of builders.
  Builders can use this variable at their discretion to control the maximum amount of parallelism.
  For instance, in Nixpkgs, if the derivation attribute `enableParallelBuilding` is set to `true`, the builder passes the `-jN` flag to GNU Make.
  It defaults to the value of the `cores` configuration setting, if set, or `1` otherwise.
  The value `0` means that the builder should use all available CPU cores in the system.
* [`--max-silent-time`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-max-silent-time)

  Sets the maximum number of seconds that a builder can go without producing any data on standard output or standard error.
  The default is specified by the `max-silent-time` configuration setting.
  `0` means no time-out.
* [`--timeout`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-timeout)

  Sets the maximum number of seconds that a builder can run.
  The default is specified by the `timeout` configuration setting.
  `0` means no timeout.
* [`--keep-going`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-keep-going) / `-k`

  Keep going in case of failed builds, to the greatest extent possible.
  That is, if building an input of some derivation fails, Nix will still build the other inputs, but not the derivation itself.
  Without this option, Nix stops if any build fails (except for builds of substitutes), possibly killing builds in progress (in case of parallel or distributed builds).
* [`--keep-failed`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-keep-failed) / `-K`

  Specifies that in case of a build failure, the temporary directory (usually in `/tmp`) in which the build takes place should not be deleted.
  The path of the build directory is printed as an informational message.
* [`--fallback`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-fallback)

  Whenever Nix attempts to build a derivation for which substitutes are known for each output path, but realising the output paths through the substitutes fails, fall back on building the derivation.

  The most common scenario in which this is useful is when we have registered substitutes in order to perform binary distribution from, say, a network repository.
  If the repository is down, the realisation of the derivation will fail.
  When this option is specified, Nix will build the derivation instead.
  Thus, installation from binaries falls back on installation from source.
  This option is not the default since it is generally not desirable for a transient failure in obtaining the substitutes to lead to a full build from source (with the related consumption of resources).
* [`--readonly-mode`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-readonly-mode)

  When this option is used, no attempt is made to open the Nix database.
  Most Nix operations do need database access, so those operations will fail.
* [`--arg`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-arg) *name* *value*

  This option is accepted by `nix-env`, `nix-instantiate`, `nix-shell` and `nix-build`.
  When evaluating Nix expressions, the expression evaluator will automatically try to call functions that it encounters.
  It can automatically call functions for which every argument has a [default value](https://nix.dev/manual/nix/2.32/language/syntax#functions) (e.g., `{ argName ? defaultValue }: ...`).

  With `--arg`, you can also call functions that have arguments without a default value (or override a default value).
  That is, if the evaluator encounters a function with an argument named *name*, it will call it with value *value*.

  For instance, the top-level `default.nix` in Nixpkgs is actually a function:

  ```
  { # The system (e.g., `i686-linux') for which to build the packages.
    system ? builtins.currentSystem
    ...
  }: ...
  ```

  So if you call this Nix expression (e.g., when you do `nix-env --install --attr pkgname`), the function will be called automatically using the value [`builtins.currentSystem`](https://nix.dev/manual/nix/2.32/language/builtins) for the `system` argument.
  You can override this using `--arg`, e.g., `nix-env --install --attr pkgname --arg system \"i686-freebsd\"`.
  (Note that since the argument is a Nix string literal, you have to escape the quotes.)
* [`--arg-from-file`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-arg-from-file) *name* *path*

  Pass the contents of file *path* as the argument *name* to Nix functions.
* [`--arg-from-stdin`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-arg-from-stdin) *name*

  Pass the contents of stdin as the argument *name* to Nix functions.
* [`--argstr`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-argstr) *name* *value*

  This option is like `--arg`, only the value is not a Nix expression but a string.
  So instead of `--arg system \"i686-linux\"` (the outer quotes are to keep the shell happy) you can say `--argstr system i686-linux`.
* [`--attr`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-attr) / `-A` *attrPath*

  Select an attribute from the top-level Nix expression being evaluated.
  (`nix-env`, `nix-instantiate`, `nix-build` and `nix-shell` only.)
  The *attribute path* *attrPath* is a sequence of attribute names separated by dots.
  For instance, given a top-level Nix expression *e*, the attribute path `xorg.xorgserver` would cause the expression `e.xorg.xorgserver` to be used.
  See [`nix-env --install`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install) for some concrete examples.

  In addition to attribute names, you can also specify array indices.
  For instance, the attribute path `foo.3.bar` selects the `bar`
  attribute of the fourth element of the array in the `foo` attribute
  of the top-level expression.
* [`--eval-store`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-eval-store) *store-url*

  The [URL to the Nix store](https://nix.dev/manual/nix/2.32/store/types/#store-url-format) to use for evaluation, i.e. where to store derivations (`.drv` files) and inputs referenced by them.
* [`--expr`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-expr) / `-E`

  Interpret the command line arguments as a list of Nix expressions to be parsed and evaluated, rather than as a list of file names of Nix expressions.
  (`nix-instantiate`, `nix-build` and `nix-shell` only.)

  For `nix-shell`, this option is commonly used to give you a shell in which you can build the packages returned by the expression.
  If you want to get a shell which contain the *built* packages ready for use, give your expression to the `nix-shell --packages`  convenience flag instead.
* [`-I` / `--include`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-I) *path*

  Add an entry to the list of search paths used to resolve [lookup paths](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path).
  This option may be given multiple times.

  Paths added through `-I` take precedence over the [`nix-path` configuration setting](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-nix-path) and the [`NIX_PATH` environment variable](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_PATH).
* [`--impure`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-impure)

  Allow access to mutable paths and repositories.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-option) *name* *value*

  Set the Nix configuration option *name* to *value*.
  This overrides settings in the Nix configuration file (see nix.conf5).
* [`--repair`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#opt-repair)

  Fix corrupted or missing store paths by redownloading or rebuilding them.
  Note that this is slow because it requires computing a cryptographic hash of the contents of every path in the closure of the build.
  Also note the warning under `nix-store --repair-path`.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.

# [Common Environment Variables](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#common-environment-variables)

Most Nix commands interpret the following environment variables:

* [`IN_NIX_SHELL`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-IN_NIX_SHELL)

  Indicator that tells if the current environment was set up by
  `nix-shell`. It can have the values `pure` or `impure`.
* [`NIX_PATH`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-NIX_PATH)

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
* [`NIX_IGNORE_SYMLINK_STORE`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-NIX_IGNORE_SYMLINK_STORE)

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
* [`NIX_STORE_DIR`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-NIX_STORE_DIR)

  Overrides the location of the Nix store (default `prefix/store`).
* [`NIX_DATA_DIR`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-NIX_DATA_DIR)

  Overrides the location of the Nix static data directory (default
  `prefix/share`).
* [`NIX_LOG_DIR`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-NIX_LOG_DIR)

  Overrides the location of the Nix log directory (default
  `prefix/var/log/nix`).
* [`NIX_STATE_DIR`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-NIX_STATE_DIR)

  Overrides the location of the Nix state directory (default
  `prefix/var/nix`).
* [`NIX_CONF_DIR`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-NIX_CONF_DIR)

  Overrides the location of the system Nix configuration directory
  (default `sysconfdir/nix`, i.e. `/etc/nix` on most systems).
* [`NIX_CONFIG`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-NIX_CONFIG)

  Applies settings from Nix configuration from the environment.
  The content is treated as if it was read from a Nix configuration file.
  Settings are separated by the newline character.
* [`NIX_USER_CONF_FILES`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-NIX_USER_CONF_FILES)

  Overrides the location of the Nix user configuration files to load from.

  The default are the locations according to the [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html).
  See the [XDG Base Directories](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#xdg-base-directories) sub-section for details.

  The variable is treated as a list separated by the `:` token.
* [`TMPDIR`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-TMPDIR)

  Use the specified directory to store temporary files. In particular,
  this includes temporary build directories; these can take up
  substantial amounts of disk space. The default is `/tmp`.
* [`NIX_REMOTE`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-NIX_REMOTE)

  This variable should be set to `daemon` if you want to use the Nix
  daemon to execute Nix operations. This is necessary in [multi-user
  Nix installations](https://nix.dev/manual/nix/2.32/installation/multi-user). If the Nix
  daemon's Unix socket is at some non-standard path, this variable
  should be set to `unix://path/to/socket`. Otherwise, it should be
  left unset.
* [`NIX_SHOW_STATS`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-NIX_SHOW_STATS)

  If set to `1`, Nix will print some evaluation statistics, such as
  the number of values allocated.
* [`NIX_COUNT_CALLS`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-NIX_COUNT_CALLS)

  If set to `1`, Nix will print how often functions were called during
  Nix expression evaluation. This is useful for profiling your Nix
  expressions.
* [`GC_INITIAL_HEAP_SIZE`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-GC_INITIAL_HEAP_SIZE)

  If Nix has been configured to use the Boehm garbage collector, this
  variable sets the initial size of the heap in bytes. It defaults to
  384 MiB. Setting it to a low value reduces memory consumption, but
  will increase runtime due to the overhead of garbage collection.

## [XDG Base Directories](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#xdg-base-directories)

Nix follows the [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html).

For backwards compatibility, Nix commands will follow the standard only when [`use-xdg-base-directories`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-xdg-base-directories) is enabled.
[New Nix commands](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix) (experimental) conform to the standard by default.

The following environment variables are used to determine locations of various state and configuration files:

* [`XDG_CONFIG_HOME`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-XDG_CONFIG_HOME) (default `~/.config`)
* [`XDG_STATE_HOME`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-XDG_STATE_HOME) (default `~/.local/state`)
* [`XDG_CACHE_HOME`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-XDG_CACHE_HOME) (default `~/.cache`)

In addition, setting the following environment variables overrides the XDG base directories:

* [`NIX_CONFIG_HOME`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-NIX_CONFIG_HOME) (default `$XDG_CONFIG_HOME/nix`)
* [`NIX_STATE_HOME`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-NIX_STATE_HOME) (default `$XDG_STATE_HOME/nix`)
* [`NIX_CACHE_HOME`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#env-NIX_CACHE_HOME) (default `$XDG_CACHE_HOME/nix`)

When [`use-xdg-base-directories`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-xdg-base-directories) is enabled, the configuration directory is:

1. `$NIX_CONFIG_HOME`, if it is defined
2. Otherwise, `$XDG_CONFIG_HOME/nix`, if `XDG_CONFIG_HOME` is defined
3. Otherwise, `~/.config/nix`.

Likewise for the state and cache directories.

# [Files](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#files)

`nix-channel` operates on the following files.

## [Channels](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#channels)

A directory containing symlinks to Nix channels, managed by [`nix-channel`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel):

* `$XDG_STATE_HOME/nix/profiles/channels` for regular users
* `$NIX_STATE_DIR/profiles/per-user/root/channels` for `root`

[`nix-channel`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel) uses a [profile](https://nix.dev/manual/nix/2.32/command-ref/files/profiles) to store channels.
This profile contains symlinks to the contents of those channels.

## [Subscribed channels](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#subscribed-channels)

The list of subscribed channels is stored in

* `~/.nix-channels`
* `$XDG_STATE_HOME/nix/channels` if [`use-xdg-base-directories`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-xdg-base-directories) is set to `true`

in the following format:

```
<url> <name>
...
```

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/nix-channel#examples)

Subscribe to the Nixpkgs channel and run `hello` from the GNU Hello package:

```
$ nix-channel --add https://nixos.org/channels/nixpkgs-unstable
$ nix-channel --list
nixpkgs https://nixos.org/channels/nixpkgs
$ nix-channel --update
$ nix-shell -p hello --run hello
hello
```

Revert channel updates using `--rollback`:

```
$ nix-instantiate --eval '<nixpkgs>' --attr lib.version
"22.11pre296212.530a53dcbc9"

$ nix-channel --rollback
switching from generation 483 to 482

$ nix-instantiate --eval '<nixpkgs>' --attr lib.version
"22.11pre281526.d0419badfad"
```

Remove a channel:

```
$ nix-channel --remove nixpkgs
$ nix-channel --list
```