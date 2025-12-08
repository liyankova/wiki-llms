---
url: https://nix.dev/guides/recipes/sharing-dependencies
title: Dependencies in the development shell — nix.dev  documentation
source_domain: nix.dev
---

# Dependencies in the development shell — nix.dev  documentation

[Skip to main content](https://nix.dev/guides/recipes/sharing-dependencies#main-content)

[![](https://nix.dev/_static/img/nix.svg)
nix.dev](https://nix.dev/)

Official documentation for getting things done with Nix.

nix.dev as [PDF](https://nix.dev/nix-dev.pdf)

* [.md](https://nix.dev/_sources/guides/recipes/sharing-dependencies.md "Download source file")

# Dependencies in the development shell

# Dependencies in the development shell[#](https://nix.dev/guides/recipes/sharing-dependencies#dependencies-in-the-development-shell "Link to this heading")

When [packaging software in `default.nix`](https://nix.dev/tutorials/packaging-existing-software#packaging-tutorial), you’ll want a [development environment in `shell.nix`](https://nix.dev/tutorials/first-steps/declarative-shell#declarative-reproducible-envs) to enter conveniently with `nix-shell` or [automatically with `direnv`](https://nix.dev/guides/recipes/direnv).

How to share the package’s dependencies in `default.nix` with the development environment in `shell.nix`?

## Summary[#](https://nix.dev/guides/recipes/sharing-dependencies#summary "Link to this heading")

Use the [`inputsFrom` attribute to `pkgs.mkShellNoCC`](https://nixos.org/manual/nixpkgs/stable/#sec-pkgs-mkShell-attributes):

```
 1# default.nix
 2let
 3  pkgs = import <nixpkgs> {};
 4  build = pkgs.callPackage ./build.nix {};
 5in
 6{
 7  inherit build;
 8  shell = pkgs.mkShellNoCC {
 9    inputsFrom = [ build ];
10  };
11}
```

Import the `shell` attribute in `shell.nix`:

```
1# shell.nix
2(import ./.).shell
```

## Complete example[#](https://nix.dev/guides/recipes/sharing-dependencies#complete-example "Link to this heading")

Assume your build is defined in `build.nix`:

```
1# build.nix
2{ cowsay, runCommand }:
3runCommand "cowsay-output" { buildInputs = [ cowsay ]; } ''
4  cowsay Hello, Nix! > $out
5''
```

In this example, `cowsay` is declared as a build-time dependency using `buildInputs`.

Further assume your project is defined in `default.nix`:

```
1# default.nix
2let
3  nixpkgs = fetchTarball "https://github.com/NixOS/nixpkgs/tarball/nixos-23.11";
4  pkgs = import nixpkgs { config = {}; overlays = []; };
5in
6{
7  build = pkgs.callPackage ./build.nix {};
8}
```

Add an attribute to `default.nix` specifying an environment:

```
 let
   nixpkgs = fetchTarball "https://github.com/NixOS/nixpkgs/tarball/nixos-23.11";
   pkgs = import nixpkgs { config = {}; overlays = []; };
 in
 {
   build = pkgs.callPackage ./build.nix {};
+  shell = pkgs.mkShellNoCC {
+  };
 }
```

Move the `build` attribute into the `let` binding to be able to re-use it.
Then take the package’s dependencies into the environment with [`inputsFrom`](https://nixos.org/manual/nixpkgs/stable/#sec-pkgs-mkShell-attributes):

```
 let
   nixpkgs = fetchTarball "https://github.com/NixOS/nixpkgs/tarball/nixos-23.11";
   pkgs = import nixpkgs { config = {}; overlays = []; };
+  build = pkgs.callPackage ./build.nix {};
 in
 {
-  build = pkgs.callPackage ./build.nix {};
+  inherit build;
   shell = pkgs.mkShellNoCC {
+    inputsFrom = [ build ];
   };
 }
```

Finally, import the `shell` attribute in `shell.nix`:

```
1# shell.nix
2(import ./.).shell
```

Check the development environment, it contains the build-time dependency `cowsay`:

```
$ nix-shell --pure
[nix-shell]$ cowsay shell.nix
```

## Next steps[#](https://nix.dev/guides/recipes/sharing-dependencies#next-steps "Link to this heading")

* [Towards reproducibility: pinning Nixpkgs](https://nix.dev/tutorials/first-steps/towards-reproducibility-pinning-nixpkgs#pinning-nixpkgs)
* [Automatic environment activation with direnv](https://nix.dev/guides/recipes/direnv)
* [Setting up a Python development environment](https://nix.dev/guides/recipes/python-environment#python-dev-environment)
* [Packaging existing software with Nix](https://nix.dev/tutorials/packaging-existing-software#packaging-tutorial)

Contents