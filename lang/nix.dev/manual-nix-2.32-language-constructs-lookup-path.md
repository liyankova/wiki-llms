---
url: https://nix.dev/manual/nix/2.32/language/constructs/lookup-path
title: Lookup path - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Lookup path - Nix 2.32.2 Reference Manual

# [Lookup path](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path#lookup-path)

> **Syntax**
>
> *lookup-path* = `<` *identifier* [ `/` *identifier* ]... `>`

A lookup path is an identifier with an optional path suffix that resolves to a [path value](https://nix.dev/manual/nix/2.32/language/types#type-path) if the identifier matches a search path entry in [`builtins.nixPath`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-nixPath).
The algorithm for lookup path resolution is described in the documentation on [`builtins.findFile`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-findFile).

> **Example**
>
> ```
> <nixpkgs>
> ```
>
> ```
> /nix/var/nix/profiles/per-user/root/channels/nixpkgs
> ```

> **Example**
>
> ```
> <nixpkgs/nixos>
> ```
>
> ```
> /nix/var/nix/profiles/per-user/root/channels/nixpkgs/nixos
> ```