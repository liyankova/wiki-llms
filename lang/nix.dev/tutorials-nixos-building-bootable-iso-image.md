---
url: https://nix.dev/tutorials/nixos/building-bootable-iso-image
title: Building a bootable ISO image — nix.dev  documentation
source_domain: nix.dev
---

# Building a bootable ISO image — nix.dev  documentation

[Skip to main content](https://nix.dev/tutorials/nixos/building-bootable-iso-image#main-content)

[![](https://nix.dev/_static/img/nix.svg)
nix.dev](https://nix.dev/)

Official documentation for getting things done with Nix.

nix.dev as [PDF](https://nix.dev/nix-dev.pdf)

* [.md](https://nix.dev/_sources/tutorials/nixos/building-bootable-iso-image.md "Download source file")

# Building a bootable ISO image

# Building a bootable ISO image[#](https://nix.dev/tutorials/nixos/building-bootable-iso-image#building-a-bootable-iso-image "Link to this heading")

Note

If you need to build images for a different platform, see [Cross compiling](https://github.com/nix-community/nixos-generators#user-content-cross-compiling).

You may find that an official installation image lacks some hardware support.

The solution is to create `myimage.nix` to point to the latest kernel using the minimal installation ISO:

```
 1{ pkgs, modulesPath, lib, ... }: {
 2  imports = [
 3    "${modulesPath}/installer/cd-dvd/installation-cd-minimal.nix"
 4  ];
 5
 6  # use the latest Linux kernel
 7  boot.kernelPackages = pkgs.linuxPackages_latest;
 8
 9  # Needed for https://github.com/NixOS/nixpkgs/issues/58959
10  boot.supportedFilesystems = lib.mkForce [ "btrfs" "reiserfs" "vfat" "f2fs" "xfs" "ntfs" "cifs" ];
11}
```

Generate an ISO with the above configuration:

```
$ NIX_PATH=nixpkgs=https://github.com/NixOS/nixpkgs/archive/74e2faf5965a12e8fa5cff799b1b19c6cd26b0e3.tar.gz nix-shell -p nixos-generators --run "nixos-generate --format iso --configuration ./myimage.nix -o result"
```

Copy the new image to your USB stick by replacing `sdX` with the name of your device:

```
$ dd if=result/iso/*.iso of=/dev/sdX status=progress
$ sync
```

## Next steps[#](https://nix.dev/tutorials/nixos/building-bootable-iso-image#next-steps "Link to this heading")

* Take a look at this [list of formats that the generators support](https://github.com/nix-community/nixos-generators#user-content-supported-formats) to find your cloud provider or virtualization technology.
* Take a look at the [alternative guide to create a NixOS live CD](https://wiki.nixos.org/wiki/Creating_a_NixOS_live_CD)

Contents