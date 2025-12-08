---
url: https://nix.dev/manual/nix/2.32/protocols/derivation-aterm
title: Derivation "ATerm" file format - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Derivation "ATerm" file format - Nix 2.32.2 Reference Manual

# [Derivation "ATerm" file format](https://nix.dev/manual/nix/2.32/protocols/derivation-aterm#derivation-aterm-file-format)

For historical reasons, [store derivations](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation) are stored on-disk in [ATerm](https://homepages.cwi.nl/~daybuild/daily-books/technology/aterm-guide/aterm-guide.html) format.

## [The ATerm format used](https://nix.dev/manual/nix/2.32/protocols/derivation-aterm#the-aterm-format-used)

Derivations are serialised in one of the following formats:

* ```
  Derive(...)
  ```

  For all stable derivations.
* ```
  DrvWithVersion(<version-string>, ...)
  ```

  The only `version-string`s that are in use today are for [experimental features](https://nix.dev/manual/nix/2.32/development/experimental-features):

  + `"xp-dyn-drv"` for the [`dynamic-derivations`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-dynamic-derivations) experimental feature.

## [Use for encoding to store object](https://nix.dev/manual/nix/2.32/protocols/derivation-aterm#use-for-encoding-to-store-object)

When derivation is encoded to a [store object](https://nix.dev/manual/nix/2.32/glossary#gloss-store-object) we make the following choices:

* The store path name is the derivation name with `.drv` suffixed at the end

  Indeed, the ATerm format above does *not* contain the name of the derivation, on the assumption that a store path will also be provided out-of-band.
* The derivation is content-addressed using the ["Text" method](https://nix.dev/manual/nix/2.32/store/store-object/content-address#method-text) of content-addressing derivations

Currently we always encode derivations to store object using the ATerm format (and the previous two choices),
but we reserve the option to encode new sorts of derivations differently in the future.