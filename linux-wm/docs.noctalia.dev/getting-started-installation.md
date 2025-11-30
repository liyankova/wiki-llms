---
url: https://docs.noctalia.dev/getting-started/installation/
title: Installation | Noctalia Docs
source_domain: docs.noctalia.dev
---

# Installation | Noctalia Docs

# Installation

Noctalia is packaged for [Arch Linux](https://docs.noctalia.dev/getting-started/installation/#arch) and [NixOS](https://docs.noctalia.dev/getting-started/nixos), but can also be [installed manually](https://docs.noctalia.dev/getting-started/installation/#manual-install) in other distributions.

## Arch Linux

[Section titled “Arch Linux”](https://docs.noctalia.dev/getting-started/installation/#arch)

### Using AUR (Recommended)

[Section titled “Using AUR (Recommended)”](https://docs.noctalia.dev/getting-started/installation/#using-aur-recommended)

The simplest way to install Noctalia on Arch Linux is through the Arch User Repository (AUR). This method installs the shell system-wide and handles dependencies automatically.

Please replace with your AUR helper of choice.

Terminal window

```
paru -S noctalia-shell
```

### Development Version

[Section titled “Development Version”](https://docs.noctalia.dev/getting-started/installation/#development-version)

For the latest features and fixes, you can install the development version directly from the Git repository:

Terminal window

```
paru -S noctalia-shell-git
```

---

## Manual Installation

[Section titled “Manual Installation”](https://docs.noctalia.dev/getting-started/installation/#manual-install)

If you prefer to install Noctalia locally or want more control over the installation process, you can install it manually to your user configuration directory. This method works on any Linux distribution.

**Step 1**: Install required dependencies

For Arch Linux:

Terminal window

```
# Core dependencies (required)

paru -S quickshell gpu-screen-recorder brightnessctl

# Desktop monitor brightness (may cause instability with some monitors)

paru -S ddcutil

# Optional dependencies

paru -S cliphist matugen-git cava wlsunset xdg-desktop-portal python3 evolution-data-server

# Polkit agent (can be any other agent)

paru -S polkit-kde-agent
```

For other distributions, install the equivalent packages using your package manager.

**Step 2**: Download and install Noctalia

Terminal window

```
mkdir -p ~/.config/quickshell/noctalia-shell && curl -sL https://github.com/noctalia-dev/noctalia-shell/releases/latest/download/noctalia-latest.tar.gz | tar -xz --strip-components=1 -C ~/.config/quickshell/noctalia-shell
```

### Dependencies Explained

[Section titled “Dependencies Explained”](https://docs.noctalia.dev/getting-started/installation/#dependencies-explained)

**Required:**

* `quickshell` - Core shell framework
* `gpu-screen-recorder` - Screen recording functionality
* `brightnessctl` - Internal/laptop monitor brightness control

**Hardware-specific:**

* `ddcutil` - Desktop monitor brightness control (⚠️ may introduce system instability with certain monitors)

**Optional but recommended:**

* `cliphist` - Clipboard history support
* `matugen-git` - Material You color scheme generation
* `cava` - Audio visualizer component
* `wlsunset` - Night light functionality
* `xdg-desktop-portal` - Enables “Portal” option in screen recorder
* `python3`, `evolution-data-server` - Calendar events
* `polkit-kde-agent` - Only needed to authenticate Battery Manager installation for laptop charge limits; skip if installing via Bin/battery-manager/install-battery-manager.sh with sudo.

---

## Getting Help

[Section titled “Getting Help”](https://docs.noctalia.dev/getting-started/installation/#getting-help)

If you encounter issues during installation:

* Check our [FAQ](https://docs.noctalia.dev/getting-started/installation/faq) for common problems
* Visit our [GitHub Issues](https://github.com/noctalia-dev/noctalia-shell/issues) page
* Join our community on [Discord](https://discord.noctalia.dev) for real-time support