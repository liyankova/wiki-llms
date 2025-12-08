---
url: https://nix.dev/concepts/faq
title: Frequently Asked Questions — nix.dev  documentation
source_domain: nix.dev
---

# Frequently Asked Questions — nix.dev  documentation

[Skip to main content](https://nix.dev/concepts/faq#main-content)

[![](https://nix.dev/_static/img/nix.svg)
nix.dev](https://nix.dev/)

Official documentation for getting things done with Nix.

nix.dev as [PDF](https://nix.dev/nix-dev.pdf)

* [.md](https://nix.dev/_sources/concepts/faq.md "Download source file")

# Frequently Asked Questions

# Frequently Asked Questions[#](https://nix.dev/concepts/faq#frequently-asked-questions "Link to this heading")

## What is the origin of the name Nix?[#](https://nix.dev/concepts/faq#what-is-the-origin-of-the-name-nix "Link to this heading")

> The name *Nix* is derived from the Dutch word *niks*, meaning *nothing*;
> build actions do not see anything that has not been explicitly declared as an input.
>
> — [Nix: A Safe and Policy-Free System for Software Deployment](https://edolstra.github.io/pubs/nspfssd-lisa2004-final.pdf), LISA XVIII, 2004

The Nix logo is inspired by [an idea for the Haskell logo](https://wiki.haskell.org/File:Sgf-logo-blue.png) and the fact that [*nix* is Latin for *snow*](https://nix-dev.science.uu.narkive.com/VDaaP1BY/nix-logo).

## What are flakes?[#](https://nix.dev/concepts/faq#what-are-flakes "Link to this heading")

See [Flakes](https://nix.dev/concepts/flakes#flakes-definition).

## Which channel branch should I use?[#](https://nix.dev/concepts/faq#which-channel-branch-should-i-use "Link to this heading")

Nixpkgs and NixOS have both stable and rolling releases.

These releases are distributed in variants called “channel branches”:
Git branches used for releases, which are also converted to Nix channels.

Tip

Consult the [`nix-channel`](https://nix.dev/manual/nix/2.22/command-ref/nix-channel) entry in the Nix Reference Manual for more information on channels, and the [Nixpkgs contributing guide](https://github.com/NixOS/nixpkgs/blob/master/CONTRIBUTING.md#branch-conventions) on the Nixpkgs branching strategy.

### Stable[#](https://nix.dev/concepts/faq#stable "Link to this heading")

Stable releases receive conservative updates to fix bugs or security vulnerabilities; otherwise package versions are not changed.
A new stable release is made every six months.

* On Linux (including NixOS and WSL), use [`nixos-*`](https://github.com/NixOS/nixpkgs/branches/all?query=nixos-).

  These branches point to commits where most Linux packages got pre-built and can be fetched from the binary cache.
  Furthermore, these commits passed the full NixOS test suite.
* On macOS/Darwin, use [`nixpkgs-*-darwin`](https://github.com/NixOS/nixpkgs/branches/all?query=nixpkgs-)

  These branches point to commits where most Darwin packages got pre-built and can be fetched from the binary cache.
* On any other platform it doesn’t matter which one of the above is used.

  Hydra doesn’t pre-build any binaries for other platforms.

All of these “channel branches” follow the corresponding [`release-*`](https://github.com/NixOS/nixpkgs/branches/all?query=release-) branch.

Example

`nixos-23.05` and `nixpkgs-23.05-darwin` are both based on `release-23.05`.

### Rolling[#](https://nix.dev/concepts/faq#rolling "Link to this heading")

Rolling releases follow [`master`](https://github.com/NixOS/nixpkgs/branches/all?query=master), the main development branch.

* On Linux (including NixOS and WSL), use [`nixos-unstable`](https://github.com/NixOS/nixpkgs/branches/all?query=nixos-unstable).
* On any other platform, use [`nixpkgs-unstable`](https://github.com/NixOS/nixpkgs/branches/all?query=nixpkgs-unstable).

[`*-small`](https://github.com/NixOS/nixpkgs/branches/all?query=-small) channel branches have passed a smaller test suite, which means they are more up-to-date with respect to their base branch, but offer fewer stability guarantees.

## Are there any impurities left in sandboxed builds?[#](https://nix.dev/concepts/faq#are-there-any-impurities-left-in-sandboxed-builds "Link to this heading")

Yes. There is:

* CPU architecture—great effort is being made to avoid compilation of native instructions in favour of hardcoded supported ones.
* System’s current time/date.
* The filesystem used for building (see also [`TMPDIR`](https://nix.dev/manual/nix/stable/command-ref/env-common.html#env-TMPDIR)).
* Linux kernel parameters, such as:

  + [IPv6 capabilities](https://github.com/NixOS/nix/issues/5615).
  + binfmt interpreters, e.g., those configured with [`boot.binfmt.emulatedSystems`](https://search.nixos.org/options?show=boot.binfmt.emulatedSystems).
* Timing behaviour of the build system—a parallel Make build may not get the correct inputs in some cases.
* Insertion of random values, e.g., from `/dev/random` or `/dev/urandom`.
* Differences between Nix versions. For instance, a new Nix version might introduce a new environment variable. A statement like `env > $out` is not promised by Nix to result in the same output, going into the future.

Contents