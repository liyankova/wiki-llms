---
url: https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell
title: nix env shell - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix env shell - Nix 2.32.2 Reference Manual

> **Warning**   
> This program is
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and its interface is subject to change.

# [Name](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#name)

`nix env shell` - run a shell in which the specified packages are available

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#synopsis)

`nix env shell` [*option*...] *installables*...

# [Examples](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#examples)

* Start a shell providing `youtube-dl` from the `nixpkgs` flake:

  ```
  # nix shell nixpkgs#youtube-dl
  # youtube-dl --version
  2020.11.01.1
  ```
* Start a shell providing GNU Hello from NixOS 20.03:

  ```
  # nix shell nixpkgs/nixos-20.03#hello
  ```
* Run GNU Hello:

  ```
  # nix shell nixpkgs#hello --command hello --greeting 'Hi everybody!'
  Hi everybody!
  ```
* Run multiple commands in a shell environment:

  ```
  # nix shell nixpkgs#gnumake --command sh -c "cd src && make"
  ```
* Run GNU Hello in a chroot store:

  ```
  # nix shell --store ~/my-nix nixpkgs#hello --command hello
  ```
* Start a shell providing GNU Hello in a chroot store:

  ```
  # nix shell --store ~/my-nix nixpkgs#hello nixpkgs#bashInteractive --command bash
  ```

  Note that it's necessary to specify `bash` explicitly because your
  default shell (e.g. `/bin/bash`) generally will not exist in the
  chroot.

# [Description](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#description)

`nix shell` runs a command in an environment in which the `$PATH` variable
provides the specified [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables). If no command is specified, it starts the
default shell of your user account specified by `$SHELL`.

# [Use as a `#!`-interpreter](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#use-as-a--interpreter)

You can use `nix` as a script interpreter to allow scripts written
in arbitrary languages to obtain their own dependencies via Nix. This is
done by starting the script with the following lines:

```
#! /usr/bin/env nix
#! nix shell installables --command real-interpreter
```

where *real-interpreter* is the “real” script interpreter that will be
invoked by `nix shell` after it has obtained the dependencies and
initialised the environment, and *installables* are the attribute names of
the dependencies in Nixpkgs.

The lines starting with `#! nix` specify options (see above). Note that you
cannot write `#! /usr/bin/env nix shell -i ...` because many operating systems
only allow one argument in `#!` lines.

For example, here is a Python script that depends on Python and the
`prettytable` package:

```
#! /usr/bin/env nix
#! nix shell github:tomberek/-#python3With.prettytable --command python

import prettytable

# Print a simple table.
t = prettytable.PrettyTable(["N", "N^2"])
for n in range(1, 10): t.add_row([n, n * n])
print(t)
```

Similarly, the following is a Perl script that specifies that it
requires Perl and the `HTML::TokeParser::Simple` and `LWP` packages:

```
#! /usr/bin/env nix
#! nix shell github:tomberek/-#perlWith.HTMLTokeParserSimple.LWP --command perl -x

use HTML::TokeParser::Simple;

# Fetch nixos.org and print all hrefs.
my $p = HTML::TokeParser::Simple->new(url => 'http://nixos.org/');

while (my $token = $p->get_tag("a")) {
    my $href = $token->get_attr("href");
    print "$href\n" if $href;
}
```

Sometimes you need to pass a simple Nix expression to customize a
package like Terraform:

```
#! /usr/bin/env nix
#! nix shell --impure --expr ``
#! nix with (import (builtins.getFlake ''nixpkgs'') {});
#! nix terraform.withPlugins (plugins: [ plugins.openstack ])
#! nix ``
#! nix --command bash

terraform "$@"
```

> **Note**
>
> You must use double backticks (``` `` ```) when passing a simple Nix expression
> in a nix shell shebang.

Finally, using the merging of multiple nix shell shebangs the following
Haskell script uses a specific branch of Nixpkgs/NixOS (the 21.11 stable
branch):

```
#!/usr/bin/env nix
#!nix shell --override-input nixpkgs github:NixOS/nixpkgs/nixos-21.11
#!nix github:tomberek/-#haskellWith.download-curl.tagsoup --command runghc

import Network.Curl.Download
import Text.HTML.TagSoup
import Data.Either
import Data.ByteString.Char8 (unpack)

-- Fetch nixos.org and print all hrefs.
main = do
  resp <- openURI "https://nixos.org/"
  let tags = filter (isTagOpenName "a") $ parseTags $ unpack $ fromRight undefined resp
  let tags' = map (fromAttrib "href") tags
  mapM_ putStrLn $ filter (/= "") tags'
```

If you want to be even more precise, you can specify a specific revision
of Nixpkgs:

```
#!nix shell --override-input nixpkgs github:NixOS/nixpkgs/eabc38219184cc3e04a974fe31857d8e0eac098d
```

You can also use a Nix expression to build your own dependencies. For example,
the Python example could have been written as:

```
#! /usr/bin/env nix
#! nix shell --impure --file deps.nix -i python
```

where the file `deps.nix` in the same directory as the `#!`-script
contains:

```
with import <nixpkgs> {};
python3.withPackages (ps: with ps; [ prettytable ])
```

# [Options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#options)

