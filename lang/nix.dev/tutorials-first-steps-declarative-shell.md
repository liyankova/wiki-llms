---
url: https://nix.dev/tutorials/first-steps/declarative-shell
title: Declarative shell environments with shell.nix — nix.dev  documentation
source_domain: nix.dev
---

# Declarative shell environments with shell.nix — nix.dev  documentation

[Skip to main content](https://nix.dev/tutorials/first-steps/declarative-shell#main-content)

[![](https://nix.dev/_static/img/nix.svg)
nix.dev](https://nix.dev/)

Official documentation for getting things done with Nix.

nix.dev as [PDF](https://nix.dev/nix-dev.pdf)

* [.md](https://nix.dev/_sources/tutorials/first-steps/declarative-shell.md "Download source file")

# Declarative shell environments with shell.nix

# Declarative shell environments with `shell.nix`[#](https://nix.dev/tutorials/first-steps/declarative-shell#declarative-shell-environments-with-shell-nix "Link to this heading")

## Overview[#](https://nix.dev/tutorials/first-steps/declarative-shell#overview "Link to this heading")

Declarative shell environments allow you to:

* Automatically run bash commands during environment activation
* Automatically set environment variables
* Put the environment definition under version control and reproduce it on other machines

### What will you learn?[#](https://nix.dev/tutorials/first-steps/declarative-shell#what-will-you-learn "Link to this heading")

In the [Ad hoc shell environments](https://nix.dev/tutorials/first-steps/ad-hoc-shell-environments#ad-hoc-envs) tutorial, you learned how to imperatively create shell environments using `nix-shell -p`.
This is great when you want to quickly access tools without installing them permanently.
You also learned how to execute that command with a specific Nixpkgs revision using a Git commit as an argument, to recreate the same environment used previously.

In this tutorial we’ll take a look at how to create reproducible shell environments with a declarative configuration in a [Nix file](https://nix.dev/reference/glossary#term-Nix-file).
This file can be shared with anyone to recreate the same environment on a different machine.

### How long will it take?[#](https://nix.dev/tutorials/first-steps/declarative-shell#how-long-will-it-take "Link to this heading")

30 minutes

### What do you need?[#](https://nix.dev/tutorials/first-steps/declarative-shell#what-do-you-need "Link to this heading")

* Familiarity with the Unix shell
* A rudimentary understanding of the [Nix language](https://nix.dev/tutorials/nix-language#reading-nix-language)

## Entering a temporary shell[#](https://nix.dev/tutorials/first-steps/declarative-shell#entering-a-temporary-shell "Link to this heading")

Suppose we want an environment where `cowsay` and `lolcat` are available.
The simplest possible way to accomplish this is via the `nix-shell -p` command:

```
$ nix-shell -p cowsay lolcat
```

This command works, but there’s a number of drawbacks:

* You have to type out `-p cowsay lolcat` every time you enter the shell.
* It doesn’t (ergonomically) allow you any further customization of your shell environment.

A better solution is to create our shell environment from a `shell.nix` file.

## A basic `shell.nix` file[#](https://nix.dev/tutorials/first-steps/declarative-shell#a-basic-shell-nix-file "Link to this heading")

Create a file called `shell.nix` with these contents:

```
 1let
 2  nixpkgs = fetchTarball "https://github.com/NixOS/nixpkgs/tarball/nixos-24.05";
 3  pkgs = import nixpkgs { config = {}; overlays = []; };
 4in
 5
 6pkgs.mkShellNoCC {
 7  packages = with pkgs; [
 8    cowsay
 9    lolcat
10  ];
11}
```

Detailed explanation

We use a version of [Nixpkgs pinned to a release branch](https://nix.dev/reference/pinning-nixpkgs#ref-pinning-nixpkgs).
If you followed the [Ad hoc shell environments](https://nix.dev/tutorials/first-steps/ad-hoc-shell-environments#ad-hoc-envs) tutorial and don’t want to download all dependencies again, specify the exact same revision as in the section [Towards reproducibility](https://nix.dev/tutorials/first-steps/ad-hoc-shell-environments#towards-reproducibility):

```
1let
2  nixpkgs = fetchTarball "https://github.com/NixOS/nixpkgs/tarball/2a601aafdc5605a5133a2ca506a34a3a73377247";
3  pkgs = import nixpkgs { config = {}; overlays = []; };
4in
```

We explicitly set `config` and `overlays` to avoid them being inadvertently overridden by [global configuration](https://nixos.org/manual/nixpkgs/stable/#chap-packageconfig).

`mkShellNoCC` is a function that takes as an argument an attribute set.
Here we give it an attribute `packages` with a list containing two items from the `pkgs` attribute set.

Side note on `mkShell`

`nix-shell` and `mkShell` were originally conceived as a way to construct a shell environment containing the [tools needed to debug package builds](https://nixos.org/manual/nixpkgs/stable/#sec-tools-of-stdenv), such as Make or GCC.
Only later did it become widely used as a general way to make temporary environments for other purposes.
`mkShellNoCC` is a function that produces such an environment, but without a compiler toolchain.

You may encounter examples of `mkShell` or `mkShellNoCC` that add packages to the `buildInputs` or `nativeBuildInputs` attributes instead.
`mkShellNoCC` is a [wrapper around `mkDerivation`](https://nixos.org/manual/nixpkgs/stable/#sec-pkgs-mkShell), so it takes the same arguments as `mkDerivation`, such as `buildInputs` or `nativeBuildInputs`.
The `packages` attribute argument to `mkShellNoCC` is simply an alias for `nativeBuildInputs`.

Enter the environment by running `nix-shell` in the same directory as `shell.nix`:

Note

The first invocation of `nix-shell` on this file may take a while to download all dependencies.

```
$ nix-shell
[nix-shell]$ cowsay hello | lolcat
```

`nix-shell` by default looks for a file called `shell.nix` in the current directory and builds a shell environment from the Nix expression in this file.
Packages defined in the `packages` attribute will be available in `$PATH`.

## Environment variables[#](https://nix.dev/tutorials/first-steps/declarative-shell#environment-variables "Link to this heading")

You may want to automatically export certain environment variables when you enter a shell environment.

Set `GREETING` so it can be used in the shell environment:

```
 let
   nixpkgs = fetchTarball "https://github.com/NixOS/nixpkgs/tarball/nixos-24.05";
   pkgs = import nixpkgs { config = {}; overlays = []; };
 in

 pkgs.mkShellNoCC {
   packages = with pkgs; [
     cowsay
     lolcat
   ];

+  GREETING = "Hello, Nix!";
 }
```

Any attribute name passed to `mkShellNoCC` that is not reserved otherwise and has a value which can be coerced to a string will end up as an environment variable.

Try it out!
Exit the shell by typing `exit` or pressing `Ctrl`+`D`, then start it again with `nix-shell`.

```
[nix-shell]$ echo $GREETING
```

Warning

Some variables are protected from being set as described above.

For example, the shell prompt format for most shells is set by the `PS1` environment variable, but `nix-shell` already sets this by default, and will ignore a `PS1` attribute set in the argument.

If you need to override these protected environment variables, use the `shellHook` attribute as described in the next section.

## Startup commands[#](https://nix.dev/tutorials/first-steps/declarative-shell#startup-commands "Link to this heading")

You may want to run some commands before entering the shell environment.
These commands can be placed in the `shellHook` attribute provided to `mkShellNoCC`.

Set `shellHook` to output a colorful greeting:

```
 let
   nixpkgs = fetchTarball "https://github.com/NixOS/nixpkgs/tarball/nixos-24.05";
   pkgs = import nixpkgs { config = {}; overlays = []; };
 in

 pkgs.mkShellNoCC {
   packages = with pkgs; [
     cowsay
     lolcat
   ];

   GREETING = "Hello, Nix!";
+
+  shellHook = ''
+    echo $GREETING | cowsay | lolcat
+  '';
 }
```

Try it again!
Exit the shell by typing `exit` or pressing `Ctrl`+`D`, then start it again with `nix-shell` to observe the effect.

## References[#](https://nix.dev/tutorials/first-steps/declarative-shell#references "Link to this heading")

* [`mkShell` documentation](https://nixos.org/manual/nixpkgs/stable/#sec-pkgs-mkShell)
* Nixpkgs [shell functions and utilities](https://nixos.org/manual/nixpkgs/stable/#ssec-stdenv-functions) documentation
* [`nix-shell` documentation](https://nix.dev/manual/nix/stable/command-ref/nix-shell)

## Next steps[#](https://nix.dev/tutorials/first-steps/declarative-shell#next-steps "Link to this heading")

* [Nix language basics](https://nix.dev/tutorials/nix-language#reading-nix-language)
* [Automatic environment activation with direnv](https://nix.dev/guides/recipes/direnv#automatic-direnv)
* [Dependencies in the development shell](https://nix.dev/guides/recipes/sharing-dependencies)
* [Automatically managing remote sources with npins](https://nix.dev/guides/recipes/dependency-management)

Contents