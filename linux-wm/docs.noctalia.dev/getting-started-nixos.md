---
url: https://docs.noctalia.dev/getting-started/nixos
title: NixOS | Noctalia Docs
source_domain: docs.noctalia.dev
---

# NixOS | Noctalia Docs

# NixOS

For NixOS users, you can add Noctalia to your system configuration using flakes and the provided NixOS module.

## Installation

[Section titled “Installation”](https://docs.noctalia.dev/getting-started/nixos#installation)

To install Noctalia, you need to [add a flake input](https://docs.noctalia.dev/getting-started/nixos#add-flake-input) and [install the package](https://docs.noctalia.dev/getting-started/nixos#install-package).

### Adding the flake input

[Section titled “Adding the flake input”](https://docs.noctalia.dev/getting-started/nixos#add-flake-input)

Add the required inputs to your flake configuration:

flake.nix

```
{

description = "NixOS configuration with Noctalia";

inputs = {

nixpkgs.url = "github:nixos/nixpkgs/nixos-unstable";

noctalia = {

url = "github:noctalia-dev/noctalia-shell";

inputs.nixpkgs.follows = "nixpkgs";

};

};

outputs = inputs@{ self, nixpkgs, ... }: {

nixosConfigurations.awesomebox = nixpkgs.lib.nixosSystem {

modules = [

# ... other modules

./noctalia.nix

];

};

};

}
```

With the flake installed, we can access Noctalia packages and modules in our configuration.

### Installing the package

[Section titled “Installing the package”](https://docs.noctalia.dev/getting-started/nixos#install-package)

If you don’t use Noctalia’s NixOS or home-manager modules, you need to manually install the default Noctalia package from the new `noctalia` input:

noctalia.nix

```
{ pkgs, inputs, ... }:

{

# install package

environment.systemPackages = with pkgs; [

inputs.noctalia.packages.${pkgs.stdenv.hostPlatform.system}.default

# ... maybe other stuff

];

}
```

Rebuild with `sudo nixos-rebuild switch --flake .`.

---

## Config with home-manager

[Section titled “Config with home-manager”](https://docs.noctalia.dev/getting-started/nixos#config-with-home-manager)

If you have [home manager](https://github.com/nix-community/home-manager) installed, you can configure your Noctalia shell in Nix.

### Noctalia settings

[Section titled “Noctalia settings”](https://docs.noctalia.dev/getting-started/nixos#noctalia-settings)

To configure Noctalia settings, you can use the Noctalia home manager module:

noctalia.nix

```
{ pkgs, inputs, ... }:

{

home-manager.users.drfoobar = {

# import the home manager module

imports = [

inputs.noctalia.homeModules.default

];

# configure options

programs.noctalia-shell = {

enable = true;

settings = {

# configure noctalia here; defaults will

# be deep merged with these attributes.

bar = {

density = "compact";

position = "right";

showCapsule = false;

widgets = {

left = [

{

id = "SidePanelToggle";

useDistroLogo = true;

}

{

id = "WiFi";

}

{

id = "Bluetooth";

}

];

center = [

{

hideUnoccupied = false;

id = "Workspace";

labelMode = "none";

}

];

right = [

{

alwaysShowPercentage = false;

id = "Battery";

warningThreshold = 30;

}

{

formatHorizontal = "HH:mm";

formatVertical = "HH mm";

id = "Clock";

useMonospacedFont = true;

usePrimaryColor = true;

}

];

};

};

colorSchemes.predefinedScheme = "Monochrome";

general = {

avatarImage = "/home/drfoobar/.face";

radiusRatio = 0.2;

};

location = {

monthBeforeDay = true;

name = "Marseille, France";

};

};

# this may also be a string or a path to a JSON file,

# but in this case must include *all* settings.

};

};

}
```

We don’t have extensive documentation of Noctalia’s configuration options; however, you can see an up-to-date list of [configuration defaults](https://docs.noctalia.dev/getting-started/nixos#config-ref).

Additionally, if you use the [systemd service](https://docs.noctalia.dev/getting-started/nixos#systemd-service), editing the settings with the GUI will show the resulting configuration in `~/.config/noctalia/gui-settings.json`. You can then use this information to update your Nix config to make it permanent.

### Theme colors

[Section titled “Theme colors”](https://docs.noctalia.dev/getting-started/nixos#theme-colors)

To configure Noctalia settings, you can use the Noctalia home manager module. Be sure to set every Material 3 color, including hover-state values, when overriding the defaults:

noctalia.nix

```
{ pkgs, inputs, ... }:

{

home-manager.users.drfoobar = {

# import the home manager module

imports = [

inputs.noctalia.homeModules.default

];

# configure options

programs.noctalia-shell = {

enable = true;

colors = {

# you must set ALL of these

mError = "#dddddd";

mOnError = "#111111";

mOnPrimary = "#111111";

mOnSecondary = "#111111";

mOnSurface = "#828282";

mOnSurfaceVariant = "#5d5d5d";

mOnTertiary = "#111111";

mOnHover = "#ffffff";

mOutline = "#3c3c3c";

mPrimary = "#aaaaaa";

mSecondary = "#a7a7a7";

mShadow = "#000000";

mSurface = "#111111";

mHover = "#1f1f1f";

mSurfaceVariant = "#191919";

mTertiary = "#cccccc";

};

# this may also be a string or a path to a JSON file.

};

};

}
```

### Keybinds

[Section titled “Keybinds”](https://docs.noctalia.dev/getting-started/nixos#keybinds)

Keybindings are configured in your compositor. You make IPC calls to Noctalia [as explained in the keybinds section](https://docs.noctalia.dev/getting-started/keybinds). The only difference is that you can call `noctalia-shell` instead of `qs -c noctalia-shell`.

To safely configure noctalia keybindings in the Niri flake, be sure to pass a list:

niri.nix

```
{ pkgs, inputs, ... }:

{

# ...

home-manager.users.drfoobar =

{ config, ... }:

{

# ...

programs.niri = {

settings = {

# ...

binds = with config.lib.niri.actions; {

"Mod+Space".action.spawn = [

"noctalia-shell" "ipc" "call" "launcher" "toggle" # ✅

];

"Mod+P".action.spawn =

"noctalia-shell ipc call sessionMenu toggle"; # ❌

};

};

};

}
```

It may be convenient to define a utility function to allow you to use simple strings:

niri.nix

```
{ pkgs, inputs, ... }:

let

noctalia = cmd: [

"noctalia-shell" "ipc" "call"

] ++ (pkgs.lib.splitString " " cmd);

in

{

# ...

home-manager.users.drfoobar =

{ config, lib, ... }:

{

# ...

programs = {

niri = {

# ...

settings = {

binds = with config.lib.niri.actions; {

# ...

"Mod+L".action.spawn = noctalia "lockScreen toggle";

"XF86AudioLowerVolume".action.spawn = noctalia "volume decrease";

"XF86AudioRaiseVolume".action.spawn = noctalia "volume increase";

"XF86AudioMute".action.spawn = noctalia "volume muteOutput";

# etc

};

};

};

};

}
```

---

## Running the shell

[Section titled “Running the shell”](https://docs.noctalia.dev/getting-started/nixos#running-the-shell)

The Noctalia shell can now be run in two ways: [manually](https://docs.noctalia.dev/getting-started/nixos#running-manually) or using a systemd service

### Running manually

[Section titled “Running manually”](https://docs.noctalia.dev/getting-started/nixos#running-manually)

To run Noctalia using the flake, run:

Terminal window

```
noctalia-shell
```

With the [Niri flake](https://github.com/sodiboo/niri-flake), you can then spawn Noctalia on startup like this:

niri.nix

```
{ pkgs, inputs, ... }:

{

# ...

home-manager.users.drfoobar = {

# ...

programs.niri = {

package = niri;

settings = {

# ...

spawn-at-startup = [

{

command = [

"noctalia-shell"

];

}

];

};

};

};

}
```

### Running with systemd

[Section titled “Running with systemd”](https://docs.noctalia.dev/getting-started/nixos#systemd-service)

You can setup systemd service via NixOS module or Home Manager module. If you [configure Noctalia shell with home-manager](https://docs.noctalia.dev/getting-started/nixos#config-with-home-manager), then Home Manager module is a better choice.
and it’s best not to enable systemd service in both modules at the same time, as names of two systemd services are the same; it’s unpredictable which one will run (usually, it’s systemd service in Home Manager module).

#### NixOS module

[Section titled “NixOS module”](https://docs.noctalia.dev/getting-started/nixos#nixos-module)

Import the Noctalia NixOS modules and enable the service:

noctalia.nix

```
{ pkgs, inputs, ... }:

{

# import the nixos module

imports = [

inputs.noctalia.nixosModules.default

];

# enable the systemd service

services.noctalia-shell.enable = true;

}
```

The service will start after [`graphical-session.target`](https://www.freedesktop.org/software/systemd/man/latest/systemd.special.html#graphical-session.target) by default, which will work correctly out of the box for [Niri](https://github.com/YaLTeR/niri) and [Hyprland with UWSM](https://wiki.hypr.land/Useful-Utilities/Systemd-start/#uwsm).

If you have some custom target, you can configure it with the `target` option:

noctalia.nix

```
{ pkgs, inputs, ... }:

{

# ...

services.noctalia-shell = {

enable = true;

target = "my-hyprland-session.target";

};

}
```

This target depends on how you configure your Hyprland session systemd service.

#### Home Manager module

[Section titled “Home Manager module”](https://docs.noctalia.dev/getting-started/nixos#home-manager-module)

Import the Noctalia Home Manager modules and enable the service:

noctalia.nix

```
{ pkgs, inputs, ... }:

{

home-manager.users.drfoobar = {

# import the home manager module

imports = [

inputs.noctalia.homeModules.default

];

# enable the systemd service

programs.noctalia-shell.systemd.enable = true;

};

}
```

The systemd service target is set by the `wayland.systemd.target` option in Home Manager.

---

## Calendar events support

[Section titled “Calendar events support”](https://docs.noctalia.dev/getting-started/nixos#calendar-events-support)

To add support for events in the calendar via evolution-data-server.

noctalia.nix

```
{ pkgs, inputs, ... }:

{

services.gnome.evolution-data-server.enable = true;

environment.systemPackages = with pkgs; [

(python3.withPackages (pyPkgs: with pyPkgs; [ pygobject3 ]))

];

environment.sessionVariables = {

GI_TYPELIB_PATH = lib.makeSearchPath "lib/girepository-1.0" (

with pkgs;

[

evolution-data-server

libical

glib.out

libsoup_3

json-glib

gobject-introspection

]

);

};

}
```

---

## Configuration Defaults

[Section titled “Configuration Defaults”](https://docs.noctalia.dev/getting-started/nixos#config-ref)

There is no comprehensive documentation of all configuration options, but the default values are autogenerated and placed in a [`settings-default.json`](https://github.com/noctalia-dev/noctalia-shell/blob/main/Assets/settings-default.json) in the Noctalia shell repository. We retrieve a live Nixified version of these here for your convenience:

noctalia.nix

```
{ pkgs, inputs, ... }:

{

home-manager.users.drfoobar = {

imports = [

inputs.noctalia.homeModules.default

];

programs.noctalia-shell = {

enable = true;

settings = {

settingsVersion = 25;

bar = {

position = "top";

backgroundOpacity = 1;

monitors = [ ];

density = "default";

showCapsule = true;

capsuleOpacity = 1;

floating = false;

marginVertical = 0.25;

marginHorizontal = 0.25;

outerCorners = true;

exclusive = true;

widgets = {

left = [

{

id = "ControlCenter";

}

{

id = "SystemMonitor";

}

{

id = "ActiveWindow";

}

{

id = "MediaMini";

}

];

center = [

{

id = "Workspace";

}

];

right = [

{

id = "ScreenRecorder";

}

{

id = "Tray";

}

{

id = "NotificationHistory";

}

{

id = "Battery";

}

{

id = "Volume";

}

{

id = "Brightness";

}

{

id = "Clock";

}

];

};

};

general = {

avatarImage = "";

dimmerOpacity = 0.6;

showScreenCorners = false;

forceBlackScreenCorners = false;

scaleRatio = 1;

radiusRatio = 1;

screenRadiusRatio = 1;

animationSpeed = 1;

animationDisabled = false;

compactLockScreen = false;

lockOnSuspend = true;

showHibernateOnLockScreen = false;

enableShadows = true;

shadowDirection = "bottom_right";

shadowOffsetX = 2;

shadowOffsetY = 3;

language = "";

allowPanelsOnScreenWithoutBar = true;

};

ui = {

fontDefault = "Roboto";

fontFixed = "DejaVu Sans Mono";

fontDefaultScale = 1;

fontFixedScale = 1;

tooltipsEnabled = true;

panelBackgroundOpacity = 1;

panelsAttachedToBar = true;

settingsPanelAttachToBar = false;

};

location = {

name = "Tokyo";

weatherEnabled = true;

weatherShowEffects = true;

useFahrenheit = false;

use12hourFormat = false;

showWeekNumberInCalendar = false;

showCalendarEvents = true;

showCalendarWeather = true;

analogClockInCalendar = false;

firstDayOfWeek = -1;

};

calendar = {

cards = [

{

enabled = true;

id = "banner-card";

}

{

enabled = true;

id = "calendar-card";

}

{

enabled = true;

id = "timer-card";

}

{

enabled = true;

id = "weather-card";

}

];

};

screenRecorder = {

directory = "";

frameRate = 60;

audioCodec = "opus";

videoCodec = "h264";

quality = "very_high";

colorRange = "limited";

showCursor = true;

audioSource = "default_output";

videoSource = "portal";

};

wallpaper = {

enabled = true;

overviewEnabled = false;

directory = "";

enableMultiMonitorDirectories = false;

recursiveSearch = false;

setWallpaperOnAllMonitors = true;

fillMode = "crop";

fillColor = "#000000";

randomEnabled = false;

randomIntervalSec = 300;

transitionDuration = 1500;

transitionType = "random";

transitionEdgeSmoothness = 0.05;

panelPosition = "follow_bar";

hideWallpaperFilenames = false;

useWallhaven = false;

wallhavenQuery = "";

wallhavenSorting = "relevance";

wallhavenOrder = "desc";

wallhavenCategories = "111";

wallhavenPurity = "100";

wallhavenResolutionMode = "atleast";

wallhavenResolutionWidth = "";

wallhavenResolutionHeight = "";

defaultWallpaper = "";

monitors = [ ];

};

appLauncher = {

enableClipboardHistory = false;

enableClipPreview = true;

position = "center";

pinnedExecs = [ ];

useApp2Unit = false;

sortByMostUsed = true;

terminalCommand = "xterm -e";

customLaunchPrefixEnabled = false;

customLaunchPrefix = "";

viewMode = "list";

};

controlCenter = {

position = "close_to_bar_button";

shortcuts = {

left = [

{

id = "WiFi";

}

{

id = "Bluetooth";

}

{

id = "ScreenRecorder";

}

{

id = "WallpaperSelector";

}

];

right = [

{

id = "Notifications";

}

{

id = "PowerProfile";

}

{

id = "KeepAwake";

}

{

id = "NightLight";

}

];

};

cards = [

{

enabled = true;

id = "profile-card";

}

{

enabled = true;

id = "shortcuts-card";

}

{

enabled = true;

id = "audio-card";

}

{

enabled = true;

id = "weather-card";

}

{

enabled = true;

id = "media-sysmon-card";

}

];

};

systemMonitor = {

cpuWarningThreshold = 80;

cpuCriticalThreshold = 90;

tempWarningThreshold = 80;

tempCriticalThreshold = 90;

memWarningThreshold = 80;

memCriticalThreshold = 90;

diskWarningThreshold = 80;

diskCriticalThreshold = 90;

cpuPollingInterval = 3000;

tempPollingInterval = 3000;

memPollingInterval = 3000;

diskPollingInterval = 3000;

networkPollingInterval = 3000;

useCustomColors = false;

warningColor = "";

criticalColor = "";

};

dock = {

enabled = true;

displayMode = "auto_hide";

backgroundOpacity = 1;

radiusRatio = 0.1;

floatingRatio = 1;

size = 1;

onlySameOutput = true;

monitors = [ ];

pinnedApps = [ ];

colorizeIcons = false;

};

network = {

wifiEnabled = true;

};

sessionMenu = {

enableCountdown = true;

countdownDuration = 10000;

position = "center";

showHeader = true;

powerOptions = [

{

action = "lock";

enabled = true;

}

{

action = "suspend";

enabled = true;

}

{

action = "hibernate";

enabled = true;

}

{

action = "reboot";

enabled = true;

}

{

action = "logout";

enabled = true;

}

{

action = "shutdown";

enabled = true;

}

];

};

notifications = {

enabled = true;

monitors = [ ];

location = "top_right";

overlayLayer = true;

backgroundOpacity = 1;

respectExpireTimeout = false;

lowUrgencyDuration = 3;

normalUrgencyDuration = 8;

criticalUrgencyDuration = 15;

enableKeyboardLayoutToast = true;

};

osd = {

enabled = true;

location = "top_right";

autoHideMs = 2000;

overlayLayer = true;

backgroundOpacity = 1;

enabledTypes = [

0

1

2

];

monitors = [ ];

};

audio = {

volumeStep = 5;

volumeOverdrive = false;

cavaFrameRate = 30;

visualizerType = "linear";

visualizerQuality = "high";

mprisBlacklist = [ ];

preferredPlayer = "";

externalMixer = "pwvucontrol || pavucontrol";

};

brightness = {

brightnessStep = 5;

enforceMinimum = true;

enableDdcSupport = false;

};

colorSchemes = {

useWallpaperColors = false;

predefinedScheme = "Noctalia (default)";

darkMode = true;

schedulingMode = "off";

manualSunrise = "06:30";

manualSunset = "18:30";

matugenSchemeType = "scheme-fruit-salad";

generateTemplatesForPredefined = true;

};

templates = {

gtk = false;

qt = false;

kcolorscheme = false;

alacritty = false;

kitty = false;

ghostty = false;

foot = false;

wezterm = false;

fuzzel = false;

discord = false;

pywalfox = false;

vicinae = false;

walker = false;

code = false;

spicetify = false;

telegram = false;

cava = false;

emacs = false;

niri = false;

enableUserTemplates = false;

};

nightLight = {

enabled = false;

forced = false;

autoSchedule = true;

nightTemp = "4000";

dayTemp = "6500";

manualSunrise = "06:30";

manualSunset = "18:30";

};

changelog = {

lastSeenVersion = "";

};

hooks = {

enabled = false;

wallpaperChange = "";

darkModeChange = "";

};

};

};

};

}
```