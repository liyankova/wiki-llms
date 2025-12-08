---
url: https://nix.dev/manual/nix/2.32/store/derivation/outputs/input-address
title: Input-addressing derivation outputs - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Input-addressing derivation outputs - Nix 2.32.2 Reference Manual

# [Input-addressing derivation outputs](https://nix.dev/manual/nix/2.32/store/derivation/outputs/input-address#input-addressing-derivation-outputs)

"Input addressing" means the address the store object by the *way it was made* rather than *what it is*.
That is to say, an input-addressed output's store path is a function not of the output itself, but of the derivation that produced it.
Even if two store paths have the same contents, if they are produced in different ways, and one is input-addressed, then they will have different store paths, and thus guaranteed to not be the same store object.