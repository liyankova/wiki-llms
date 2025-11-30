---
url: https://docs.noctalia.dev/getting-started/compositor-settings/
title: Compositor Settings | Noctalia Docs
source_domain: docs.noctalia.dev
---

# Compositor Settings | Noctalia Docs

# Compositor Settings

For the best experience with Noctalia, you’ll need to configure your compositor with some specific settings.

## Niri configuration

[Section titled “Niri configuration”](https://docs.noctalia.dev/getting-started/compositor-settings/#niri-configuration)

Add the following settings to your Niri configuration file (usually located at ~/.config/niri/config.kdl).

These settings are for general window appearance and functionality.

```
window-rule {

// Rounded corners for a modern look.

geometry-corner-radius 20

// Clips window contents to the rounded corner boundaries.

clip-to-geometry true

}

debug {

// Allows notification actions and window activation from Noctalia.

honor-xdg-activation-with-invalid-serial

}
```

## Niri wallpaper and overview setup

[Section titled “Niri wallpaper and overview setup”](https://docs.noctalia.dev/getting-started/compositor-settings/#niri-wallpaper-and-overview-setup)

Next choose one of the following options for your wallpaper and overview setup.

### Option 1: Blurred Overview Wallpaper

[Section titled “Option 1: Blurred Overview Wallpaper”](https://docs.noctalia.dev/getting-started/compositor-settings/#option-1-blurred-overview-wallpaper)

This minimal configuration allows you to have a blurred and dimmed copy of your wallpaper that appears only in Niri’s overview.

![Blurred Overview Wallpaper](https://docs.noctalia.dev/_astro/option1.BVNhyECB_Zchkga.webp)

```
// Set the overview wallpaper on the backdrop.

layer-rule {

match namespace="^noctalia-overview*"

place-within-backdrop true

}
```

### Option 2: Stationary Wallpaper

[Section titled “Option 2: Stationary Wallpaper”](https://docs.noctalia.dev/getting-started/compositor-settings/#option-2-stationary-wallpaper)

If you prefer a stationary wallpaper that is visible at all times and that does not scroll when switching workspaces, use the following configuration.

![Stationary Wallpaper](https://docs.noctalia.dev/_astro/option2.DOeuvBbH_l2Hnh.webp)

```
// Set the regular wallpaper on the backdrop.

layer-rule {

match namespace="^noctalia-wallpaper*"

place-within-backdrop true

}

// Set transparent workspace background color so you see the backdrop at all times.

layout {

background-color "transparent"

}

// Optionally, disable the workspace shadows in the overview.

overview {

workspace-shadow {

off

}

}
```

### Option 3: Flat colored overview

[Section titled “Option 3: Flat colored overview”](https://docs.noctalia.dev/getting-started/compositor-settings/#option-3-flat-colored-overview)

If you prefer a more productivity oriented look, you can use this minimal configuration.

![Flat colored overview](https://docs.noctalia.dev/_astro/option3.CMRqNWK1_gduAx.webp)

```
overview {

// Choose your favorite color.

backdrop-color "#26233a"

}
```