---
url: https://nix.dev/tutorials/module-system/
title: Module system — nix.dev  documentation
source_domain: nix.dev
---

# Module system — nix.dev  documentation

[Skip to main content](https://nix.dev/tutorials/module-system/#main-content)

[![](https://nix.dev/_static/img/nix.svg)
nix.dev](https://nix.dev/)

Official documentation for getting things done with Nix.

nix.dev as [PDF](https://nix.dev/nix-dev.pdf)

* [.md](https://nix.dev/_sources/tutorials/module-system/index.md "Download source file")

# Module system

# Module system[#](https://nix.dev/tutorials/module-system/#module-system "Link to this heading")

Much of the power in Nixpkgs and NixOS comes from the module system.

The module system is a Nix language library that enables you to

* Declare one attribute set using many separate Nix expressions.
* Imposes type constraints on values in that attribute set.
* Define values for the same attribute in different Nix expressions and merge these values automatically according to their type.

These Nix expressions are called modules and must have a particular structure.

In this tutorial series you’ll learn

* What a module is and how to create one.
* What options are and how to declare them.
* How to express dependencies between modules.

## What do you need?[#](https://nix.dev/tutorials/module-system/#what-do-you-need "Link to this heading")

* Familiarity with data types and general programming concepts
* A [Nix installation](https://nix.dev/install-nix#install-nix) to run the examples
* Intermediate proficiency in reading and writing the [Nix language](https://nix.dev/tutorials/nix-language#reading-nix-language)

## How long will it take?[#](https://nix.dev/tutorials/module-system/#how-long-will-it-take "Link to this heading")

This is a very long tutorial.
Prepare for at least 3 hours of work.

Lessons

* [1. A basic module](https://nix.dev/tutorials/module-system/a-basic-module/)
* [2. Module system deep dive](https://nix.dev/tutorials/module-system/deep-dive)

Contents