---
url: https://nix.dev/install-nix
title: Install Nix — nix.dev  documentation
source_domain: nix.dev
---

# Install Nix — nix.dev  documentation

[Skip to main content](https://nix.dev/install-nix#main-content)

[![](https://nix.dev/_static/img/nix.svg)
nix.dev](https://nix.dev/)

Official documentation for getting things done with Nix.

nix.dev as [PDF](https://nix.dev/nix-dev.pdf)

* [.md](https://nix.dev/_sources/install-nix.md "Download source file")

# Install Nix

# Install Nix[#](https://nix.dev/install-nix#install-nix "Link to this heading")

Requirements:

* Prior to installation, you might first need to install `xz-utils` or similar for decompressing the Nix binary tarball (`.tar.xz`) that will be downloaded via the scripts below.

Linux

Install Nix via the recommended [multi-user installation](https://nix.dev/manual/nix/stable/installation/multi-user.html):

```
$ curl -L https://nixos.org/nix/install | sh -s -- --daemon
```

On Arch Linux, you can alternatively [install Nix through `pacman`](https://wiki.archlinux.org/title/Nix#Installation).

macOS

Install Nix via the recommended [multi-user installation](https://nix.dev/manual/nix/stable/installation/multi-user.html):

```
$ curl -L https://nixos.org/nix/install | sh
```

Important

**Updating to macOS 15 Sequoia**

If you recently updated to macOS 15 Sequoia and are getting the error

```
error: the user '_nixbld1' in the group 'nixbld' does not exist
```

when running Nix commands, refer to GitHub issue [NixOS/nix#10892](https://github.com/NixOS/nix/issues/10892) for instructions to fix your installation without reinstalling.

Windows (WSL2)

Install Nix via the recommended [single-user installation](https://nix.dev/manual/nix/stable/installation/single-user.html):

```
$ curl -L https://nixos.org/nix/install | sh -s -- --no-daemon
```

However, if you have [systemd support](https://learn.microsoft.com/en-us/windows/wsl/wsl-config#systemd-support) enabled, install Nix via the recommended [multi-user installation](https://nix.dev/manual/nix/stable/installation/multi-user.html):

```
$ curl -L https://nixos.org/nix/install | sh -s -- --daemon
```

Docker

Start a Docker shell with Nix:

```
$ docker run -it nixos/nix
```

Or start a Docker shell with Nix exposing a `workdir` directory:

```
$ mkdir workdir
$ docker run -it -v $(pwd)/workdir:/workdir nixos/nix
```

The `workdir` example from above can also be used to start hacking on Nixpkgs:

```
$ git clone git@github.com:NixOS/nixpkgs
$ docker run -it -v $(pwd)/nixpkgs:/nixpkgs nixos/nix
bash-5.1# nix-build -I nixpkgs=/nixpkgs -A hello
bash-5.1# find ./result # this symlink points to the build package
```

## Verify installation[#](https://nix.dev/install-nix#verify-installation "Link to this heading")

Check the installation by opening **a new terminal** and typing:

```
$ nix --version
nix (Nix) 2.11.0
```

Contents