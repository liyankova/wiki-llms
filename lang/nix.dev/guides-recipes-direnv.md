---
url: https://nix.dev/guides/recipes/direnv
title: Automatic environment activation with direnv — nix.dev  documentation
source_domain: nix.dev
---

# Automatic environment activation with direnv — nix.dev  documentation

[Skip to main content](https://nix.dev/guides/recipes/direnv#main-content)

[![](https://nix.dev/_static/img/nix.svg)
nix.dev](https://nix.dev/)

Official documentation for getting things done with Nix.

nix.dev as [PDF](https://nix.dev/nix-dev.pdf)

* [.md](https://nix.dev/_sources/guides/recipes/direnv.md "Download source file")

# Automatic environment activation with direnv

# Automatic environment activation with `direnv`[#](https://nix.dev/guides/recipes/direnv#automatic-environment-activation-with-direnv "Link to this heading")

Instead of manually activating the environment for each project, you can reload a [declarative shell](https://nix.dev/tutorials/first-steps/declarative-shell#declarative-reproducible-envs) every time you enter the project’s directory or change the `shell.nix` inside it.

1. [Make nix-direnv available](https://github.com/nix-community/nix-direnv)
2. [Hook it into your shell](https://direnv.net/docs/hook.html)

For example, write a `shell.nix` with the following contents:

```
 1let
 2  nixpkgs = fetchTarball "https://github.com/NixOS/nixpkgs/tarball/nixos-23.11";
 3  pkgs = import nixpkgs { config = {}; overlays = []; };
 4in
 5
 6pkgs.mkShellNoCC {
 7  packages = with pkgs; [
 8    hello
 9  ];
10}
```

From the top-level directory of your project, run:

```
$ echo "use nix" > .envrc && direnv allow
```

The next time you launch your terminal and enter the top-level directory of your project, `direnv` will automatically launch the shell defined in `shell.nix`.

```
$ cd myproject
$ which hello
/nix/store/1gxz5nfzfnhyxjdyzi04r86sh61y4i00-hello-2.12.1/bin/hello
```

`direnv` will also check for changes to the `shell.nix` file.

Make the following addition:

```
 let
   nixpkgs = fetchTarball "https://github.com/NixOS/nixpkgs/tarball/nixos-23.11";
   pkgs = import nixpkgs { config = {}; overlays = []; };
 in

 pkgs.mkShellNoCC {
   packages = with pkgs; [
     hello
   ];
+
+  shellHook = ''
+    hello
+  '';
 }
```

The running environment should reload itself after the first interaction (run any command or press `Enter`).

```
Hello, world!
```