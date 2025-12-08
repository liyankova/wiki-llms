---
url: https://nix.dev/manual/nix/2.32/command-ref/nix-store
title: nix-store - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# nix-store - Nix 2.32.2 Reference Manual

# [Name](https://nix.dev/manual/nix/2.32/command-ref/nix-store#name)

`nix-store` - manipulate or query the Nix store

# [Synopsis](https://nix.dev/manual/nix/2.32/command-ref/nix-store#synopsis)

`nix-store` *operation* [*options…*] [*arguments…*]
[`--option` *name* *value*]
[`--add-root` *path*]

# [Description](https://nix.dev/manual/nix/2.32/command-ref/nix-store#description)

The command `nix-store` performs primitive operations on the Nix store.
You generally do not need to run this command manually.

`nix-store` takes exactly one *operation* flag which indicates the subcommand to be performed. The following operations are available:

* [`--realise`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/realise)
* [`--serve`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/serve)
* [`--gc`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/gc)
* [`--delete`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/delete)
* [`--query`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/query)
* [`--add`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/add)
* [`--add-fixed`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/add-fixed)
* [`--verify`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/verify)
* [`--verify-path`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/verify-path)
* [`--repair-path`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/repair-path)
* [`--dump`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/dump)
* [`--restore`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/restore)
* [`--export`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/export)
* [`--import`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/import)
* [`--optimise`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/optimise)
* [`--read-log`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/read-log)
* [`--dump-db`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/dump-db)
* [`--load-db`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/load-db)
* [`--print-env`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/print-env)
* [`--generate-binary-cache-key`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/generate-binary-cache-key)

These pages can be viewed offline:

* `man nix-store-<operation>`.

  Example: `man nix-store-realise`
* `nix-store --help --<operation>`

  Example: `nix-store --help --realise`