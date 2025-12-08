---
url: https://nix.dev/manual/nix/2.32/command-ref/files/channels
title: Channels - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Channels - Nix 2.32.2 Reference Manual

## [Channels](https://nix.dev/manual/nix/2.32/command-ref/files/channels#channels)

A directory containing symlinks to Nix channels, managed by [`nix-channel`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel):

* `$XDG_STATE_HOME/nix/profiles/channels` for regular users
* `$NIX_STATE_DIR/profiles/per-user/root/channels` for `root`

[`nix-channel`](https://nix.dev/manual/nix/2.32/command-ref/nix-channel) uses a [profile](https://nix.dev/manual/nix/2.32/command-ref/files/profiles) to store channels.
This profile contains symlinks to the contents of those channels.

## [Subscribed channels](https://nix.dev/manual/nix/2.32/command-ref/files/channels#subscribed-channels)

The list of subscribed channels is stored in

* `~/.nix-channels`
* `$XDG_STATE_HOME/nix/channels` if [`use-xdg-base-directories`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-use-xdg-base-directories) is set to `true`

in the following format:

```
<url> <name>
...
```