* [`--command`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-command) / `-c` *command* *args*

  Command and arguments to be executed, defaulting to `$SHELL`
* [`--stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-stdin)

  Read installables from the standard input. No default installable applied.

## [Common evaluation options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#common-evaluation-options)

* [`--arg`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-arg) *name* *expr*

  Pass the value *expr* as the argument *name* to Nix functions.
* [`--arg-from-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-arg-from-file) *name* *path*

  Pass the contents of file *path* as the argument *name* to Nix functions.
* [`--arg-from-stdin`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-arg-from-stdin) *name*

  Pass the contents of stdin as the argument *name* to Nix functions.
* [`--argstr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-argstr) *name* *string*

  Pass the string *string* as the argument *name* to Nix functions.
* [`--debugger`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-debugger)

  Start an interactive environment if evaluation fails.
* [`--eval-store`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-eval-store) *store-url*

  The [URL of the Nix store](https://nix.dev/manual/nix/2.32/store/types/#store-url-format)
  to use for evaluation, i.e. to store derivations (`.drv` files) and inputs referenced by them.
* [`--impure`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-impure)

  Allow access to mutable paths and repositories.
* [`--include`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-include) / `-I` *path*

  Add *path* to search path entries used to resolve [lookup paths](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path)

  This option may be given multiple times.

  Paths added through `-I` take precedence over the [`nix-path` configuration setting](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-nix-path) and the [`NIX_PATH` environment variable](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_PATH).
* [`--override-flake`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-override-flake) *original-ref* *resolved-ref*

  Override the flake registries, redirecting *original-ref* to *resolved-ref*.

## [Common flake-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#common-flake-related-options)

* [`--commit-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-commit-lock-file)

  Commit changes to the flake's lock file.
* [`--inputs-from`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-inputs-from) *flake-url*

  Use the inputs of the specified flake as registry entries.
* [`--no-registries`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-no-registries)

  Don't allow lookups in the flake registries.

  > **DEPRECATED**
  >
  > Use [`--no-use-registries`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-registries) instead.
* [`--no-update-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-no-update-lock-file)

  Do not allow any updates to the flake's lock file.
* [`--no-write-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-no-write-lock-file)

  Do not write the flake's newly generated lock file.
* [`--output-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-output-lock-file) *flake-lock-path*

  Write the given lock file instead of `flake.lock` within the top-level flake.
* [`--override-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-override-input) *input-path* *flake-url*

  Override a specific flake input (e.g. `dwarffs/nixpkgs`). This implies `--no-write-lock-file`.
* [`--recreate-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-recreate-lock-file)

  Recreate the flake's lock file from scratch.

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.
* [`--reference-lock-file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-reference-lock-file) *flake-lock-path*

  Read the given lock file instead of `flake.lock` within the top-level flake.
* [`--update-input`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-update-input) *input-path*

  Update a specific flake input (ignoring its previous entry in the lock file).

  > **DEPRECATED**
  >
  > Use [`nix flake update`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake-update) instead.

## [Logging-related options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#logging-related-options)

* [`--debug`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-debug)

  Set the logging verbosity level to 'debug'.
* [`--log-format`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-log-format) *format*

  Set the format of log output; one of `raw`, `internal-json`, `bar` or `bar-with-logs`.
* [`--print-build-logs`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-print-build-logs) / `-L`

  Print full build logs on standard error.
* [`--quiet`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-quiet)

  Decrease the logging verbosity level.
* [`--verbose`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-verbose) / `-v`

  Increase the logging verbosity level.

## [Miscellaneous global options](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#miscellaneous-global-options)

* [`--help`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-help)

  Show usage information.
* [`--offline`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-offline)

  Disable substituters and consider all previously downloaded files up-to-date.
* [`--option`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-option) *name* *value*

  Set the Nix configuration setting *name* to *value* (overriding `nix.conf`).
* [`--refresh`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-refresh)

  Consider all previously downloaded files out-of-date.
* [`--repair`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-repair)

  During evaluation, rewrite missing or corrupted files in the Nix store. During building, rebuild missing or corrupted store paths.
* [`--version`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-version)

  Show version information.

## [Options that change environment variables](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#options-that-change-environment-variables)

* [`--ignore-env`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-ignore-env) / `-i`

  Clear the entire environment, except for those specified with `--keep-env-var`.
* [`--keep-env-var`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-keep-env-var) / `-k` *name*

  Keep the environment variable *name*, when using `--ignore-env`.
* [`--set-env-var`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-set-env-var) / `-s` *name* *value*

  Sets an environment variable *name* with *value*.
* [`--unset-env-var`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-unset-env-var) / `-u` *name*

  Unset the environment variable *name*.

## [Options that change the interpretation of](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#options-that-change-the-interpretation-of-installables) [installables](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables)

* [`--expr`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-expr) *expr*

  Interpret [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression *expr*.
* [`--file`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-env-shell#opt-file) / `-f` *file*

  Interpret [*installables*](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) as attribute paths relative to the Nix expression stored in *file*. If *file* is the character -, then a Nix expression is read from standard input. Implies `--impure`.

> **Note**
>
> See [`man nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#command-line-flags) for overriding configuration settings with command line flags.