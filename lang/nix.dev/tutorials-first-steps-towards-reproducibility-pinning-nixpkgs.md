---
url: https://nix.dev/tutorials/first-steps/towards-reproducibility-pinning-nixpkgs
title: Towards reproducibility: pinning Nixpkgs — nix.dev  documentation
source_domain: nix.dev
---

# Towards reproducibility: pinning Nixpkgs — nix.dev  documentation

[Skip to main content](https://nix.dev/tutorials/first-steps/towards-reproducibility-pinning-nixpkgs#main-content)

[![](https://nix.dev/_static/img/nix.svg)
nix.dev](https://nix.dev/)

Official documentation for getting things done with Nix.

nix.dev as [PDF](https://nix.dev/nix-dev.pdf)

* [.md](https://nix.dev/_sources/tutorials/first-steps/towards-reproducibility-pinning-nixpkgs.md "Download source file")

# Towards reproducibility: pinning Nixpkgs

# Towards reproducibility: pinning Nixpkgs[#](https://nix.dev/tutorials/first-steps/towards-reproducibility-pinning-nixpkgs#towards-reproducibility-pinning-nixpkgs "Link to this heading")

In various Nix examples, you’ll often see the following:

```
1{ pkgs ? import <nixpkgs> {} }:
2
3...
```

Note

`<nixpkgs>` points to the file system path of some revision of [Nixpkgs](https://nix.dev/reference/glossary#term-Nixpkgs).
Find more information on [lookup paths](https://nix.dev/tutorials/nix-language#lookup-path-tutorial) in [Nix language basics](https://nix.dev/tutorials/nix-language#reading-nix-language).

This is a **convenient** way to quickly demonstrate a Nix expression and get it working by importing Nix packages.

However, **the resulting Nix expression is not fully reproducible**.

## Pinning packages with URLs inside a Nix expression[#](https://nix.dev/tutorials/first-steps/towards-reproducibility-pinning-nixpkgs#pinning-packages-with-urls-inside-a-nix-expression "Link to this heading")

To create **fully reproducible** Nix expressions, we can pin an exact version of Nixpkgs.

The simplest way to do this is to fetch the required Nixpkgs version as a tarball specified via the relevant Git commit hash:

```
1{ pkgs ? import (fetchTarball "https://github.com/NixOS/nixpkgs/archive/06278c77b5d162e62df170fec307e83f1812d94b.tar.gz") {}
2}:
3
4...
```

Picking the commit can be done via [status.nixos.org](https://status.nixos.org/),
which lists all the releases and the latest commit that has passed all tests.

When choosing a commit, it is recommended to follow either

* the **latest stable NixOS** release by using a specific version, such as `nixos-21.05`, **or**
* the latest **unstable release** via `nixos-unstable`.

## Next steps[#](https://nix.dev/tutorials/first-steps/towards-reproducibility-pinning-nixpkgs#next-steps "Link to this heading")

* For more examples and details of the different ways to pin `nixpkgs`, see [Pinning Nixpkgs](https://nix.dev/reference/pinning-nixpkgs#ref-pinning-nixpkgs).
* [Automatically managing remote sources with npins](https://nix.dev/guides/recipes/dependency-management#dependency-management-npins)

Contents