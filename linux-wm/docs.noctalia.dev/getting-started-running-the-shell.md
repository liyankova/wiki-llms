---
url: https://docs.noctalia.dev/getting-started/running-the-shell/
title: Running the shell | Noctalia Docs
source_domain: docs.noctalia.dev
---

# Running the shell | Noctalia Docs

# Running the shell

### Autostart by your Wayland compositor

[Section titled “Autostart by your Wayland compositor”](https://docs.noctalia.dev/getting-started/running-the-shell/#autostart-by-your-wayland-compositor)

This is the recommended method for launching noctalia-shell, as it integrates with your window manager.

For the *Niri* compositor, add the following line to the end of your configuration file, typically located at `~/.config/niri/config.kdl`

```
spawn-at-startup "qs" "-c" "noctalia-shell"
```

For the *Hyprland* compositor, append this line to your configuration file, typically located at `~/.config/hypr/hyprland.conf`

```
exec-once = qs -c noctalia-shell
```

### Running as a Systemd Service (Advanced)

[Section titled “Running as a Systemd Service (Advanced)”](https://docs.noctalia.dev/getting-started/running-the-shell/#running-as-a-systemd-service-advanced)

For more robust process management, you can configure Noctalia to run as a systemd user service. This approach provides automatic restarts on failure and centralizes logging with `journalctl`.

#### 1. Create the service file

[Section titled “1. Create the service file”](https://docs.noctalia.dev/getting-started/running-the-shell/#1-create-the-service-file)

First, create a new service definition file at `~/.config/systemd/user/noctalia.service` with the following content:

```
[Unit]

Description=Noctalia Shell Service

PartOf=graphical-session.target

Requisite=graphical-session.target

After=graphical-session.target

[Service]

ExecStart=qs -c noctalia-shell

Restart=on-failure

RestartSec=1

[Install]

WantedBy=graphical-session.target
```

#### 2. Enable and Start the Service

[Section titled “2. Enable and Start the Service”](https://docs.noctalia.dev/getting-started/running-the-shell/#2-enable-and-start-the-service)

Next, enable the service to have it start automatically with your graphical session.

If you use a compositor like Niri, it’s best to tie Noctalia directly to it. This ensures they start and stop together.

Terminal window

```
# Example for Niri users

systemctl --user add-wants niri.service noctalia.service
```

Alternatively, you can enable it more generally with:

Terminal window

```
systemctl --user enable --now noctalia.service
```

### Manual Launch for Debugging

[Section titled “Manual Launch for Debugging”](https://docs.noctalia.dev/getting-started/running-the-shell/#manual-launch-for-debugging)

The most direct way to run Noctalia for testing or debugging is to invoke it through Quickshell. Open a terminal and execute:

Terminal window

```
qs -c noctalia-shell
```