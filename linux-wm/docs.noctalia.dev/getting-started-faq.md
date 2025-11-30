---
url: https://docs.noctalia.dev/getting-started/faq/
title: FAQ | Noctalia Docs
source_domain: docs.noctalia.dev
---

# FAQ | Noctalia Docs

# FAQ

Find answers to common questions about Noctalia installation, configuration, and usage.

## Frequently Asked Questions

[Section titled “Frequently Asked Questions”](https://docs.noctalia.dev/getting-started/faq/#frequently-asked-questions)

**Why are some of my app icons missing?**

The issue is most likely that your environment variables and icons theme are not set properly.

Add these variables via your compositor or to `/etc/environment` and reboot.
On NixOS, use `environment.variables` or `home.sessionVariables`.

Then use one of the three following options:

**How can I make empty or unused workspaces always show up in Hyprland?**

To make workspaces always visible, even when empty, you need to set them as persistent in your hyprland.conf file. You can find the specific syntax and examples in the official documentation for [Workspace Rules](https://wiki.hypr.land/Configuring/Workspace-Rules/#rules).

```
workspace = 1, monitor:DP-1, persistent:true

workspace = 2, monitor:DP-1, persistent:true

workspace = 3, monitor:DP-1, persistent:true

workspace = 4, monitor:DP-1, persistent:true

workspace = 5, monitor:DP-1, persistent:true
```

**How can I make the UI bigger?**

You can start noctalia-shell like this to make the UI bigger:
`QT_SCALE_FACTOR=2 qs -c noctalia-shell`
You might have to play around with the scale factor to fit your needs.
This can also be added to your compositor autostart.

**How can I run Noctalia on distributions other than Arch and NixOS?**

Most distributions offer `quickshell`. If you can install either, you can use Noctalia. If your distro doesn’t provide Quickshell, you can build it from source.

**How can I get Noctalia to display in my language?**

Noctalia automatically uses your operating system’s language settings. If the application appears in English, it’s likely because a translation for your language isn’t available yet, causing it to use English as a fallback.

How to Change the Language
Changing Noctalia’s language involves adjusting your computer’s system-wide language settings, not a setting within the app itself.

1. Check if Your Language is Supported
   First, you can see which translations are included with Noctalia. Look inside the installation folder for a directory named /Assets/Translations. You’ll find files ending in .json, named with language codes (e.g., es.json for Spanish, fr.json for French, de.json for German). If you don’t see a file for your language, you’ll need to use one that is available.
2. Set Your System Language
   You’ll need to change the primary language for your entire operating system.

The method varies by distribution. For command-line users, the localectl command is common. For example, to set your language to Spanish (Spain), you would run:

Terminal window

```
sudo localectl set-locale LANG=es_ES.UTF-8
```

After changing your system’s language, restart Noctalia for the changes to take effect.

If Noctalia doesn’t support your language yet, consider contributing a translation! Check the project’s repository on GitHub for instructions on how to contribute.

**Why aren’t my keybinds working?**

Common causes:

1. **Wrong command syntax**: Make sure you’re using the correct IPC command format
2. **Window manager configuration**: Verify your keybind syntax matches your WM (Hyprland vs Niri)
3. **Noctalia not running**: Keybinds only work when Noctalia is running
**What window managers does Noctalia support?**

Noctalia is designed for and tested with Hyprland and Niri. While it may work with other compositors, we currently only support workspace indicators for Niri and Hyprland.

**Why wont some applications appear in the launcher?**

The launcher looks for `.desktop` files in standard locations. If an application doesn’t appear:

1. **Refresh the launcher cache** by restarting Noctalia.
2. **Verify that a `.desktop` file exists** in one of these directories:
   * `/usr/share/applications/`
   * `~/.local/share/applications/`
   * `$HOME/.nix-profile/share/applications/` (apps installed with Nix/Home Manager)
   * `/etc/profiles/per-user/$USER/share/applications/` (system/user-wide Nix profiles)
3. **Create a `.desktop` file manually** for custom applications if none is provided.
**Why my screen recorder won’t start recording?**

Common causes:

1. **Missing package**: Make sure you’re have installed the proper package or flatpak
2. **Portal crashed**: Verify the status of your xdg-desktop-portal-xxx service and/or restart it. On Niri the gnome portal is recommended and can be restarted using the following command: `systemctl --user restart xdg-desktop-portal-gnome.service`
3. **Change the vide source**: In Noctalia’s settings, switch the source from portal to screen. And try recording.
4. **Check output in terminal**: `gpu-screen-recorder -w screen -f 60 -a default_output -o video.mp4`
**Why does Noctalia crash on startup?**

1. **Check the error output** by running Noctalia from the terminal
2. **Update dependencies** - outdated Quickshell versions can cause issues
3. **Check system logs** for additional error information
**Why does the shell look different than expected?**

1. **Check your theme settings** in the settings panel
2. **Verify your display settings** - scaling and resolution can affect appearance
3. **Update to the latest version** - UI improvements are frequently released
**Why do I have a weird gap?**

This usually means `noctalia-shell` is running more than once (for example, launched by both your compositor autostart and the systemd service). Multiple instances fight over layout space and leave blank gaps.

Make sure only a single instance is started:

1. Stop extra copies (`kill -9 qs` or reboot)
2. Pick one startup method (manual, compositor autostart, systemd, or Home Manager) and disable the others
**Why can’t I unlock my lock screen??**

openSUSE in particular does not provide the required /etc/pam.d/login.
You must create an /etc/pam.d/login manually.
Execute:

Terminal window

```
sudo tee /etc/pam.d/login <<'EOF'
```

And enter:

%PAM-1.0

```
auth       include      common-auth

account    include      common-account

password   include      common-password

session    include      common-session

EOF
```

## Still Need Help?

[Section titled “Still Need Help?”](https://docs.noctalia.dev/getting-started/faq/#still-need-help)

If your question isn’t answered here:

* **Search our documentation** for more detailed guides
* **Join our Discord community** for real-time help and discussion
* **Check GitHub issues** for similar problems and solutions
* **Create a new issue** if you’ve found a bug or need specific help

Remember to include relevant system information and error messages when asking for help!