---
url: https://bun.com/docs/installation
title: Installation - Bun
source_domain: bun.com
---

# Installation - Bun

## [​](https://bun.com/docs/installation#overview) Overview

Bun ships as a single, dependency-free executable. You can install it via script, package manager, or Docker across macOS, Linux, and Windows.

After installation, verify with `bun --version` and `bun --revision`.

## [​](https://bun.com/docs/installation#installation) Installation

* macOS & Linux
* Windows
* Package Managers
* Docker

Copy

```
curl -fsSL https://bun.com/install | bash
```

**Linux users**  The `unzip` package is required to install Bun. Use `sudo apt install unzip` to install the unzip package. Kernel version 5.6 or higher is strongly recommended, but the minimum is 5.1. Use `uname -r` to check Kernel version.

To check that Bun was installed successfully, open a new terminal window and run:

terminal

Copy

```
bun --version
# Output: 1.x.y

# See the precise commit of `oven-sh/bun` that you're using
bun --revision
# Output: 1.x.y+b7982ac13189
```

If you’ve installed Bun but are seeing a `command not found` error, you may have to manually add the installation
directory (`~/.bun/bin`) to your `PATH`.

Add Bun to your PATH

* macOS & Linux
* Windows

1

Determine which shell you're using

terminal

Copy

```
echo $SHELL
# /bin/zsh  or /bin/bash or /bin/fish
```

2

Open your shell configuration file

* For bash: `~/.bashrc`
* For zsh: `~/.zshrc`
* For fish: `~/.config/fish/config.fish`

3

Add the Bun directory to PATH

Add this line to your configuration file:

terminal

Copy

```
export BUN_INSTALL="$HOME/.bun"
export PATH="$BUN_INSTALL/bin:$PATH"
```

4

Reload your shell configuration

terminal

Copy

```
source ~/.bashrc  # or ~/.zshrc
```

---

## [​](https://bun.com/docs/installation#upgrading) Upgrading

Once installed, the binary can upgrade itself:

terminal

Copy

```
bun upgrade
```

**Homebrew users**   
To avoid conflicts with Homebrew, use `brew upgrade bun` instead.**Scoop users**   
To avoid conflicts with Scoop, use `scoop update bun` instead.

---

## [​](https://bun.com/docs/installation#canary-builds) Canary Builds

[-> View canary build](https://github.com/oven-sh/bun/releases/tag/canary)
Bun automatically releases an (untested) canary build on every commit to main. To upgrade to the latest canary build:

terminal

Copy

```
# Upgrade to latest canary
bun upgrade --canary

# Switch back to stable
bun upgrade --stable
```

The canary build is useful for testing new features and bug fixes before they’re released in a stable build. To help the Bun team fix bugs faster, canary builds automatically upload crash reports to Bun’s team.

---

## [​](https://bun.com/docs/installation#installing-older-versions) Installing Older Versions

Since Bun is a single binary, you can install older versions by re-running the installer script with a specific version.

* Linux & macOS
* Windows

To install a specific version, pass the git tag to the install script:

terminal

Copy

```
curl -fsSL https://bun.com/install | bash -s "bun-v1.3.3"
```

---

## [​](https://bun.com/docs/installation#direct-downloads) Direct Downloads

To download Bun binaries directly, visit the [releases page on GitHub](https://github.com/oven-sh/bun/releases).

### [​](https://bun.com/docs/installation#latest-version-downloads) Latest Version Downloads

[![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/linux.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=300e7a130d2220736a473333f9679855](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/linux.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=300e7a130d2220736a473333f9679855)

## Linux x64

Standard Linux x64 binary](https://github.com/oven-sh/bun/releases/latest/download/bun-linux-x64.zip)[![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/linux.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=300e7a130d2220736a473333f9679855](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/linux.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=300e7a130d2220736a473333f9679855)

## Linux x64 Baseline

For older CPUs without AVX2](https://github.com/oven-sh/bun/releases/latest/download/bun-linux-x64-baseline.zip)[![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/windows.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=4588088d53614404d5bbf7ff09e683ed](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/windows.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=4588088d53614404d5bbf7ff09e683ed)

## Windows x64

Standard Windows binary](https://github.com/oven-sh/bun/releases/latest/download/bun-windows-x64.zip)[![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/windows.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=4588088d53614404d5bbf7ff09e683ed](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/windows.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=4588088d53614404d5bbf7ff09e683ed)

## Windows x64 Baseline

For older CPUs without AVX2](https://github.com/oven-sh/bun/releases/latest/download/bun-windows-x64-baseline.zip)[![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/apple.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=0ac996da7680574a1630b68716af5714](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/apple.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=0ac996da7680574a1630b68716af5714)

## macOS ARM64

Apple Silicon (M1/M2/M3)](https://github.com/oven-sh/bun/releases/latest/download/bun-darwin-aarch64.zip)[![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/apple.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=0ac996da7680574a1630b68716af5714](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/apple.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=0ac996da7680574a1630b68716af5714)

## macOS x64

Intel Macs](https://github.com/oven-sh/bun/releases/latest/download/bun-darwin-x64.zip)[![https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/linux.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=300e7a130d2220736a473333f9679855](https://mintcdn.com/bun-1dd33a4e/Hq64iapoQXHbYMEN/icons/linux.svg?fit=max&auto=format&n=Hq64iapoQXHbYMEN&q=85&s=300e7a130d2220736a473333f9679855)

## Linux ARM64

ARM64 Linux systems](https://github.com/oven-sh/bun/releases/latest/download/bun-linux-aarch64.zip)

### [​](https://bun.com/docs/installation#musl-binaries) Musl Binaries

For distributions without `glibc` (Alpine Linux, Void Linux):

* [Linux x64 musl](https://github.com/oven-sh/bun/releases/latest/download/bun-linux-x64-musl.zip)
* [Linux x64 musl baseline](https://github.com/oven-sh/bun/releases/latest/download/bun-linux-x64-musl-baseline.zip)
* [Linux ARM64 musl](https://github.com/oven-sh/bun/releases/latest/download/bun-linux-aarch64-musl.zip)

If you encounter an error like `bun: /lib/x86_64-linux-gnu/libm.so.6: version GLIBC_2.29 not found`, try using the
musl binary. Bun’s install script automatically chooses the correct binary for your system.

---

## [​](https://bun.com/docs/installation#cpu-requirements) CPU Requirements

Bun has specific CPU requirements based on the binary you’re using:

* Standard Builds
* Baseline Builds

**x64 binaries** target the Haswell CPU architecture (AVX and AVX2 instructions required)

| Platform | Intel Requirement | AMD Requirement |
| --- | --- | --- |
| x64 | Haswell (4th gen Core) or newer | Excavator or newer |

Bun does not support CPUs older than the baseline target, which mandates the SSE4.2 extension. macOS requires version
13.0 or later.

---

## [​](https://bun.com/docs/installation#uninstall) Uninstall

To remove Bun from your system:

* macOS & Linux
* Windows
* Package Managers

terminal

Copy

```
rm -rf ~/.bun
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/installation.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /installation)

⌘I