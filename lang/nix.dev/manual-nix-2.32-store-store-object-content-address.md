---
url: https://nix.dev/manual/nix/2.32/store/store-object/content-address
title: Content-Addressing Store Objects - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Content-Addressing Store Objects - Nix 2.32.2 Reference Manual

# [Content-Addressing Store Objects](https://nix.dev/manual/nix/2.32/store/store-object/content-address#content-addressing-store-objects)

Just [like](https://nix.dev/manual/nix/2.32/store/file-system-object/content-address) [File System Objects](https://nix.dev/manual/nix/2.32/store/file-system-object),
[Store Objects](https://nix.dev/manual/nix/2.32/store/store-object) can also be [content-addressed](https://nix.dev/manual/nix/2.32/glossary#gloss-content-addressed),
unless they are [input-addressed](https://nix.dev/manual/nix/2.32/glossary#gloss-input-addressed-store-object).

For store objects, the content address we produce will take the form of a [Store Path](https://nix.dev/manual/nix/2.32/store/store-path) rather than regular hash.
In particular, the content-addressing scheme will ensure that the digest of the store path is solely computed from the

* file system object graph (the root one and its children, if it has any)
* references
* [store directory](https://nix.dev/manual/nix/2.32/store/store-path#store-directory)
* name

of the store object, and not any other information, which would not be an intrinsic property of that store object.

For the full specification of the algorithms involved, see the [specification of store path digests](https://nix.dev/manual/nix/2.32/protocols/store-path).

## [Content addressing each part of a store object](https://nix.dev/manual/nix/2.32/store/store-object/content-address#content-addressing-each-part-of-a-store-object)

### [File System Objects](https://nix.dev/manual/nix/2.32/store/store-object/content-address#file-system-objects)

With all currently-supported store object content-addressing methods, the file system object is always [content-addressed](https://nix.dev/manual/nix/2.32/store/file-system-object/content-address) first, and then that hash is incorporated into content address computation for the store object.

### [References](https://nix.dev/manual/nix/2.32/store/store-object/content-address#references)

#### [References to other store objects](https://nix.dev/manual/nix/2.32/store/store-object/content-address#references-to-other-store-objects)

With all currently supported store object content addressing methods,
other objects are referred to by their regular (string-encoded-) [store paths](https://nix.dev/manual/nix/2.32/store/store-path).

#### [Self-references](https://nix.dev/manual/nix/2.32/store/store-object/content-address#self-references)

Self-references however cannot be referred to by their path, because we are in the midst of describing how to compute that path!

> The alternative would require finding as hash function fixed point, i.e. the solution to an equation in the form
>
> ```
> digest = hash(..... || digest || ....)
> ```
>
> which is computationally infeasible.
> As far as we know, this is equivalent to finding a hash collision.

Instead we have a "has self-reference" boolean, which ends up affecting the digest:
In all currently-supported store object content-addressing methods, when hashing the file system object data, any occurrence of store object's own store path in the digested data is replaced with a [sentinel value](https://en.wikipedia.org/wiki/Sentinel_value).
The hashes of these modified input streams are used instead.

When validating the content address of a store object after the fact, the above process works as written.
However, when first creating the store object we don't know the store object's store path, as explained just above.
We therefore, strictly speaking, do not know what value we will be replacing with the sentinel value in the inputs to hash functions.
What instead happens is that the provisional store object --- the data from which we wish to create a store object --- is paired with a provisional "scratch" store path (that presumably was chosen when the data was created).
That provisional store path is instead what is replaced with the sentinel value, rather than the final store object which we do not yet know.

> **Design note**
>
> It is an informal property of content-addressed store objects that the choice of provisional store path should not matter.
> In other words, if a provisional store object is prepared in the same way except for the choice of provision store path, the provisional data need not be identical.
> But, after the sentinel value is substituted in place of each provisional store object's provision store path, the final so-normalized data *should* be identical.
>
> If, conversely, the data after this normalization process is still different, we'll compute a different content-address.
> The method of preparing the provisional self-referenced data has *failed* to be deterministic in the sense of not *leaking* the choice of provisional store path --- a choice which is supposed to be arbitrary --- into the final store object.
>
> This property is informal because at this stage, we are just described store objects, which have no formal notion of their origin.
> Without such a formal notion, there is nothing to formally accuse of being insufficiently deterministic.
> Where we cover [derivations](https://nix.dev/manual/nix/2.32/store/derivation/), we will have a chance to make this a formal property, not of content-addressed store objects themselves, but of derivations that *produce* content-addressed store objects.

### [Name and Store Directory](https://nix.dev/manual/nix/2.32/store/store-object/content-address#name-and-store-directory)

These two items affect the digest in a way that is standard for store path digest computations and not specific to content-addressing.
Consult the [specification of store path digests](https://nix.dev/manual/nix/2.32/protocols/store-path) for further details.

## [Content addressing Methods](https://nix.dev/manual/nix/2.32/store/store-object/content-address#content-addressing-methods)

For historical reasons, we don't support all features in all combinations.
Each currently supported method of content addressing chooses a single method of file system object hashing, and may offer some restrictions on references.
The names and store directories are unrestricted however.

### [Flat](https://nix.dev/manual/nix/2.32/store/store-object/content-address#method-flat)

This uses the corresponding [Flat](https://nix.dev/manual/nix/2.32/store/file-system-object/content-address#serial-flat) method of file system object content addressing.

References are not supported: store objects with flat hashing *and* references can not be created.

### [Text](https://nix.dev/manual/nix/2.32/store/store-object/content-address#method-text)

This also uses the corresponding [Flat](https://nix.dev/manual/nix/2.32/store/file-system-object/content-address#serial-flat) method of file system object content addressing.

References to other store objects are supported, but self-references are not.

This is the only store-object content-addressing method that is not named identically with a corresponding file system object method.
It is somewhat obscure, mainly used for "drv files"
(derivations serialized as store objects in their ["ATerm" file format](https://nix.dev/manual/nix/2.32/protocols/derivation-aterm)).
Prefer another method if possible.

### [Nix Archive](https://nix.dev/manual/nix/2.32/store/store-object/content-address#method-nix-archive)

This uses the corresponding [Nix Archive](https://nix.dev/manual/nix/2.32/store/file-system-object/content-address#serial-nix-archive) method of file system object content addressing.

References (to other store objects and self-references alike) are supported so long as the hash algorithm is SHA-256, but not (neither kind) otherwise.

### [Git](https://nix.dev/manual/nix/2.32/store/store-object/content-address#method-git)

> **Warning**
>
> This method is part of the [`git-hashing`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-git-hashing) experimental feature.

This uses the corresponding [Git](https://nix.dev/manual/nix/2.32/store/file-system-object/content-address#serial-git) method of file system object content addressing.

References are not supported.

Only SHA-1 is supported at this time.
If [SHA-256-based Git](https://git-scm.com/docs/hash-function-transition)
becomes more widespread, this restriction will be revisited.