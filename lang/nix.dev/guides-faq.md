---
url: https://nix.dev/guides/faq
title: Frequently Asked Questions — nix.dev  documentation
source_domain: nix.dev
---

# Frequently Asked Questions — nix.dev  documentation

[Skip to main content](https://nix.dev/guides/faq#main-content)

[![](https://nix.dev/_static/img/nix.svg)
nix.dev](https://nix.dev/)

Official documentation for getting things done with Nix.

nix.dev as [PDF](https://nix.dev/nix-dev.pdf)

* [.md](https://nix.dev/_sources/guides/faq.md "Download source file")

# Frequently Asked Questions

# Frequently Asked Questions[#](https://nix.dev/guides/faq#frequently-asked-questions "Link to this heading")

## Nix[#](https://nix.dev/guides/faq#nix "Link to this heading")

### How to format Nix language code automatically?[#](https://nix.dev/guides/faq#how-to-format-nix-language-code-automatically "Link to this heading")

[`nixfmt`](https://github.com/NixOS/nixfmt) is the official formatter for [Nix language](https://nix.dev/reference/glossary#term-Nix-language) code.
Please refer to its source repository for installation instructions.

`nixfmt` is [used to format all code](https://github.com/NixOS/nixpkgs/blob/master/ci/default.nix) in [Nixpkgs](https://nix.dev/reference/glossary#term-Nixpkgs).

### How to convert between paths and strings in the Nix language?[#](https://nix.dev/guides/faq#how-to-convert-between-paths-and-strings-in-the-nix-language "Link to this heading")

See the Nix reference manual on [string interpolation](https://nix.dev/manual/nix/2.19/language/string-interpolation) and [operators on paths and strings](https://nix.dev/manual/nix/2.19/language/operators#string-concatenation).

### How to build reverse dependencies of a package?[#](https://nix.dev/guides/faq#how-to-build-reverse-dependencies-of-a-package "Link to this heading")

```
$ nix-shell -p nixpkgs-review --run "nixpkgs-review wip"
```

### How can I manage dotfiles in $HOME with Nix?[#](https://nix.dev/guides/faq#how-can-i-manage-dotfiles-in-home-with-nix "Link to this heading")

See [nix-community/home-manager](https://github.com/nix-community/home-manager)

### What’s the recommended process for building custom packages?[#](https://nix.dev/guides/faq#what-s-the-recommended-process-for-building-custom-packages "Link to this heading")

Please read [Packaging existing software with Nix](https://nix.dev/tutorials/packaging-existing-software#packaging-tutorial).

### How to use a clone of the Nixpkgs repository to update or write new packages?[#](https://nix.dev/guides/faq#how-to-use-a-clone-of-the-nixpkgs-repository-to-update-or-write-new-packages "Link to this heading")

Please read [Packaging existing software with Nix](https://nix.dev/tutorials/packaging-existing-software#packaging-tutorial) and the [Nixpkgs contributing guide](https://github.com/NixOS/nixpkgs/blob/master/CONTRIBUTING.md).

## NixOS[#](https://nix.dev/guides/faq#nixos "Link to this heading")

### How to run non-nix executables?[#](https://nix.dev/guides/faq#how-to-run-non-nix-executables "Link to this heading")

NixOS cannot run dynamically linked executables intended for generic Linux environments out of the box.
This is because, by design, it does not have a global library path, nor does it follow the [Filesystem Hierarchy Standard](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html) (FHS).

There are a few ways to resolve this mismatch in environment expectations:

* Use the version packaged in Nixpkgs, if there is one.
  You can search available packages at <https://search.nixos.org/packages>.
* Write a Nix expression for the program to package it in your own configuration.

  There are multiple approaches to this:

  + Build from source.

    Many open-source programs are highly flexible at compile time in terms of where their files go.
    For an introduction to this, see [Packaging existing software with Nix](https://nix.dev/tutorials/packaging-existing-software#packaging-tutorial).
  + Modify the program’s [ELF header](https://en.wikipedia.org/wiki/Executable_and_Linkable_Format) to include paths to libraries using [`autoPatchelfHook`](https://nixos.org/manual/nixpkgs/stable/#setup-hook-autopatchelfhook).

    Do this if building from source isn’t feasible.
  + Wrap the program to run in an FHS-like environment using [`buildFHSEnv`](https://nixos.org/manual/nixpkgs/stable/#sec-fhs-environments).

    This is a last resort, but sometimes necessary, for example if the program downloads and runs other executables.
* Create a library path that only applies to unpackaged programs by using [`nix-ld`](https://github.com/Mic92/nix-ld).
  Add this to your `configuration.nix`:

  ```
  1  programs.nix-ld.enable = true;
  2  programs.nix-ld.libraries = with pkgs; [
  3    # Add any missing dynamic libraries for unpackaged programs
  4    # here, NOT in environment.systemPackages
  5  ];
  ```

  Then run `nixos-rebuild switch`, and log out and back in again to propagate the new environment variables.
  (This is only necessary when enabling `nix-ld`; changes in included libraries take effect immediately on rebuild.)

  Note

  `nix-ld` does not work for 32-bit executables on `x86_64` machines.
* Run your program in the FHS-like environment made for the Steam package using [`steam-run`](https://nixos.org/manual/nixpkgs/stable/#sec-steam-run):

  ```
  $ nix-shell -p steam-run --run "steam-run <command>"
  ```

### How to build my own ISO?[#](https://nix.dev/guides/faq#how-to-build-my-own-iso "Link to this heading")

See <http://nixos.org/nixos/manual/index.html#sec-building-image>

### How do I connect to any of the machines in NixOS tests?[#](https://nix.dev/guides/faq#how-do-i-connect-to-any-of-the-machines-in-nixos-tests "Link to this heading")

Apply the following patch:

```
diff --git a/nixos/lib/test-driver/test-driver.pl b/nixos/lib/test-driver/test-driver.pl
index 8ad0d67..838fbdd 100644
--- a/nixos/lib/test-driver/test-driver.pl
+++ b/nixos/lib/test-driver/test-driver.pl
@@ -34,7 +34,7 @@ foreach my $vlan (split / /, $ENV{VLANS} || "") {
     if ($pid == 0) {
         dup2(fileno($pty->slave), 0);
         dup2(fileno($stdoutW), 1);
-        exec "vde_switch -s $socket" or _exit(1);
+        exec "vde_switch -tap tap0 -s $socket" or _exit(1);
     }
     close $stdoutW;
     print $pty "version\n";
```

And then the vde\_switch network should be accessible locally.

### How to bootstrap NixOS inside an existing Linux installation?[#](https://nix.dev/guides/faq#how-to-bootstrap-nixos-inside-an-existing-linux-installation "Link to this heading")

There are a couple of tools:

* [nix-community/nixos-anywhere](https://github.com/nix-community/nixos-anywhere)
* [jeaye/nixos-in-place](https://github.com/jeaye/nixos-in-place)
* [elitak/nixos-infect](https://github.com/elitak/nixos-infect)
* [cleverca22/nix-tests](https://github.com/cleverca22/nix-tests/tree/master/kexec)

Contents