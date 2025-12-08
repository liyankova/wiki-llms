---
url: https://nix.dev/tutorials/nixos/provisioning-remote-machines
title: Provisioning remote machines via SSH — nix.dev  documentation
source_domain: nix.dev
---

# Provisioning remote machines via SSH — nix.dev  documentation

[Skip to main content](https://nix.dev/tutorials/nixos/provisioning-remote-machines#main-content)

[![](https://nix.dev/_static/img/nix.svg)
nix.dev](https://nix.dev/)

Official documentation for getting things done with Nix.

nix.dev as [PDF](https://nix.dev/nix-dev.pdf)

* [.md](https://nix.dev/_sources/tutorials/nixos/provisioning-remote-machines.md "Download source file")

# Provisioning remote machines via SSH

# Provisioning remote machines via SSH[#](https://nix.dev/tutorials/nixos/provisioning-remote-machines#provisioning-remote-machines-via-ssh "Link to this heading")

It is possible to replace any Linux installation with a NixOS configuration on running systems using [`nixos-anywhere`](https://nix-community.github.io/nixos-anywhere/) and [`disko`](https://github.com/nix-community/disko).

## Introduction[#](https://nix.dev/tutorials/nixos/provisioning-remote-machines#introduction "Link to this heading")

In this tutorial, you will deploy a NixOS configuration to a running computer.

### What will you learn?[#](https://nix.dev/tutorials/nixos/provisioning-remote-machines#what-will-you-learn "Link to this heading")

You’ll learn how to

* Specify a minimal NixOS configuration with a declarative disk layout and SSH access
* Check that a configuration is valid
* Deploy and update a NixOS configuration on a remote machine

### What do you need?[#](https://nix.dev/tutorials/nixos/provisioning-remote-machines#what-do-you-need "Link to this heading")

* Familiarity with the [Nix language](https://nix.dev/tutorials/nix-language#reading-nix-language)
* Familiarity with the [Module system](https://nix.dev/tutorials/module-system/#module-system-tutorial)

For a successful unattended installation, ensure for the *target machine* that:

* It is a QEMU virtual machine running Linux

  + With [`kexec`](https://en.wikipedia.org/wiki/Kexec) support
  + On the `x86-64` or `aarch64` instruction set architecture (ISA)
  + With at least 1 GB of RAM

  This may also be a live system booted from USB, such as the [NixOS installer](https://nixos.org/download/#download-nixos-accordion).
* The IP address is configured automatically with DHCP
* You can login via SSH

  + With public key authentication (preferred), or password
  + As user `root` or another user with `sudo` permissions

The *local machine* only needs a working [Nix installation](https://nix.dev/install-nix#install-nix).

We call the *target machine* `target-machine` in this tutorial.
Replace it with the actual hostname or IP address.

## Prepare the environment[#](https://nix.dev/tutorials/nixos/provisioning-remote-machines#prepare-the-environment "Link to this heading")

Create a new project directory and enter it with your shell:

```
mkdir remote
cd remote
```

[Specify dependencies](https://nix.dev/guides/recipes/dependency-management#dependency-management-npins) on `nixpkgs`, `disko`, and `nixos-anywhere`:

```
$ nix-shell -p npins
[nix-shell:remote]$ npins init
[nix-shell:remote]$ npins add github nix-community disko
[nix-shell:remote]$ npins add github nix-community nixos-anywhere
```

Create a new file `shell.nix` which provides all needed tooling using the pinned dependencies:

```
let
  sources = import ./npins;
  pkgs = import sources.nixpkgs {};
in

pkgs.mkShell {
  nativeBuildInputs = with pkgs; [
    npins
    nixos-anywhere
    nixos-rebuild
  ];
  shellHook = ''
    export NIX_PATH="nixpkgs=${sources.nixpkgs}:nixos-config=$PWD/configuration.nix"
  '';
}
```

Now exit the temporary environment and enter the newly specified one:

```
[nix-shell:remote]$ exit
$ nix-shell
```

This shell environment is ready to use well-defined versions of Nixpkgs with `nixos-anywhere` and `nixos-rebuild`.

Important

Run all following commands in this environment.

## Create a NixOS configuration[#](https://nix.dev/tutorials/nixos/provisioning-remote-machines#create-a-nixos-configuration "Link to this heading")

The new NixOS configuration will consist of the general system configuration and a disk layout specification.

The disk layout in this example describes a single disk with a [master boot record](https://en.wikipedia.org/wiki/Master_boot_record) (MBR) and [EFI system partition](https://en.wikipedia.org/wiki/EFI_system_partition) (ESP) partition, and a root file system that takes all remaining available space.
It will work on both EFI and BIOS systems.

Create a new file `single-disk-layout.nix` with the disk layout specification:

```
 1{ ... }:
 2
 3{
 4  disko.devices.disk.main = {
 5    type = "disk";
 6    content = {
 7      type = "gpt";
 8      partitions = {
 9        MBR = {
10          priority = 0;
11          size = "1M";
12          type = "EF02";
13        };
14        ESP = {
15          priority = 1;
16          size = "500M";
17          type = "EF00";
18          content = {
19            type = "filesystem";
20            format = "vfat";
21            mountpoint = "/boot";
22          };
23        };
24        root = {
25          priority = 2;
26          size = "100%";
27          content = {
28            type = "filesystem";
29            format = "ext4";
30            mountpoint = "/";
31          };
32        };
33      };
34    };
35  };
36}
```

Create the file `configuration.nix`, which imports the disk layout definition and specifies which disk to format:

Tip

If you don’t know the target disk’s device identifier, list all devices on the *target machine* with `lsblk`:

```
$ ssh target-machine lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
sda      8:0    0   256G  0 disk
├─sda1   8:1    0 248.5G  0 part /nix/store
│                                /
└─sda2   8:2    0   7.5G  0 part [SWAP]
sr0     11:0    1  1024M  0 rom
```

In this example, the disk name is `sda`.
The block device path is then `/dev/sda`.
Note that value for later.

```
 1{ modulesPath, ... }:
 2
 3let
 4  diskDevice = "/dev/sda";
 5  sources = import ./npins;
 6in
 7{
 8  imports = [
 9    (modulesPath + "/profiles/qemu-guest.nix")
10    (sources.disko + "/module.nix")
11    ./single-disk-layout.nix
12  ];
13
14  disko.devices.disk.main.device = diskDevice;
15
16  boot.loader.grub = {
17    devices = [ diskDevice ];
18    efiSupport = true;
19    efiInstallAsRemovable = true;
20  };
21
22  services.openssh.enable = true;
23
24  users.users.root.openssh.authorizedKeys.keys = [
25    "<your SSH key here>"
26  ];
27
28  system.stateVersion = "24.11";
29}
```

Important

Replace `/dev/sda` with your disk block device path.

Replace the `<your SSH key here>` string with the SSH public key that you want to use for future logins as user `root`.

Detailed explanation

The `diskDevice` variable in the `let` block defines the path of the disk block device:

```
3let
4  diskDevice = "/dev/sda";
5  sources = import ./npins;
6in
```

It is used to set the target for the partitioning and formatting as described in the disk layout specification.
It is also used in the boot loader configuration to make it bootable on both legacy BIOS as well as UEFI systems:

```
14  disko.devices.disk.main.device = diskDevice;
15
16  boot.loader.grub = {
17    devices = [ diskDevice ];
18    efiSupport = true;
19    efiInstallAsRemovable = true;
20  };
```

The `qemu-guest.nix` module makes this system compatible for running inside a QEMU virtual machine:

```
 8  imports = [
 9    (modulesPath + "/profiles/qemu-guest.nix")
10    (sources.disko + "/module.nix")
11    ./single-disk-layout.nix
12  ];
```

From a disk layout specification, the `disko` library generates a partitioning script and the portion of the NixOS configuration that mounts the partitions accordingly at boot time.
The first line imports the library, the second line applies the disk layout:

```
 8  imports = [
 9    (modulesPath + "/profiles/qemu-guest.nix")
10    (sources.disko + "/module.nix")
11    ./single-disk-layout.nix
12  ];
```

## Test the disk layout[#](https://nix.dev/tutorials/nixos/provisioning-remote-machines#test-the-disk-layout "Link to this heading")

Check that the disk layout is valid:

```
nix-build -E "((import <nixpkgs> {}).nixos [ ./configuration.nix ]).installTest"
```

This command runs the complete installation in a virtual machine by building a derivation in the `installTest` attribute provided by the `disko` module.

## Deploy the system[#](https://nix.dev/tutorials/nixos/provisioning-remote-machines#deploy-the-system "Link to this heading")

To deploy the system, build the configuration and the corresponding disk formatting script, and run `nixos-anywhere` using the results:

Important

Replace `target-host` with the hostname or IP address of your *target machine*.

```
toplevel=$(nixos-rebuild build --no-flake)
diskoScript=$(nix-build -E "((import <nixpkgs> {}).nixos [ ./configuration.nix ]).diskoScript")
nixos-anywhere --store-paths "$diskoScript" "$toplevel" root@target-host
```

Note

If you don’t have public key authentication:
Set the environment variable `SSH_PASS` to your password then append the `--env-password` flag to the `nixos-anywhere` command.

`nixos-anywhere` will now log into the target system, partition, format, and mount the disk, and install the NixOS configuration.
Then, it reboots the system.

## Update the system[#](https://nix.dev/tutorials/nixos/provisioning-remote-machines#update-the-system "Link to this heading")

To update the system, run `npins` and re-deploy the configuration:

```
npins update nixpkgs
nixos-rebuild switch --no-flake --target-host root@target-host
```

`nixos-anywhere` is not needed any more, unless you want to change the disk layout.

# Next steps[#](https://nix.dev/tutorials/nixos/provisioning-remote-machines#next-steps "Link to this heading")

* [Setting up an HTTP binary cache](https://nix.dev/tutorials/nixos/binary-cache-setup)
* [Setting up post-build hooks](https://nix.dev/guides/recipes/post-build-hook#post-build-hooks)

## References[#](https://nix.dev/tutorials/nixos/provisioning-remote-machines#references "Link to this heading")

* [`nixos-anywhere` project page](https://nix-community.github.io/nixos-anywhere/)
* [`disko` project repository](https://github.com/nix-community/disko)
* [Collection of disk layout examples](https://github.com/nix-community/disko/tree/master/example)

Contents