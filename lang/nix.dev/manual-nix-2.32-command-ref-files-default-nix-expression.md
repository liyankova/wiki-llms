---
url: https://nix.dev/manual/nix/2.32/command-ref/files/default-nix-expression
title: Default Nix expression - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Default Nix expression - Nix 2.32.2 Reference Manual

## [Default Nix expression](https://nix.dev/manual/nix/2.32/command-ref/files/default-nix-expression#default-nix-expression)

The source for the [Nix expressions](https://nix.dev/manual/nix/2.32/glossary#gloss-nix-expression) used by [`nix-env`](https://nix.dev/manual/nix/2.32/command-ref/nix-env) by default:

* `~/.nix-defexpr`
* `$XDG_STATE_HOME/nix/defexpr` if [`use-xdg-base-directories`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-xdg-base-directories) is set to `true`.

It is loaded as follows:

* If the default expression is a file, it is loaded as a Nix expression.
* If the default expression is a directory containing a `default.nix` file, that `default.nix` file is loaded as a Nix expression.
* If the default expression is a directory without a `default.nix` file, then its contents (both files and subdirectories) are loaded as Nix expressions.
  The expressions are combined into a single attribute set, each expression under an attribute with the same name as the original file or subdirectory.
  Subdirectories without a `default.nix` file are traversed recursively in search of more Nix expressions, but the names of these intermediate directories are not added to the attribute paths of the default Nix expression.

Then, the resulting expression is interpreted like this:

* If the expression is an attribute set, it is used as the default Nix expression.
* If the expression is a function, an empty set is passed as argument and the return value is used as the default Nix expression.

> **Example**
>
> If the default expression contains two files, `foo.nix` and `bar.nix`, then the default Nix expression will be equivalent to
>
> ```
> {
>   foo = import ~/.nix-defexpr/foo.nix;
>   bar = import ~/.nix-defexpr/bar.nix;
> }
> ```

The file [`manifest.nix`](https://nix.dev/manual/nix/2.32/command-ref/files/manifest.nix) is always ignored.

The command [`nix-channel`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel) places a symlink to the current user's [channels](https://nix.dev/manual/nix/2.32/command-ref/files/channels) in this directory, the [user channel link](https://nix.dev/manual/nix/2.32/command-ref/files/default-nix-expression#user-channel-link).
This makes all subscribed channels available as attributes in the default expression.

## [User channel link](https://nix.dev/manual/nix/2.32/command-ref/files/default-nix-expression#user-channel-link)

A symlink that ensures that [`nix-env`](https://nix.dev/manual/nix/2.32/command-ref/nix-env) can find the current user's [channels](https://nix.dev/manual/nix/2.32/command-ref/files/channels):

* `~/.nix-defexpr/channels`
* `$XDG_STATE_HOME/defexpr/channels` if [`use-xdg-base-directories`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-xdg-base-directories) is set to `true`.

This symlink points to:

* `$XDG_STATE_HOME/profiles/channels` for regular users
* `$NIX_STATE_DIR/profiles/per-user/root/channels` for `root`

In a multi-user installation, you may also have `~/.nix-defexpr/channels_root`, which links to the channels of the root user.