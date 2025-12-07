---
url: https://bun.com/docs/guides/ecosystem/systemd
title: Run Bun as a daemon with systemd - Bun
source_domain: bun.com
---

# Run Bun as a daemon with systemd - Bun

[systemd](https://systemd.io) is an init system and service manager for Linux operating systems that manages the startup and control of system processes and services.

---

To run a Bun application as a daemon using **systemd** you’ll need to create a *service file* in `/lib/systemd/system/`.

terminal

Copy

```
cd /lib/systemd/system
touch my-app.service
```

---

Here is a typical service file that runs an application on system start. You can use this as a template for your own service. Replace `YOUR_USER` with the name of the user you want to run the application as. To run as `root`, replace `YOUR_USER` with `root`, though this is generally not recommended for security reasons.
Refer to the [systemd documentation](https://www.freedesktop.org/software/systemd/man/systemd.service.html) for more information on each setting.

my-app.service

Copy

```
[Unit]
# describe the app
Description=My App
# start the app after the network is available
After=network.target

[Service]
# usually you'll use 'simple'
# one of https://www.freedesktop.org/software/systemd/man/systemd.service.html#Type=
Type=simple
# which user to use when starting the app
User=YOUR_USER
# path to your application's root directory
WorkingDirectory=/home/YOUR_USER/path/to/my-app
# the command to start the app
# requires absolute paths
ExecStart=/home/YOUR_USER/.bun/bin/bun run index.ts
# restart policy
# one of {no|on-success|on-failure|on-abnormal|on-watchdog|on-abort|always}
Restart=always

[Install]
# start the app automatically
WantedBy=multi-user.target
```

---

If your application starts a webserver, note that non-`root` users are not able to listen on ports 80 or 443 by default. To permanently allow Bun to listen on these ports when executed by a non-`root` user, use the following command. This step isn’t necessary when running as `root`.

terminal

Copy

```
setcap CAP_NET_BIND_SERVICE=+eip ~/.bun/bin/bun
```

---

With the service file configured, you can now *enable* the service. Once enabled, it will start automatically on reboot. This requires `sudo` permissions.

terminal

Copy

```
systemctl enable my-app
```

---

To start the service without rebooting, you can manually *start* it.

terminal

Copy

```
systemctl start my-app
```

---

Check the status of your application with `systemctl status`. If you’ve started your app successfully, you should see something like this:

terminal

Copy

```
systemctl status my-app
```

Copy

```
● my-app.service - My App
     Loaded: loaded (/lib/systemd/system/my-app.service; enabled; preset: enabled)
     Active: active (running) since Thu 2023-10-12 11:34:08 UTC; 1h 8min ago
   Main PID: 309641 (bun)
      Tasks: 3 (limit: 503)
     Memory: 40.9M
        CPU: 1.093s
     CGroup: /system.slice/my-app.service
             └─309641 /home/YOUR_USER/.bun/bin/bun run /home/YOUR_USER/application/index.ts
```

---

To update the service, edit the contents of the service file, then reload the daemon.

terminal

Copy

```
systemctl daemon-reload
```

---

For a complete guide on the service unit configuration, you can check [this page](https://www.freedesktop.org/software/systemd/man/systemd.service.html). Or refer to this cheatsheet of common commands:

terminal

Copy

```
systemctl daemon-reload # tell systemd that some files got changed
systemctl enable my-app # enable the app (to allow auto-start)
systemctl disable my-app # disable the app (turns off auto-start)
systemctl start my-app # start the app if is stopped
systemctl stop my-app # stop the app
systemctl restart my-app # restart the app
```

Was this page helpful?

[Suggest edits](https://github.com/oven-sh/bun/edit/main/docs/guides/ecosystem/systemd.mdx)[Raise issue](https://github.com/oven-sh/bun/issues/new?title=Issue on docs&body=Path: /guides/ecosystem/systemd)

⌘I