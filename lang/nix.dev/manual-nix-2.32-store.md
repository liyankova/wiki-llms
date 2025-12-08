---
url: https://nix.dev/manual/nix/2.32/store/
title: Nix Store - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Nix Store - Nix 2.32.2 Reference Manual

# [Nix Store](https://nix.dev/manual/nix/2.32/store/#nix-store)

The *Nix store* is an abstraction to store immutable file system data (such as software packages) that can have dependencies on other such data.

There are [multiple types of Nix stores](https://nix.dev/manual/nix/2.32/store/types/) with different capabilities, such as the default one on the [local filesystem](https://nix.dev/manual/nix/2.32/store/types/local-store) (`/nix/store`) or [binary caches](https://nix.dev/manual/nix/2.32/store/types/http-binary-cache-store).