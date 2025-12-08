---
url: https://nix.dev/tutorials/nixos/nixos-configuration-on-vm
title: NixOS virtual machines — nix.dev  documentation
source_domain: nix.dev
---

# NixOS virtual machines — nix.dev  documentation

[Skip to main content](https://nix.dev/tutorials/nixos/nixos-configuration-on-vm#main-content)

[![](https://nix.dev/_static/img/nix.svg)
nix.dev](https://nix.dev/)

Official documentation for getting things done with Nix.

nix.dev as [PDF](https://nix.dev/nix-dev.pdf)

* [.md](https://nix.dev/_sources/tutorials/nixos/nixos-configuration-on-vm.md "Download source file")

# NixOS virtual machines

# NixOS virtual machines[#](https://nix.dev/tutorials/nixos/nixos-configuration-on-vm#nixos-virtual-machines "Link to this heading")

One of the most important features of NixOS is the ability to configure the entire system declaratively, including packages to be installed, services to be run, as well as other settings and options.

NixOS configurations can be used to test and use NixOS using a virtual machine, independent of an installation on a “bare metal” computer.

## What will you learn?[#](https://nix.dev/tutorials/nixos/nixos-configuration-on-vm#what-will-you-learn "Link to this heading")

This tutorial serves as an introduction to creating NixOS virtual machines.
Virtual machines are a practical tool for experimenting with or debugging NixOS configurations.

## What do you need?[#](https://nix.dev/tutorials/nixos/nixos-configuration-on-vm#what-do-you-need "Link to this heading")

* A Linux system with virtualisation support
* (optional) A graphical environment for running a graphical virtual machine
* A working [Nix installation](https://nix.dev/install-nix)
* Basic knowledge of the [Nix language](https://nix.dev/tutorials/nix-language#reading-nix-language)

Important

A NixOS configuration is a Nix language function following the [NixOS module](https://nixos.org/manual/nixos/stable/index.html#sec-writing-modules) convention.
For a thorough treatment of the module system, check the [Module system deep dive](https://nix.dev/tutorials/module-system/deep-dive#module-system-deep-dive) tutorial.

## Starting from a default NixOS configuration[#](https://nix.dev/tutorials/nixos/nixos-configuration-on-vm#starting-from-a-default-nixos-configuration "Link to this heading")

Note

This tutorial starts with building up your `configuration.nix` from first principles, explaining each step.
If you prefer, you can skip ahead to the [sample configuration](https://nix.dev/tutorials/nixos/nixos-configuration-on-vm#sample-nixos-config) section.

We start with a minimal `configuration.nix`:

```
1{ config, pkgs, ... }:
2
3{
4  boot.loader.systemd-boot.enable = true;
5  boot.loader.efi.canTouchEfiVariables = true;
6
7  system.stateVersion = "24.05";
8}
```

To be able to log in, add the following lines to the returned attribute set:

```
1  users.users.alice = {
2    isNormalUser = true;
3    extraGroups = [ "wheel" ];
4  };
```

Additionally, you need to specify a password for this user.
For the purpose of demonstration only, you specify an insecure, plain text password by adding the `initialPassword` option to the user configuration:

```
1   initialPassword = "test";
```

We add two lightweight programs as an example:

```
1  environment.systemPackages = with pkgs; [
2    cowsay
3    lolcat
4  ];
```

Warning

Do not use plain text passwords outside of this example unless you know what you are doing. See [`initialHashedPassword`](https://nixos.org/manual/nixos/stable/options.html#opt-users.extraUsers._name_.initialHashedPassword) or [`ssh.authorizedKeys`](https://nixos.org/manual/nixos/stable/options.html#opt-users.extraUsers._name_.openssh.authorizedKeys.keys) for more secure alternatives.

### Sample configuration[#](https://nix.dev/tutorials/nixos/nixos-configuration-on-vm#sample-configuration "Link to this heading")

The complete `configuration.nix` file looks like this:

```
 1{ config, pkgs, ... }:
 2{
 3  boot.loader.systemd-boot.enable = true;
 4  boot.loader.efi.canTouchEfiVariables = true;
 5
 6  users.users.alice = {
 7    isNormalUser = true;
 8    extraGroups = [ "wheel" ]; # Enable ‘sudo’ for the user.
 9    initialPassword = "test";
10  };
11
12  environment.systemPackages = with pkgs; [
13    cowsay
14    lolcat
15  ];
16
17  system.stateVersion = "24.05";
18}
```

## Creating a QEMU based virtual machine from a NixOS configuration[#](https://nix.dev/tutorials/nixos/nixos-configuration-on-vm#creating-a-qemu-based-virtual-machine-from-a-nixos-configuration "Link to this heading")

A NixOS virtual machine is created with the `nix-build` command:

```
$ nix-build '<nixpkgs/nixos>' -A vm -I nixpkgs=channel:nixos-24.05 -I nixos-config=./configuration.nix
```

This command builds the attribute `vm` from the `nixos-24.05` release of NixOS, using the NixOS configuration as specified in the relative path.

Detailed explanation

* The positional argument to [`nix-build`](https://nix.dev/manual/nix/stable/command-ref/nix-build.html) is a path to the derivation to be built.
  That path can be obtained from [a Nix expression that evaluates to a derivation](https://nix.dev/tutorials/nix-language#derivations).

  The virtual machine build helper is defined in NixOS, which is part of the [`nixpkgs` repository](https://github.com/NixOS/nixpkgs).
  Therefore we use the [lookup path](https://nix.dev/tutorials/nix-language#lookup-path-tutorial) `<nixpkgs/nixos>`.
* The [`-A` option](https://nix.dev/manual/nix/stable/command-ref/opt-common.html#opt-attr) specifies the attribute to pick from the provided Nix expression `<nixpkgs/nixos>`.

  To build the virtual machine, we choose the `vm` attribute as defined in [`nixos/default.nix`](https://github.com/NixOS/nixpkgs/blob/7c164f4bea71d74d98780ab7be4f9105630a2eba/nixos/default.nix#L19).
* The [`-I` option](https://nix.dev/manual/nix/stable/command-ref/opt-common.html#opt-I) prepends entries to the search path.

  Here we set `nixpkgs` to refer to a [specific version of Nixpkgs](https://nix.dev/reference/pinning-nixpkgs#ref-pinning-nixpkgs) and set `nix-config` to the `configuration.nix` file in the current directory.

## Running the virtual machine[#](https://nix.dev/tutorials/nixos/nixos-configuration-on-vm#running-the-virtual-machine "Link to this heading")

The previous command created a link with the name `result` in the working directory.
It links to the directory that contains the virtual machine.

```
$ ls -R ./result
result:
bin  system

result/bin:
run-nixos-vm
```

Run the virtual machine:

```
$ QEMU_KERNEL_PARAMS=console=ttyS0 ./result/bin/run-nixos-vm -nographic; reset
```

This command will run QEMU in the current terminal due to `-nographic`.
`console=ttyS0` will also show the boot process, which ends at the console login screen.

Log in as `alice` with the password `test`.
Check that the programs are indeed available as specified:

```
$ cowsay hello | lolcat
```

Exit the virtual machine by shutting it down:

```
$ sudo poweroff
```

Note

If you forgot to add the user to `wheel` or didn’t set a password, stop the virtual machine from a different terminal:

```
$ sudo pkill qemu
```

Running the virtual machine will create a `nixos.qcow2` file in the current directory.
This disk image file contains the dynamic state of the virtual machine.
It can interfere with debugging as it keeps the state of previous runs, for example the user password.

Delete this file when you change the configuration:

```
$ rm nixos.qcow2
```

## Running GNOME on a graphical VM[#](https://nix.dev/tutorials/nixos/nixos-configuration-on-vm#running-gnome-on-a-graphical-vm "Link to this heading")

To create a virtual machine with a graphical user interface, add the following lines to the configuration:

```
1  # Enable the X11 windowing system.
2  services.xserver.enable = true;
3
4  # Enable the GNOME Desktop Environment.
5  services.xserver.displayManager.gdm.enable = true;
6  services.xserver.desktopManager.gnome.enable = true;
```

These three lines activate X11, the GDM display manager (to be able to login) and Gnome as desktop manager.

Tip

You can also use the `installation-cd-graphical-gnome.nix` module to generate the configuration file from scratch:

```
nix-shell -I nixpkgs=channel:nixos-24.05 -p "$(cat <<EOF
  let
    pkgs = import <nixpkgs> { config = {}; overlays = []; };
    iso-config = pkgs.path + /nixos/modules/installer/cd-dvd/installation-cd-graphical-gnome.nix;
    nixos = pkgs.nixos iso-config;
  in nixos.config.system.build.nixos-generate-config
EOF
)"
```

```
$ nixos-generate-config --dir ./
```

The complete `configuration.nix` file looks like this:

```
 1{ config, pkgs, ... }:
 2{
 3  boot.loader.systemd-boot.enable = true;
 4  boot.loader.efi.canTouchEfiVariables = true;
 5
 6  services.xserver.enable = true;
 7
 8  services.xserver.displayManager.gdm.enable = true;
 9  services.xserver.desktopManager.gnome.enable = true;
10
11  users.users.alice = {
12    isNormalUser = true;
13    extraGroups = [ "wheel" ];
14    initialPassword = "test";
15  };
16
17  system.stateVersion = "24.05";
18}
```

To get graphical output, run the virtual machine without special options:

```
$ nix-build '<nixpkgs/nixos>' -A vm -I nixpkgs=channel:nixos-24.05 -I nixos-config=./configuration.nix
$ ./result/bin/run-nixos-vm
```

## Running Sway as Wayland compositor on a VM[#](https://nix.dev/tutorials/nixos/nixos-configuration-on-vm#running-sway-as-wayland-compositor-on-a-vm "Link to this heading")

To change to a Wayland compositor, disable `services.xserver.desktopManager.gnome` and enable `programs.sway`:

configuration.nix[#](https://nix.dev/tutorials/nixos/nixos-configuration-on-vm#id1 "Link to this code")

```
-  services.xserver.desktopManager.gnome.enable = true;
+  programs.sway.enable = true;
```

Note

Running Wayland compositors in a virtual machine might lead to complications with the display drivers used by QEMU.
You need to choose from the available drivers one that is compatible with Sway.
See [QEMU User Documentation](https://www.qemu.org/docs/master/system/qemu-manpage.html) for options.
One possibility is the `virtio-vga` driver:

```
$ ./result/bin/run-nixos-vm -device virtio-vga
```

Arguments to QEMU can also be added to the configuration file:

```
 1{ config, pkgs, ... }:
 2{
 3  boot.loader.systemd-boot.enable = true;
 4  boot.loader.efi.canTouchEfiVariables = true;
 5
 6  services.xserver.enable = true;
 7
 8  services.xserver.displayManager.gdm.enable = true;
 9  programs.sway.enable = true;
10
11  imports = [ <nixpkgs/nixos/modules/virtualisation/qemu-vm.nix> ];
12  virtualisation.qemu.options = [
13    "-device virtio-vga"
14  ];
15
16  users.users.alice = {
17    isNormalUser = true;
18    extraGroups = [ "wheel" ];
19    initialPassword = "test";
20  };
21
22  system.stateVersion = "24.05";
23}
```

The NixOS manual has chapters on [X11](https://nixos.org/manual/nixos/stable/#sec-x11) and [Wayland](https://nixos.org/manual/nixos/stable/#sec-wayland) listing alternative window managers.

## References[#](https://nix.dev/tutorials/nixos/nixos-configuration-on-vm#references "Link to this heading")

* [NixOS Manual: NixOS Configuration](https://nixos.org/manual/nixos/stable/index.html#ch-configuration).
* [NixOS Manual: Modules](https://nixos.org/manual/nixos/stable/index.html#sec-writing-modules).
* [NixOS Manual Options reference](https://nixos.org/manual/nixos/stable/options.html).
* [NixOS Manual: Changing the configuration](https://nixos.org/manual/nixos/stable/#sec-changing-config).
* [NixOS source code: `configuration template` in `tools.nix`](https://github.com/NixOS/nixpkgs/blob/4e0525a8cdb370d31c1e1ba2641ad2a91fded57d/nixos/modules/installer/tools/tools.nix#L122-L226).
* [NixOS source code: `vm` attribute in `default.nix`](https://github.com/NixOS/nixpkgs/blob/master/nixos/default.nix).
* [Nix manual: `nix-build`](https://nix.dev/manual/nix/stable/command-ref/nix-build.html).
* [Nix manual: common command-line options](https://nix.dev/manual/nix/stable/command-ref/opt-common.html).
* [QEMU User Documentation](https://www.qemu.org/docs/master/system/qemu-manpage.html) for more runtime options
* [NixOS option search: `virtualisation.qemu`](https://search.nixos.org/options?query=virtualisation.qemu) for declarative virtual machine configuration

## Next steps[#](https://nix.dev/tutorials/nixos/nixos-configuration-on-vm#next-steps "Link to this heading")

* [Module system deep dive](https://nix.dev/tutorials/module-system/deep-dive#module-system-deep-dive)
* [Integration testing with NixOS virtual machines](https://nix.dev/tutorials/nixos/integration-testing-using-virtual-machines#integration-testing-vms)
* [Building a bootable ISO image](https://nix.dev/tutorials/nixos/building-bootable-iso-image#bootable-iso-image)

Contents