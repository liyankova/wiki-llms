---
url: https://docs.noctalia.dev/getting-started/keybinds
title: Keybinds | Noctalia Docs
source_domain: docs.noctalia.dev
---

# Keybinds | Noctalia Docs

# Keybinds

Take full control of Noctalia with keyboard shortcuts and IPC commands. This page covers how to start the shell and all available commands you can bind to your favorite keys.

## Available Commands

[Section titled “Available Commands”](https://docs.noctalia.dev/getting-started/keybinds#available-commands)

Noctalia provides extensive IPC (Inter-Process Communication) support, allowing you to control every aspect of the shell through commands. These are perfect for binding to keyboard shortcuts in your window manager or desktop environment.

### Core Functions

[Section titled “Core Functions”](https://docs.noctalia.dev/getting-started/keybinds#core-functions)

| Function | Command | Description |
| --- | --- | --- |
| **Application Launcher** | `qs -c noctalia-shell ipc call launcher toggle` | Open/close the application launcher |
| **Control Center** | `qs -c noctalia-shell ipc call controlCenter toggle` | Toggle the control center visibility |
| **Settings** | `qs -c noctalia-shell ipc call settings toggle` | Open/close the settings window |

### Quick Access

[Section titled “Quick Access”](https://docs.noctalia.dev/getting-started/keybinds#quick-access)

| Function | Command | Description |
| --- | --- | --- |
| **Clipboard History** | `qs -c noctalia-shell ipc call launcher clipboard` | Access your clipboard history |
| **Calculator** | `qs -c noctalia-shell ipc call launcher calculator` | Quick calculator access |
| **Emoji** | `qs -c noctalia-shell ipc call launcher emoji` | Quick emoji selector access |
| **Calendar** | `qs -c noctalia-shell ipc call calendar toggle` | Open/close the Calendar window |
| **Session Menu** | `qs -c noctalia-shell ipc call sessionMenu toggle` | Logout, reboot, shutdown… |
| **Lock & Suspend** | `qs -c noctalia-shell ipc call sessionMenu lockAndSuspend` | Lock the screen and suspend the system |

### System Controls

[Section titled “System Controls”](https://docs.noctalia.dev/getting-started/keybinds#system-controls)

#### Audio Management

[Section titled “Audio Management”](https://docs.noctalia.dev/getting-started/keybinds#audio-management)

| Function | Command | Description |
| --- | --- | --- |
| **Volume Up** | `qs -c noctalia-shell ipc call volume increase` | Increase system volume |
| **Volume Down** | `qs -c noctalia-shell ipc call volume decrease` | Decrease system volume |
| **Mute Output** | `qs -c noctalia-shell ipc call volume muteOutput` | Toggle output audio mute |
| **Input Up** | `qs -c noctalia-shell ipc call volume increaseInput` | Increase input volume |
| **Input Down** | `qs -c noctalia-shell ipc call volume decreaseInput` | Decrease input volume |
| **Mute Input** | `qs -c noctalia-shell ipc call volume muteInput` | Toggle input audio mute |

#### Media Controls

[Section titled “Media Controls”](https://docs.noctalia.dev/getting-started/keybinds#media-controls)

| Function | Command | Description |
| --- | --- | --- |
| **Play/Pause** | `qs -c noctalia-shell ipc call media playPause` | Toggle play/pause for media |
| **Play** | `qs -c noctalia-shell ipc call media play` | Play media |
| **Pause** | `qs -c noctalia-shell ipc call media pause` | Pause media |
| **Next** | `qs -c noctalia-shell ipc call media next` | Go to the next media track |
| **Previous** | `qs -c noctalia-shell ipc call media previous` | Go to the previous media track |
| **Seek Relative** | `qs -c noctalia-shell ipc call media seekRelative $offset` | Seek media by a relative offset in seconds |
| **Seek By Ratio** | `qs -c noctalia-shell ipc call media seekByRatio $position` | Seek media to a specific position from 0.0 to 1.0 |

#### Display & Brightness

[Section titled “Display & Brightness”](https://docs.noctalia.dev/getting-started/keybinds#display--brightness)

| Function | Command | Description |
| --- | --- | --- |
| **Brightness Up** | `qs -c noctalia-shell ipc call brightness increase` | Increase screen brightness |
| **Brightness Down** | `qs -c noctalia-shell ipc call brightness decrease` | Decrease screen brightness |

#### Screen Recorder

[Section titled “Screen Recorder”](https://docs.noctalia.dev/getting-started/keybinds#screen-recorder)

| Function | Command | Description |
| --- | --- | --- |
| **Screen record toggle** | `qs -c noctalia-shell ipc call screenRecorder toggle` | Start / stop the screen recording |

#### Battery Management

[Section titled “Battery Management”](https://docs.noctalia.dev/getting-started/keybinds#battery-management)

| Function | Command | Description |
| --- | --- | --- |
| **Cycle charging modes** | `qs -c noctalia-shell ipc call batteryManager cycle` | Switch between charging modes |
| **Full capacity** | `qs -c noctalia-shell ipc call batteryManager set full` | Set Full capacity mode |
| **Balanced** | `qs -c noctalia-shell ipc call batteryManager set balanced` | Set Balanced mode |
| **Lifespan** | `qs -c noctalia-shell ipc call batteryManager set lifespan` | Set Lifespan mode |

#### Power Profile Management

[Section titled “Power Profile Management”](https://docs.noctalia.dev/getting-started/keybinds#power-profile-management)

| Function | Command | Description |
| --- | --- | --- |
| **Cycle power profiles** | `qs -c noctalia-shell ipc call powerProfile cycle` | Switch between power profiles |
| \**Power Saver* | `qs -c noctalia-shell ipc call powerProfile set powersaver` | Set Power Saver mode |
| **Balanced** | `qs -c noctalia-shell ipc call powerProfile set balanced` | Set Balanced mode |
| **Performance** | `qs -c noctalia-shell ipc call powerProfile set performance` | Set Performance mode |

### Security & Privacy

[Section titled “Security & Privacy”](https://docs.noctalia.dev/getting-started/keybinds#security--privacy)

| Function | Command | Description |
| --- | --- | --- |
| **Lock Screen** | `qs -c noctalia-shell ipc call lockScreen lock` | Lock your screen |
| **Idle Inhibitor** | `qs -c noctalia-shell ipc call idleInhibitor toggle` | Prevent system from going idle |

### Notifications

[Section titled “Notifications”](https://docs.noctalia.dev/getting-started/keybinds#notifications)

| Function | Command | Description |
| --- | --- | --- |
| **Notification History** | `qs -c noctalia-shell ipc call notifications toggleHistory` | View past notifications |
| **Toggle Do Not Disturb** | `qs -c noctalia-shell ipc call notifications toggleDND` | Toggle notification silence mode |
| **Enable Do Not Disturb** | `qs -c noctalia-shell ipc call notifications enableDND` | Enable notification silence mode |
| **Disable Do Not Disturb** | `qs -c noctalia-shell ipc call notifications disableDND` | Disable notification silence mode |
| **Clear Notification History** | `qs -c noctalia-shell ipc call notifications clear` | Clear notification history |
| **Remove Oldest** | `qs -c noctalia-shell ipc call notifications removeOldestHistory` | Remove oldest notification from history |
| **Dismiss Oldest** | `qs -c noctalia-shell ipc call notifications dismissOldest` | Dismiss the oldest active notification |
| **Dismiss All** | `qs -c noctalia-shell ipc call notifications dismissAll` | Dismiss all active notifications |

### Appearance

[Section titled “Appearance”](https://docs.noctalia.dev/getting-started/keybinds#appearance)

#### Visibility

[Section titled “Visibility”](https://docs.noctalia.dev/getting-started/keybinds#visibility)

| Function | Command | Description |
| --- | --- | --- |
| **Toggle Bar Visibility** | `qs -c noctalia-shell ipc call bar toggle` | Switch between invisible and visible |
| **Toggle Dock Visibility** | `qs -c noctalia-shell ipc call dock toggle` | Toggle dock visibility |

#### Theme Controls

[Section titled “Theme Controls”](https://docs.noctalia.dev/getting-started/keybinds#theme-controls)

| Function | Command | Description |
| --- | --- | --- |
| **Toggle Dark Mode** | `qs -c noctalia-shell ipc call darkMode toggle` | Switch between light/dark themes |
| **Set Dark Mode** | `qs -c noctalia-shell ipc call darkMode setDark` | Force dark theme |
| **Set Light Mode** | `qs -c noctalia-shell ipc call darkMode setLight` | Force light theme |
| **Set Color Scheme** | `qs -c noctalia-shell ipc call colorScheme set <theme>` | Set a new color scheme by name |

#### Wallpaper Management

[Section titled “Wallpaper Management”](https://docs.noctalia.dev/getting-started/keybinds#wallpaper-management)

| Function | Command | Description |
| --- | --- | --- |
| **Toggle Selector** | `qs -c noctalia-shell ipc call wallpaper toggle` | Toggle the wallpaper selector |
| **Set Wallpaper** | `qs -c noctalia-shell ipc call wallpaper set $path $monitor` | Set specific wallpaper on a monitor |
| **Random Wallpaper** | `qs -c noctalia-shell ipc call wallpaper random` | Apply a random wallpaper |
| **Toggle Automation** | `qs -c noctalia-shell ipc call wallpaper toggleAutomation` | Toggle wallpaper automation |
| **Enable Automation** | `qs -c noctalia-shell ipc call wallpaper enableAutomation` | Enable wallpaper automation |
| **Disable Automation** | `qs -c noctalia-shell ipc call wallpaper disableAutomation` | Disable wallpaper automation |

## Example Configurations

[Section titled “Example Configurations”](https://docs.noctalia.dev/getting-started/keybinds#example-configurations)

**Niri Configuration**

Add these binds to your `~/.config/niri/config.kdl`:

```
binds {

// Core Noctalia binds

Mod+Space { spawn "qs" "-c" "noctalia-shell" "ipc" "call" "launcher" "toggle"; }

Mod+S { spawn "qs" "-c" "noctalia-shell" "ipc" "call" "controlCenter" "toggle"; }

Mod+Comma { spawn "qs" "-c" "noctalia-shell" "ipc" "call" "settings" "toggle"; }

// Audio controls

XF86AudioRaiseVolume { spawn "qs" "-c" "noctalia-shell" "ipc" "call" "volume" "increase"; }

XF86AudioLowerVolume { spawn "qs" "-c" "noctalia-shell" "ipc" "call" "volume" "decrease"; }

XF86AudioMute { spawn "qs" "-c" "noctalia-shell" "ipc" "call" "volume" "muteOutput"; }

// Brightness controls

XF86MonBrightnessUp { spawn "qs" "-c" "noctalia-shell" "ipc" "call" "brightness" "increase"; }

XF86MonBrightnessDown { spawn "qs" "-c" "noctalia-shell" "ipc" "call" "brightness" "decrease"; }

// Utility shortcuts

Mod+V { spawn "qs" "-c" "noctalia-shell" "ipc" "call" "launcher" "clipboard"; }

Mod+C { spawn "qs" "-c" "noctalia-shell" "ipc" "call" "launcher" "calculator"; }

Mod+L { spawn "qs" "-c" "noctalia-shell" "ipc" "call" "lockScreen" "lock"; }

}
```

**Hyprland Configuration**

Add these binds to your `hyprland.conf`:

```
# Core Noctalia binds

bind = SUPER, SPACE, exec, qs -c noctalia-shell ipc call launcher toggle

bind = SUPER, S, exec, qs -c noctalia-shell ipc call controlCenter toggle

bind = SUPER, comma, exec, qs -c noctalia-shell ipc call settings toggle

# Audio controls

bindel = , XF86AudioRaiseVolume, exec, qs -c noctalia-shell ipc call volume increase

bindel = , XF86AudioLowerVolume, exec, qs -c noctalia-shell ipc call volume decrease

bindl = , XF86AudioMute, exec, qs -c noctalia-shell ipc call volume muteOutput

# Brightness controls

bindel = , XF86MonBrightnessUp, exec, qs -c noctalia-shell ipc call brightness increase

bindel = , XF86MonBrightnessDown, exec, qs -c noctalia-shell ipc call brightness decrease

# Utility shortcuts

bind = SUPER, V, exec, qs -c noctalia-shell ipc call launcher clipboard

bind = SUPER, C, exec, qs -c noctalia-shell ipc call launcher calculator

bind = SUPER, L, exec, qs -c noctalia-shell ipc call lockScreen lock
```

## Pro Tips

[Section titled “Pro Tips”](https://docs.noctalia.dev/getting-started/keybinds#pro-tips)