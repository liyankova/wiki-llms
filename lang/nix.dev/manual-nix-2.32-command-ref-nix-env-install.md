---
url: https://nix.dev/manual/nix/2.32/command-ref/nix-env/install
title: nix-env --install - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix-env --install - Nix 2.32.2 Reference Manual

# [Name](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#name)

`nix-env --install` - add packages to user environment

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#synopsis)

`nix-env` {`--install` | `-i`} *args…*
[{`--prebuilt-only` | `-b`}]
[{`--attr` | `-A`}]
[`--from-expression`] [`-E`]
[`--from-profile` *path*]
[`--preserve-installed` | `-P`]
[`--remove-all` | `-r`]
[`--priority` *priority*]

# [Description](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#description)

The `--install` operation creates a new user environment.
It is based on the current generation of the active [profile](https://nix.dev/manual/nix/2.32/command-ref/files/profiles), to which a set of [store paths](https://nix.dev/manual/nix/2.32/store/store-path) described by *args* is added.

The arguments *args* map to store paths in a number of possible ways:

* By default, *args* is a set of names denoting derivations in the [default Nix expression](https://nix.dev/manual/nix/2.32/command-ref/files/default-nix-expression).
  These are [realised](https://nix.dev/manual/nix/2.32/glossary#gloss-realise), and the resulting output paths are installed.
  Currently installed derivations with a name equal to the name of a derivation being added are removed unless the option `--preserve-installed` is specified.

  If there are multiple derivations matching a name in *args* that
  have the same name (e.g., `gcc-3.3.6` and `gcc-4.1.1`), then the
  derivation with the highest *priority* is used. A derivation can
  define a priority by declaring the `meta.priority` attribute. This
  attribute should be a number, with a higher value denoting a lower
  priority. The default priority is `5`.

  If there are multiple matching derivations with the same priority,
  then the derivation with the highest version will be installed.

  You can force the installation of multiple derivations with the same
  name by being specific about the versions. For instance, `nix-env --install gcc-3.3.6 gcc-4.1.1` will install both version of GCC (and will
  probably cause a user environment conflict!).
* If [`--attr`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-attr) / `-A` is specified, the arguments are *attribute paths* that select attributes from the [default Nix expression](https://nix.dev/manual/nix/2.32/command-ref/files/default-nix-expression).
  This is faster than using derivation names and unambiguous.
  Show the attribute paths of available packages with [`nix-env --query`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/query):

  ```
  nix-env --query --available --attr-path
  ```
* If `--from-profile` *path* is given, *args* is a set of names
  denoting installed [store paths](https://nix.dev/manual/nix/2.32/store/store-path) in the profile *path*. This is an
  easy way to copy user environment elements from one profile to
  another.
* If `--from-expression` is given, *args* are [Nix language functions](https://nix.dev/manual/nix/2.32/language/syntax#functions) that are called with the [default Nix expression](https://nix.dev/manual/nix/2.32/command-ref/files/default-nix-expression) as their single argument.
  The derivations returned by those function calls are installed.
  This allows derivations to be specified in an unambiguous way, which is necessary if there are multiple derivations with the same name.
* If `--priority` *priority* is given, the priority of the derivations being installed is set to *priority*.
  This can be used to override the priority of the derivations being installed.
  This is useful if *args* are [store paths](https://nix.dev/manual/nix/2.32/store/store-path), which don't have any priority information.
* If *args* are [store paths](https://nix.dev/manual/nix/2.32/store/store-path) that point to [store derivations](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation), then those store derivations are [realised](https://nix.dev/manual/nix/2.32/glossary#gloss-realise), and the resulting output paths are installed.
* If *args* are [store paths](https://nix.dev/manual/nix/2.32/store/store-path) that do not point to store derivations, then these are [realised](https://nix.dev/manual/nix/2.32/glossary#gloss-realise) and installed.
* By default all [outputs](https://nix.dev/manual/nix/2.32/language/derivations#attr-outputs) are installed for each [store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation).
  This can be overridden by adding a `meta.outputsToInstall` attribute on the derivation listing a subset of the output names.

  Example:

  The file `example.nix` defines a derivation with two outputs `foo` and `bar`, each containing a file.

  ```
  # example.nix
  let
    pkgs = import <nixpkgs> {};
    command = ''
      ${pkgs.coreutils}/bin/mkdir -p $foo $bar
      echo foo > $foo/foo-file
      echo bar > $bar/bar-file
    '';
  in
  derivation {
    name = "example";
    builder = "${pkgs.bash}/bin/bash";
    args = [ "-c" command ];
    outputs = [ "foo" "bar" ];
    system = builtins.currentSystem;
  }
  ```

  Installing from this Nix expression will make files from both outputs appear in the current profile.

  ```
  $ nix-env --install --file example.nix
  installing 'example'
  $ ls ~/.nix-profile
  foo-file
  bar-file
  manifest.nix
  ```

  Adding `meta.outputsToInstall` to that derivation will make `nix-env` only install files from the specified outputs.

  ```
  # example-outputs.nix
  import ./example.nix // { meta.outputsToInstall = [ "bar" ]; }
  ```

  ```
  $ nix-env --install --file example-outputs.nix
  installing 'example'
  $ ls ~/.nix-profile
  bar-file
  manifest.nix
  ```

# [Options](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#options)

* `--prebuilt-only` / `-b`

  Use only derivations for which a substitute is registered, i.e.,
  there is a pre-built binary available that can be downloaded in lieu
  of building the derivation. Thus, no packages will be built from
  source.
* `--preserve-installed` / `-P`

  Do not remove derivations with a name matching one of the
  derivations being installed. Usually, trying to have two versions of
  the same package installed in the same generation of a profile will
  lead to an error in building the generation, due to file name
  clashes between the two versions. However, this is not the case for
  all packages.
* `--remove-all` / `-r`

  Remove all previously installed packages first. This is equivalent
  to running `nix-env --uninstall '.*'` first, except that everything happens
  in a single transaction.

# [Options](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#options-1)

The following options are allowed for all `nix-env` operations, but may not always have an effect.

* `--file` / `-f` *path*

  Specifies the Nix expression (designated below as the *active Nix
  expression*) used by the `--install`, `--upgrade`, and `--query --available` operations to obtain derivations. The default is
  `~/.nix-defexpr`.

  If the argument starts with `http://` or `https://`, it is
  interpreted as the URL of a tarball that will be downloaded and
  unpacked to a temporary location. The tarball must include a single
  top-level directory containing at least a file named `default.nix`.
* `--profile` / `-p` *path*

  Specifies the profile to be used by those operations that operate on
  a profile (designated below as the *active profile*). A profile is a
  sequence of user environments called *generations*, one of which is
  the *current generation*.
* `--dry-run`

  For the `--install`, `--upgrade`, `--uninstall`,
  `--switch-generation`, `--delete-generations` and `--rollback`
  operations, this flag will cause `nix-env` to print what *would* be
  done if this flag had not been specified, without actually doing it.

  `--dry-run` also prints out which paths will be
  [substituted](https://nix.dev/manual/nix/2.32/glossary) (i.e., downloaded) and which paths
  will be built from source (because no substitute is available).
* `--system-filter` *system*

  By default, operations such as `--query --available` show derivations matching any platform. This option
  allows you to use derivations for the specified platform *system*.

# [Common Options](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#common-options)

Most Nix commands accept the following command-line options:

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-help)

  Prints out a summary of the command syntax and exits.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-version)

  Prints out the Nix version number on standard output and exits.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-verbose) / `-v`

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
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-quiet)

  Decreases the level of verbosity of diagnostic messages printed on standard error.
  This is the inverse option to `-v` / `--verbose`.

  This option may be specified repeatedly.
  See the previous verbosity levels list.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-log-format) *format*

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
* [`--no-build-output`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-no-build-output) / `-Q`

  By default, output written by builders to standard output and standard error is echoed to the Nix command's standard error.
  This option suppresses this behaviour.
  Note that the builder's standard output and error are always written to a log file in `prefix/nix/var/log/nix`.
* [`--max-jobs`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-max-jobs) / `-j` *number*

  Sets the maximum number of build jobs that Nix will perform in parallel to the specified number.
  Specify `auto` to use the number of CPUs in the system.
  The default is specified by the `max-jobs` configuration setting, which itself defaults to `1`.
  A higher value is useful on SMP systems or to exploit I/O latency.

  Setting it to `0` disallows building on the local machine, which is useful when you want builds to happen only on remote builders.
* [`--cores`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-cores)

  Sets the value of the `NIX_BUILD_CORES` environment variable in the invocation of builders.
  Builders can use this variable at their discretion to control the maximum amount of parallelism.
  For instance, in Nixpkgs, if the derivation attribute `enableParallelBuilding` is set to `true`, the builder passes the `-jN` flag to GNU Make.
  It defaults to the value of the `cores` configuration setting, if set, or `1` otherwise.
  The value `0` means that the builder should use all available CPU cores in the system.
* [`--max-silent-time`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-max-silent-time)

  Sets the maximum number of seconds that a builder can go without producing any data on standard output or standard error.
  The default is specified by the `max-silent-time` configuration setting.
  `0` means no time-out.
* [`--timeout`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-timeout)

  Sets the maximum number of seconds that a builder can run.
  The default is specified by the `timeout` configuration setting.
  `0` means no timeout.
* [`--keep-going`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-keep-going) / `-k`

  Keep going in case of failed builds, to the greatest extent possible.
  That is, if building an input of some derivation fails, Nix will still build the other inputs, but not the derivation itself.
  Without this option, Nix stops if any build fails (except for builds of substitutes), possibly killing builds in progress (in case of parallel or distributed builds).
* [`--keep-failed`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-keep-failed) / `-K`

  Specifies that in case of a build failure, the temporary directory (usually in `/tmp`) in which the build takes place should not be deleted.
  The path of the build directory is printed as an informational message.
* [`--fallback`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-fallback)

  Whenever Nix attempts to build a derivation for which substitutes are known for each output path, but realising the output paths through the substitutes fails, fall back on building the derivation.

  The most common scenario in which this is useful is when we have registered substitutes in order to perform binary distribution from, say, a network repository.
  If the repository is down, the realisation of the derivation will fail.
  When this option is specified, Nix will build the derivation instead.
  Thus, installation from binaries falls back on installation from source.
  This option is not the default since it is generally not desirable for a transient failure in obtaining the substitutes to lead to a full build from source (with the related consumption of resources).
* [`--readonly-mode`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-readonly-mode)

  When this option is used, no attempt is made to open the Nix database.
  Most Nix operations do need database access, so those operations will fail.
* [`--arg`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-arg) *name* *value*

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
* [`--arg-from-file`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-arg-from-file) *name* *path*

  Pass the contents of file *path* as the argument *name* to Nix functions.
* [`--arg-from-stdin`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-arg-from-stdin) *name*

  Pass the contents of stdin as the argument *name* to Nix functions.
* [`--argstr`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-argstr) *name* *value*

  This option is like `--arg`, only the value is not a Nix expression but a string.
  So instead of `--arg system \"i686-linux\"` (the outer quotes are to keep the shell happy) you can say `--argstr system i686-linux`.
* [`--attr`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-attr) / `-A` *attrPath*

  Select an attribute from the top-level Nix expression being evaluated.
  (`nix-env`, `nix-instantiate`, `nix-build` and `nix-shell` only.)
  The *attribute path* *attrPath* is a sequence of attribute names separated by dots.
  For instance, given a top-level Nix expression *e*, the attribute path `xorg.xorgserver` would cause the expression `e.xorg.xorgserver` to be used.
  See [`nix-env --install`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install) for some concrete examples.

  In addition to attribute names, you can also specify array indices.
  For instance, the attribute path `foo.3.bar` selects the `bar`
  attribute of the fourth element of the array in the `foo` attribute
  of the top-level expression.
* [`--eval-store`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-eval-store) *store-url*

  The [URL to the Nix store](https://nix.dev/manual/nix/2.32/store/types/#store-url-format) to use for evaluation, i.e. where to store derivations (`.drv` files) and inputs referenced by them.
* [`--expr`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-expr) / `-E`

  Interpret the command line arguments as a list of Nix expressions to be parsed and evaluated, rather than as a list of file names of Nix expressions.
  (`nix-instantiate`, `nix-build` and `nix-shell` only.)

  For `nix-shell`, this option is commonly used to give you a shell in which you can build the packages returned by the expression.
  If you want to get a shell which contain the *built* packages ready for use, give your expression to the `nix-shell --packages`  convenience flag instead.
* [`-I` / `--include`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-I) *path*

  Add an entry to the list of search paths used to resolve [lookup paths](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path).
  This option may be given multiple times.

  Paths added through `-I` take precedence over the [`nix-path` configuration setting](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-nix-path) and the [`NIX_PATH` environment variable](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_PATH).
* [`--impure`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-impure)

  Allow access to mutable paths and repositories.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-option) *name* *value*

  Set the Nix configuration option *name* to *value*.
  This overrides settings in the Nix configuration file (see nix.conf5).
* [`--repair`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#opt-repair)

  Fix corrupted or missing store paths by redownloading or rebuilding them.
  Note that this is slow because it requires computing a cryptographic hash of the contents of every path in the closure of the build.
  Also note the warning under `nix-store --repair-path`.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.

# [Environment variables](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#environment-variables)

* `NIX_PROFILE`

  Location of the Nix profile. Defaults to the target of the symlink
  `~/.nix-profile`, if it exists, or `/nix/var/nix/profiles/default`
  otherwise.

# [Common Environment Variables](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#common-environment-variables)

Most Nix commands interpret the following environment variables:

* [`IN_NIX_SHELL`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#env-IN_NIX_SHELL)

  Indicator that tells if the current environment was set up by
  `nix-shell`. It can have the values `pure` or `impure`.
* [`NIX_PATH`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#env-NIX_PATH)

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
* [`NIX_IGNORE_SYMLINK_STORE`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#env-NIX_IGNORE_SYMLINK_STORE)

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
* [`NIX_STORE_DIR`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#env-NIX_STORE_DIR)

  Overrides the location of the Nix store (default `prefix/store`).
* [`NIX_DATA_DIR`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#env-NIX_DATA_DIR)

  Overrides the location of the Nix static data directory (default
  `prefix/share`).
* [`NIX_LOG_DIR`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#env-NIX_LOG_DIR)

  Overrides the location of the Nix log directory (default
  `prefix/var/log/nix`).
* [`NIX_STATE_DIR`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#env-NIX_STATE_DIR)

  Overrides the location of the Nix state directory (default
  `prefix/var/nix`).
* [`NIX_CONF_DIR`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#env-NIX_CONF_DIR)

  Overrides the location of the system Nix configuration directory
  (default `sysconfdir/nix`, i.e. `/etc/nix` on most systems).
* [`NIX_CONFIG`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#env-NIX_CONFIG)

  Applies settings from Nix configuration from the environment.
  The content is treated as if it was read from a Nix configuration file.
  Settings are separated by the newline character.
* [`NIX_USER_CONF_FILES`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#env-NIX_USER_CONF_FILES)

  Overrides the location of the Nix user configuration files to load from.

  The default are the locations according to the [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html).
  See the [XDG Base Directories](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#xdg-base-directories) sub-section for details.

  The variable is treated as a list separated by the `:` token.
* [`TMPDIR`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#env-TMPDIR)

  Use the specified directory to store temporary files. In particular,
  this includes temporary build directories; these can take up
  substantial amounts of disk space. The default is `/tmp`.
* [`NIX_REMOTE`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#env-NIX_REMOTE)

  This variable should be set to `daemon` if you want to use the Nix
  daemon to execute Nix operations. This is necessary in [multi-user
  Nix installations](https://nix.dev/manual/nix/2.32/installation/multi-user). If the Nix
  daemon's Unix socket is at some non-standard path, this variable
  should be set to `unix://path/to/socket`. Otherwise, it should be
  left unset.
* [`NIX_SHOW_STATS`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#env-NIX_SHOW_STATS)

  If set to `1`, Nix will print some evaluation statistics, such as
  the number of values allocated.
* [`NIX_COUNT_CALLS`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#env-NIX_COUNT_CALLS)

  If set to `1`, Nix will print how often functions were called during
  Nix expression evaluation. This is useful for profiling your Nix
  expressions.
* [`GC_INITIAL_HEAP_SIZE`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#env-GC_INITIAL_HEAP_SIZE)

  If Nix has been configured to use the Boehm garbage collector, this
  variable sets the initial size of the heap in bytes. It defaults to
  384 MiB. Setting it to a low value reduces memory consumption, but
  will increase runtime due to the overhead of garbage collection.

## [XDG Base Directories](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#xdg-base-directories)

Nix follows the [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html).

For backwards compatibility, Nix commands will follow the standard only when [`use-xdg-base-directories`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-xdg-base-directories) is enabled.
[New Nix commands](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix) (experimental) conform to the standard by default.

The following environment variables are used to determine locations of various state and configuration files:

* [`XDG_CONFIG_HOME`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#env-XDG_CONFIG_HOME) (default `~/.config`)
* [`XDG_STATE_HOME`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#env-XDG_STATE_HOME) (default `~/.local/state`)
* [`XDG_CACHE_HOME`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#env-XDG_CACHE_HOME) (default `~/.cache`)

In addition, setting the following environment variables overrides the XDG base directories:

* [`NIX_CONFIG_HOME`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#env-NIX_CONFIG_HOME) (default `$XDG_CONFIG_HOME/nix`)
* [`NIX_STATE_HOME`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#env-NIX_STATE_HOME) (default `$XDG_STATE_HOME/nix`)
* [`NIX_CACHE_HOME`](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#env-NIX_CACHE_HOME) (default `$XDG_CACHE_HOME/nix`)

When [`use-xdg-base-directories`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-xdg-base-directories) is enabled, the configuration directory is:

1. `$NIX_CONFIG_HOME`, if it is defined
2. Otherwise, `$XDG_CONFIG_HOME/nix`, if `XDG_CONFIG_HOME` is defined
3. Otherwise, `~/.config/nix`.

Likewise for the state and cache directories.

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/nix-env/install#examples)

To install a package using a specific attribute path from the active Nix expression:

```
$ nix-env --install --attr gcc40mips
installing `gcc-4.0.2'
$ nix-env --install --attr xorg.xorgserver
installing `xorg-server-1.2.0'
```

To install a specific version of `gcc` using the derivation name:

```
$ nix-env --install gcc-3.3.2
installing `gcc-3.3.2'
uninstalling `gcc-3.1'
```

Using attribute path for selecting a package is preferred,
as it is much faster and there will not be multiple matches.

Note the previously installed version is removed, since
`--preserve-installed` was not specified.

To install an arbitrary version:

```
$ nix-env --install gcc
installing `gcc-3.3.2'
```

To install all derivations in the Nix expression `foo.nix`:

```
$ nix-env --file ~/foo.nix --install '.*'
```

To copy the store path with symbolic name `gcc` from another profile:

```
$ nix-env --install --from-profile /nix/var/nix/profiles/foo gcc
```

To install a specific [store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation) (typically created by
`nix-instantiate`):

```
$ nix-env --install /nix/store/fibjb1bfbpm5mrsxc4mh2d8n37sxh91i-gcc-3.4.3.drv
```

To install a specific output path:

```
$ nix-env --install /nix/store/y3cgx0xj1p4iv9x0pnnmdhr8iyg741vk-gcc-3.4.3
```

To install from a Nix expression specified on the command-line:

```
$ nix-env --file ./foo.nix --install --expr \
    'f: (f {system = "i686-linux";}).subversionWithJava'
```

I.e., this evaluates to `(f: (f {system = "i686-linux";}).subversionWithJava) (import ./foo.nix)`, thus selecting
the `subversionWithJava` attribute from the set returned by calling the
function defined in `./foo.nix`.

A dry-run tells you which paths will be downloaded or built from source:

```
$ nix-env --file '<nixpkgs>' --install --attr hello --dry-run
(dry run; not doing anything)
installing ‘hello-2.10’
this path will be fetched (0.04 MiB download, 0.19 MiB unpacked):
  /nix/store/wkhdf9jinag5750mqlax6z2zbwhqb76n-hello-2.10
  ...
```

To install Firefox from the latest revision in the Nixpkgs/NixOS 14.12
channel:

```
$ nix-env --file https://github.com/NixOS/nixpkgs/archive/nixos-14.12.tar.gz --install --attr firefox
```