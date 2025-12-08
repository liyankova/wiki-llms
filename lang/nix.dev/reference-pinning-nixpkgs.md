---
url: https://nix.dev/reference/pinning-nixpkgs
title: Pinning Nixpkgs — nix.dev  documentation
source_domain: nix.dev
---

# Pinning Nixpkgs — nix.dev  documentation

[Skip to main content](https://nix.dev/reference/pinning-nixpkgs#main-content)

[![](https://nix.dev/_static/img/nix.svg)
nix.dev](https://nix.dev/)

Official documentation for getting things done with Nix.

nix.dev as [PDF](https://nix.dev/nix-dev.pdf)

* [.md](https://nix.dev/_sources/reference/pinning-nixpkgs.md "Download source file")

# Pinning Nixpkgs

# Pinning Nixpkgs[#](https://nix.dev/reference/pinning-nixpkgs#pinning-nixpkgs "Link to this heading")

Specifying remote Nix expressions, such as the one provided by Nixpkgs, can be done in several ways:

* [`$NIX_PATH` environment variable](https://nix.dev/manual/nix/stable/command-ref/env-common.html#env-NIX_PATH)
* [`-I` option](https://nix.dev/manual/nix/stable/command-ref/opt-common.html#opt-I) to most commands like `nix-build`, `nix-shell`, etc.
* [`fetchurl`](https://nix.dev/manual/nix/stable/language/builtins.html#builtins-fetchurl), [`fetchTarball`](https://nix.dev/manual/nix/stable/language/builtins.html#builtins-fetchTarball), [`fetchGit`](https://nix.dev/manual/nix/stable/language/builtins.html#builtins-fetchGit) or [Nixpkgs fetchers](https://nixos.org/manual/nixpkgs/stable/#chap-pkgs-fetchers) in Nix expressions

## Possible URL values[#](https://nix.dev/reference/pinning-nixpkgs#possible-url-values "Link to this heading")

* Local file path:

  ```
  ./path/to/expression.nix
  ```

  Using `./.` means that the expression is located in a file `default.nix` in the current directory.
* Pinned to a specific commit:

  ```
  https://github.com/NixOS/nixpkgs/archive/eabc38219184cc3e04a974fe31857d8e0eac098d.tar.gz
  ```
* Using the latest channel version, meaning all tests have passed:

  ```
  http://nixos.org/channels/nixos-22.11/nixexprs.tar.xz
  ```
* Shorthand syntax for channels:

  ```
  channel:nixos-22.11
  ```
* Using the latest channel version, hosted by GitHub:

  ```
  https://github.com/NixOS/nixpkgs/archive/nixos-22.11.tar.gz
  ```
* Using the latest commit on the release branch, but not tested yet:

  ```
  https://github.com/NixOS/nixpkgs/archive/release-21.11.tar.gz
  ```

## Examples[#](https://nix.dev/reference/pinning-nixpkgs#examples "Link to this heading")

* ```
  $ nix-build -I ~/dev
  ```
* ```
  $ nix-build -I nixpkgs=http://nixos.org/channels/nixos-22.11/nixexprs.tar.xz
  ```
* ```
  $ nix-build -I nixpkgs=channel:nixos-22.11
  ```
* ```
  $ NIX_PATH=nixpkgs=http://nixos.org/channels/nixos-22.11/nixexprs.tar.xz nix-build
  ```
* ```
  $ NIX_PATH=nixpkgs=channel:nixos-22.11 nix-build
  ```
* In the Nix language:

  ```
  1let
  2  pkgs = import (fetchTarball "https://github.com/NixOS/nixpkgs/archive/nixos-22.11.tar.gz") {};
  3in pkgs.stdenv.mkDerivation { ... }
  ```

## Finding specific commits and releases[#](https://nix.dev/reference/pinning-nixpkgs#finding-specific-commits-and-releases "Link to this heading")

[status.nixos.org](https://status.nixos.org/) provides:

* Latest tested commits for each release - use when pinning to specific commits
* List of active release channels - use when tracking latest channel versions

The complete list of channels is available at [nixos.org/channels](https://nixos.org/channels).

Tip

More information on Nixpkgs and NixOS releases: [Which channel branch should I use?](https://nix.dev/concepts/faq#channel-branches)

Contents