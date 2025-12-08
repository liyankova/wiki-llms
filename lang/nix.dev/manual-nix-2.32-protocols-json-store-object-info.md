---
url: https://nix.dev/manual/nix/2.32/protocols/json/store-object-info
title: Store Object Info - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Store Object Info - Nix 2.32.2 Reference Manual

# [Store object info JSON format](https://nix.dev/manual/nix/2.32/protocols/json/store-object-info#store-object-info-json-format)

> **Warning**
>
> This JSON format is currently
> [**experimental**](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-nix-command)
> and subject to change.

Info about a [store object].

* `path`:

  [Store path](https://nix.dev/manual/nix/2.32/store/store-path) to the given store object.
* `narHash`:

  Hash of the [file system object](https://nix.dev/manual/nix/2.32/store/file-system-object) part of the store object when serialized as a [Nix Archive](https://nix.dev/manual/nix/2.32/store/file-system-object/content-address#serial-nix-archive).
* `narSize`:

  Size of the [file system object](https://nix.dev/manual/nix/2.32/store/file-system-object) part of the store object when serialized as a [Nix Archive](https://nix.dev/manual/nix/2.32/store/file-system-object/content-address#serial-nix-archive).
* `references`:

  An array of [store paths](https://nix.dev/manual/nix/2.32/store/store-path), possibly including this one.
* `ca`:

  If the store object is [content-addressed](https://nix.dev/manual/nix/2.32/store/store-object/content-address),
  this is the content address of this store object's file system object, used to compute its store path.
  Otherwise (i.e. if it is [input-addressed](https://nix.dev/manual/nix/2.32/glossary#gloss-input-addressed-store-object)), this is `null`.

## [Impure fields](https://nix.dev/manual/nix/2.32/protocols/json/store-object-info#impure-fields)

These are not intrinsic properties of the store object.
In other words, the same store object residing in different store could have different values for these properties.

* `deriver`:

  If known, the path to the [store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation) from which this store object was produced.
  Otherwise `null`.
* `registrationTime` (optional):

  If known, when this derivation was added to the store.
  Otherwise `null`.
* `ultimate`:

  Whether this store object is trusted because we built it ourselves, rather than substituted a build product from elsewhere.
* `signatures`:

  Signatures claiming that this store object is what it claims to be.
  Not relevant for [content-addressed](https://nix.dev/manual/nix/2.32/store/store-object/content-address) store objects,
  but useful for [input-addressed](https://nix.dev/manual/nix/2.32/glossary#gloss-input-addressed-store-object) store objects.

### [`.narinfo` extra fields](https://nix.dev/manual/nix/2.32/protocols/json/store-object-info#narinfo-extra-fields)

This meta data is specific to the "binary cache" family of Nix store types.
This information is not intrinsic to the store object, but about how it is stored.

* `url`:

  Where to download a compressed archive of the file system objects of this store object.
* `compression`:

  The compression format that the archive is in.
* `fileHash`:

  A digest for the compressed archive itself, as opposed to the data contained within.
* `fileSize`:

  The size of the compressed archive itself.

## [Computed closure fields](https://nix.dev/manual/nix/2.32/protocols/json/store-object-info#computed-closure-fields)

These fields are not stored at all, but computed by traversing the other fields across all the store objects in a [closure](https://nix.dev/manual/nix/2.32/glossary#gloss-closure).

* `closureSize`:

  The total size of the compressed archive itself for this object, and the compressed archive of every object in this object's [closure](https://nix.dev/manual/nix/2.32/glossary#gloss-closure).

### [`.narinfo` extra fields](https://nix.dev/manual/nix/2.32/protocols/json/store-object-info#narinfo-extra-fields-1)

* `closureSize`:

  The total size of this store object and every other object in its [closure](https://nix.dev/manual/nix/2.32/glossary#gloss-closure).