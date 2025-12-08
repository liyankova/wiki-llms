---
url: https://nix.dev/manual/nix/2.32/glossary
title: Glossary - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Glossary - Nix 2.32.2 Reference Manual

# [Glossary](https://nix.dev/manual/nix/2.32/glossary#glossary)

* [build system](https://nix.dev/manual/nix/2.32/glossary#gloss-build-system)

  Generic term for software that facilitates the building of software by automating the invocation of compilers, linkers, and other tools.

  Nix can be used as a generic build system.
  It has no knowledge of any particular programming language or toolchain.
  These details are specified in [derivation expressions](https://nix.dev/manual/nix/2.32/glossary#gloss-derivation-expression).
* [content address](https://nix.dev/manual/nix/2.32/glossary#gloss-content-address)

  A
  [*content address*](https://en.wikipedia.org/wiki/Content-addressable_storage)
  is a secure way to reference immutable data.
  The reference is calculated directly from the content of the data being referenced, which means the reference is
  [*tamper proof*](https://en.wikipedia.org/wiki/Tamperproofing)
  --- variations of the data should always calculate to distinct content addresses.

  For how Nix uses content addresses, see:

  + [Content-Addressing File System Objects](https://nix.dev/manual/nix/2.32/store/file-system-object/content-address)
  + [Content-Addressing Store Objects](https://nix.dev/manual/nix/2.32/store/store-object/content-address)
  + [content-addressing derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-content-addressing-derivation)

  Software Heritage's writing on [*Intrinsic and Extrinsic identifiers*](https://www.softwareheritage.org/2020/07/09/intrinsic-vs-extrinsic-identifiers) is also a good introduction to the value of content-addressing over other referencing schemes.

  Besides content addressing, the Nix store also uses [input addressing](https://nix.dev/manual/nix/2.32/glossary#gloss-input-addressed-store-object).
* [content-addressed storage](https://nix.dev/manual/nix/2.32/glossary#gloss-content-addressed-store)

  The industry term for storage and retrieval systems using [content addressing](https://nix.dev/manual/nix/2.32/glossary#gloss-content-address). A Nix store also has [input addressing](https://nix.dev/manual/nix/2.32/glossary#gloss-input-addressed-store-object), and metadata.
* [derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-derivation)

  A derivation can be thought of as a [pure function](https://en.wikipedia.org/wiki/Pure_function) that produces new [store objects](https://nix.dev/manual/nix/2.32/glossary#gloss-store-object) from existing store objects.

  Derivations are implemented as [operating system processes that run in a sandbox](https://nix.dev/manual/nix/2.32/store/building#builder-execution).
  This sandbox by default only allows reading from store objects specified as inputs, and only allows writing to designated [outputs](https://nix.dev/manual/nix/2.32/glossary#gloss-output) to be [captured as store objects](https://nix.dev/manual/nix/2.32/store/building#processing-outputs).

  A derivation is typically specified as a [derivation expression](https://nix.dev/manual/nix/2.32/glossary#gloss-derivation-expression) in the [Nix language](https://nix.dev/manual/nix/2.32/language/), and [instantiated](https://nix.dev/manual/nix/2.32/glossary#gloss-instantiate) to a [store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation).
  There are multiple ways of obtaining store objects from store derivatons, collectively called [realisation](https://nix.dev/manual/nix/2.32/glossary#gloss-realise).
* [store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation)

  A [derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-derivation) represented as a [store object](https://nix.dev/manual/nix/2.32/glossary#gloss-store-object).

  See [Store Derivation](https://nix.dev/manual/nix/2.32/store/derivation/#store-derivation) for details.
* [directed acyclic graph](https://nix.dev/manual/nix/2.32/glossary#gloss-directed-acyclic-graph)

  A [directed acyclic graph](https://en.wikipedia.org/wiki/Directed_acyclic_graph) (DAG) is graph whose edges are given a direction ("a to b" is not the same edge as "b to a"), and for which no possible path (created by joining together edges) forms a cycle.

  DAGs are very important to Nix.
  In particular, the non-self-[references](https://nix.dev/manual/nix/2.32/glossary#gloss-reference) of [store object](https://nix.dev/manual/nix/2.32/glossary#gloss-store-object) form a cycle.
* [derivation path](https://nix.dev/manual/nix/2.32/glossary#gloss-derivation-path)

  A [store path](https://nix.dev/manual/nix/2.32/glossary#gloss-store-path) which uniquely identifies a [store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation).

  See [Referencing Store Derivations](https://nix.dev/manual/nix/2.32/store/derivation/#derivation-path) for details.

  Not to be confused with [deriving path].
* [derivation expression](https://nix.dev/manual/nix/2.32/glossary#gloss-derivation-expression)

  A description of a [store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation) using the [`derivation` primitive](https://nix.dev/manual/nix/2.32/language/derivations) in the [Nix language](https://nix.dev/manual/nix/2.32/language/).
* [instantiate](https://nix.dev/manual/nix/2.32/glossary#gloss-instantiate), instantiation

  Translate a [derivation expression](https://nix.dev/manual/nix/2.32/glossary#gloss-derivation-expression) into a [store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation).

  See [`nix-instantiate`](https://nix.dev/manual/nix/2.32/command-ref/nix-instantiate), which produces a store derivation from a Nix expression that evaluates to a derivation.
* [realise](https://nix.dev/manual/nix/2.32/glossary#gloss-realise), realisation

  Ensure a [store path](https://nix.dev/manual/nix/2.32/glossary#gloss-store-path) is [valid](https://nix.dev/manual/nix/2.32/glossary#gloss-validity).

  This can be achieved by:

  + Fetching a pre-built [store object](https://nix.dev/manual/nix/2.32/glossary#gloss-store-object) from a [substituter](https://nix.dev/manual/nix/2.32/glossary#gloss-substituter)
  + [Building](https://nix.dev/manual/nix/2.32/store/building) the corresponding [store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation)
  + Delegating to a [remote machine](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-builders) and retrieving the outputs

  See [`nix-store --realise`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/realise) for a detailed description of the algorithm.

  See also [`nix-build`](https://nix.dev/manual/nix/2.32/command-ref/nix-build) and [`nix build`](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-build) (experimental).
* [content-addressing derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-content-addressing-derivation)

  A derivation which has the
  [`__contentAddressed`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-__contentAddressed)
  attribute set to `true`.
* [fixed-output derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-fixed-output-derivation) (FOD)

  A [store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation) where a cryptographic hash of the [output](https://nix.dev/manual/nix/2.32/glossary#gloss-output) is determined in advance using the [`outputHash`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-outputHash) attribute, and where the [`builder`](https://nix.dev/manual/nix/2.32/language/derivations#attr-builder) executable has access to the network.
* [store](https://nix.dev/manual/nix/2.32/glossary#gloss-store)

  A collection of [store objects](https://nix.dev/manual/nix/2.32/glossary#gloss-store-object), with operations to manipulate that collection.
  See [Nix Store](https://nix.dev/manual/nix/2.32/store/) for details.

  There are many types of stores, see [Store Types](https://nix.dev/manual/nix/2.32/store/types/) for details.
* [Nix instance](https://nix.dev/manual/nix/2.32/glossary#gloss-nix-instance)

  1. An installation of Nix, which includes the presence of a [store](https://nix.dev/manual/nix/2.32/glossary#gloss-store), and the Nix package manager which operates on that store.
     A local Nix installation and a [remote builder](https://nix.dev/manual/nix/2.32/advanced-topics/distributed-builds) are two examples of Nix instances.
  2. A running Nix process, such as the `nix` command.
* [binary cache](https://nix.dev/manual/nix/2.32/glossary#gloss-binary-cache)

  A *binary cache* is a Nix store which uses a different format: its
  metadata and signatures are kept in `.narinfo` files rather than in a
  [Nix database](https://nix.dev/manual/nix/2.32/glossary#gloss-nix-database). This different format simplifies serving store objects
  over the network, but cannot host builds. Examples of binary caches
  include S3 buckets and the [NixOS binary cache](https://cache.nixos.org).
* [store path](https://nix.dev/manual/nix/2.32/glossary#gloss-store-path)

  The location of a [store object](https://nix.dev/manual/nix/2.32/glossary#gloss-store-object) in the file system, i.e., an immediate child of the Nix store directory.

  > **Example**
  >
  > `/nix/store/a040m110amc4h71lds2jmr8qrkj2jhxd-git-2.38.1`

  See [Store Path](https://nix.dev/manual/nix/2.32/store/store-path) for details.
* [file system object](https://nix.dev/manual/nix/2.32/glossary#gloss-file-system-object)

  The Nix data model for representing simplified file system data.

  See [File System Object](https://nix.dev/manual/nix/2.32/store/file-system-object) for details.
* [store object](https://nix.dev/manual/nix/2.32/glossary#gloss-store-object)

  Part of the contents of a [store](https://nix.dev/manual/nix/2.32/glossary#gloss-store).

  A store object consists of a [file system object](https://nix.dev/manual/nix/2.32/glossary#gloss-file-system-object), [references](https://nix.dev/manual/nix/2.32/glossary#gloss-reference) to other store objects, and other metadata.
  It can be referred to by a [store path](https://nix.dev/manual/nix/2.32/glossary#gloss-store-path).

  See [Store Object](https://nix.dev/manual/nix/2.32/store/store-object) for details.
* [IFD](https://nix.dev/manual/nix/2.32/glossary#gloss-ifd)

  [Import From Derivation](https://nix.dev/manual/nix/2.32/language/import-from-derivation)
* [input-addressed store object](https://nix.dev/manual/nix/2.32/glossary#gloss-input-addressed-store-object)

  A store object produced by building a
  non-[content-addressed](https://nix.dev/manual/nix/2.32/glossary#gloss-content-addressing-derivation),
  non-[fixed-output](https://nix.dev/manual/nix/2.32/glossary#gloss-fixed-output-derivation)
  derivation.

  See [input-addressing derivation outputs](https://nix.dev/manual/nix/2.32/store/derivation/outputs/input-address) for details.
* [content-addressed store object](https://nix.dev/manual/nix/2.32/glossary#gloss-content-addressed-store-object)

  A [store object](https://nix.dev/manual/nix/2.32/glossary#gloss-store-object) which is [content-addressed](https://nix.dev/manual/nix/2.32/glossary#gloss-content-address),
  i.e. whose [store path](https://nix.dev/manual/nix/2.32/glossary#gloss-store-path) is determined by its contents.
  This includes derivations, the outputs of [content-addressing derivations](https://nix.dev/manual/nix/2.32/glossary#gloss-content-addressing-derivation), and the outputs of [fixed-output derivations](https://nix.dev/manual/nix/2.32/glossary#gloss-fixed-output-derivation).

  See [Content-Addressing Store Objects](https://nix.dev/manual/nix/2.32/store/store-object/content-address) for details.
* [substitute](https://nix.dev/manual/nix/2.32/glossary#gloss-substitute)

  A substitute is a command invocation stored in the [Nix database](https://nix.dev/manual/nix/2.32/glossary#gloss-nix-database) that
  describes how to build a store object, bypassing the normal build
  mechanism (i.e., derivations). Typically, the substitute builds the
  store object by downloading a pre-built version of the store object
  from some server.
* [substituter](https://nix.dev/manual/nix/2.32/glossary#gloss-substituter)

  An additional [store](https://nix.dev/manual/nix/2.32/glossary#gloss-store) from which Nix can obtain store objects instead of building them.
  Often the substituter is a [binary cache](https://nix.dev/manual/nix/2.32/glossary#gloss-binary-cache), but any store can serve as substituter.

  See the [`substituters` configuration option](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-substituters) for details.
* [purity](https://nix.dev/manual/nix/2.32/glossary#gloss-purity)

  The assumption that equal Nix derivations when run always produce
  the same output. This cannot be guaranteed in general (e.g., a
  builder can rely on external inputs such as the network or the
  system time) but the Nix model assumes it.
* [impure derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-impure-derivation)

  [An experimental feature](https://nix.dev/manual/nix/2.32/glossary#./development/experimental-features.md#xp-feature-impure-derivations) that allows derivations to be explicitly marked as impure,
  so that they are always rebuilt, and their outputs not reused by subsequent calls to realise them.
* [Nix database](https://nix.dev/manual/nix/2.32/glossary#gloss-nix-database)

  An SQlite database to track [reference](https://nix.dev/manual/nix/2.32/glossary#gloss-reference)s between [store object](https://nix.dev/manual/nix/2.32/glossary#gloss-store-object)s.
  This is an implementation detail of the [local store](https://nix.dev/manual/nix/2.32/store/types/local-store).

  Default location: `/nix/var/nix/db`.
* [Nix expression](https://nix.dev/manual/nix/2.32/glossary#gloss-nix-expression)

  A syntactically valid use of the [Nix language](https://nix.dev/manual/nix/2.32/language/).

  > **Example**
  >
  > The contents of a `.nix` file form a Nix expression.

  Nix expressions specify [derivation expressions](https://nix.dev/manual/nix/2.32/glossary#gloss-derivation-expression), which are [instantiated](https://nix.dev/manual/nix/2.32/glossary#gloss-instantiate) into the Nix store as [store derivations](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation).
  These derivations can then be [realised](https://nix.dev/manual/nix/2.32/glossary#gloss-realise) to produce [outputs](https://nix.dev/manual/nix/2.32/glossary#gloss-output).

  > **Example**
  >
  > Building and deploying software using Nix entails writing Nix expressions to describe [packages](https://nix.dev/manual/nix/2.32/glossary#package) and compositions thereof.
* [reference](https://nix.dev/manual/nix/2.32/glossary#gloss-reference)

  An edge from one [store object](https://nix.dev/manual/nix/2.32/glossary#gloss-store-object) to another.

  See [References](https://nix.dev/manual/nix/2.32/store/store-object#references) for details.

  See [References](https://nix.dev/manual/nix/2.32/store/store-object#references) for details.
* [reachable](https://nix.dev/manual/nix/2.32/glossary#gloss-reachable)

  A store path `Q` is reachable from another store path `P` if `Q`
  is in the *closure* of the *references* relation.

  See [References](https://nix.dev/manual/nix/2.32/store/store-object#references) for details.
* [closure](https://nix.dev/manual/nix/2.32/glossary#gloss-closure)

  The closure of a store path is the set of store paths that are
  directly or indirectly “reachable” from that store path; that is,
  it’s the closure of the path under the *references* relation. For
  a package, the closure of its derivation is equivalent to the
  build-time dependencies, while the closure of its [output path](https://nix.dev/manual/nix/2.32/glossary#gloss-output-path) is
  equivalent to its runtime dependencies. For correct deployment it
  is necessary to deploy whole closures, since otherwise at runtime
  files could be missing. The command `nix-store --query --requisites`  prints out
  closures of store paths.

  As an example, if the [store object](https://nix.dev/manual/nix/2.32/glossary#gloss-store-object) at path `P` contains a [reference](https://nix.dev/manual/nix/2.32/glossary#gloss-reference)
  to a store object at path `Q`, then `Q` is in the closure of `P`. Further, if `Q`
  references `R` then `R` is also in the closure of `P`.

  See [References](https://nix.dev/manual/nix/2.32/store/store-object#references) for details.
* [requisite](https://nix.dev/manual/nix/2.32/glossary#gloss-requisite)

  A store object [reachable] by a path (chain of references) from a given [store object](https://nix.dev/manual/nix/2.32/glossary#gloss-store-object).
  The [closure](https://nix.dev/manual/nix/2.32/glossary#gloss-closure) is the set of requisites.

  See [References](https://nix.dev/manual/nix/2.32/store/store-object#references) for details.
* [referrer](https://nix.dev/manual/nix/2.32/glossary#gloss-reference)

  A reversed edge from one [store object](https://nix.dev/manual/nix/2.32/glossary#gloss-store-object) to another.
* [output](https://nix.dev/manual/nix/2.32/glossary#gloss-output)

  A [store object](https://nix.dev/manual/nix/2.32/glossary#gloss-store-object) produced by a [store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation).
  See [the `outputs` argument to the `derivation` function](https://nix.dev/manual/nix/2.32/language/derivations#attr-outputs) for details.
* [output path](https://nix.dev/manual/nix/2.32/glossary#gloss-output-path)

  The [store path](https://nix.dev/manual/nix/2.32/glossary#gloss-store-path) to the [output](https://nix.dev/manual/nix/2.32/glossary#gloss-output) of a [store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation).
* [output closure](https://nix.dev/manual/nix/2.32/glossary#gloss-output-closure)  
  The [closure](https://nix.dev/manual/nix/2.32/glossary#gloss-closure) of an [output path](https://nix.dev/manual/nix/2.32/glossary#gloss-output-path). It only contains what is [reachable] from the output.
* [deriving path](https://nix.dev/manual/nix/2.32/glossary#gloss-deriving-path)

  Deriving paths are a way to refer to [store objects](https://nix.dev/manual/nix/2.32/glossary#gloss-store-object) that might not yet be [realised](https://nix.dev/manual/nix/2.32/glossary#gloss-realise).

  See [Deriving Path](https://nix.dev/manual/nix/2.32/store/derivation/#deriving-path) for details.

  Not to be confused with [derivation path](https://nix.dev/manual/nix/2.32/glossary#gloss-derivation-path).
* [deriver](https://nix.dev/manual/nix/2.32/glossary#gloss-deriver)

  The [store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation) that produced an [output path](https://nix.dev/manual/nix/2.32/glossary#gloss-output-path).

  The deriver for an output path can be queried with the `--deriver` option to
  [`nix-store --query`](https://nix.dev/manual/nix/2.32/command-ref/nix-store/query).
* [validity](https://nix.dev/manual/nix/2.32/glossary#gloss-validity)

  A store path is valid if all [store object](https://nix.dev/manual/nix/2.32/glossary#gloss-store-object)s in its [closure](https://nix.dev/manual/nix/2.32/glossary#gloss-closure) can be read from the [store](https://nix.dev/manual/nix/2.32/glossary#gloss-store).

  For a [local store](https://nix.dev/manual/nix/2.32/store/types/local-store), this means:

  + The store path leads to an existing [store object](https://nix.dev/manual/nix/2.32/glossary#gloss-store-object) in that [store](https://nix.dev/manual/nix/2.32/glossary#gloss-store).
  + The store path is listed in the [Nix database](https://nix.dev/manual/nix/2.32/glossary#gloss-nix-database) as being valid.
  + All paths in the store path's [closure](https://nix.dev/manual/nix/2.32/glossary#gloss-closure) are valid.
* [user environment](https://nix.dev/manual/nix/2.32/glossary#gloss-user-env)

  An automatically generated store object that consists of a set of
  symlinks to “active” applications, i.e., other store paths. These
  are generated automatically by
  [`nix-env`](https://nix.dev/manual/nix/2.32/command-ref/nix-env). See *profiles*.
* [profile](https://nix.dev/manual/nix/2.32/glossary#gloss-profile)

  A symlink to the current *user environment* of a user, e.g.,
  `/nix/var/nix/profiles/default`.
* [installable](https://nix.dev/manual/nix/2.32/glossary#gloss-installable)

  Something that can be realised in the Nix store.

  See [installables](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix#installables) for [`nix` commands](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix) (experimental) for details.
* [Nix Archive (NAR)](https://nix.dev/manual/nix/2.32/glossary#gloss-nar)

  A *N*ix *AR*chive. This is a serialisation of a path in the Nix
  store. It can contain regular files, directories and symbolic
  links. NARs are generated and unpacked using `nix-store --dump`
  and `nix-store --restore`.

  See [Nix Archive](https://nix.dev/manual/nix/2.32/store/file-system-object/content-address#serial-nix-archive) for details.
* [`∅`](https://nix.dev/manual/nix/2.32/glossary#gloss-empty-set)

  The empty set symbol. In the context of profile history, this denotes a package is not present in a particular version of the profile.
* [`ε`](https://nix.dev/manual/nix/2.32/glossary#gloss-epsilon)

  The epsilon symbol. In the context of a package, this means the version is empty. More precisely, the derivation does not have a version attribute.
* [package](https://nix.dev/manual/nix/2.32/glossary#package)

  A software package; files that belong together for a particular purpose, and metadata.

  Nix represents files as [file system objects](https://nix.dev/manual/nix/2.32/glossary#gloss-file-system-object), and how they belong together is encoded as [references](https://nix.dev/manual/nix/2.32/glossary#gloss-reference) between [store objects](https://nix.dev/manual/nix/2.32/glossary#gloss-store-object) that contain these file system objects.

  The [Nix language](https://nix.dev/manual/nix/2.32/language/) allows denoting packages in terms of [attribute sets](https://nix.dev/manual/nix/2.32/language/types#attribute-set) containing:

  + attributes that refer to the files of a package, typically in the form of [derivation outputs](https://nix.dev/manual/nix/2.32/glossary#output),
  + attributes with metadata, such as information about how the package is supposed to be used.

  The exact shape of these attribute sets is up to convention.
* [string interpolation](https://nix.dev/manual/nix/2.32/glossary#gloss-string-interpolation)

  Expanding expressions enclosed in `${ }` within a [string](https://nix.dev/manual/nix/2.32/language/types#type-string), [path](https://nix.dev/manual/nix/2.32/language/types#type-path), or [attribute name](https://nix.dev/manual/nix/2.32/language/types#attribute-set).

  See [String interpolation](https://nix.dev/manual/nix/2.32/language/string-interpolation) for details.
* [base directory](https://nix.dev/manual/nix/2.32/glossary#gloss-base-directory)

  The location from which relative paths are resolved.

  + For expressions in a file, the base directory is the directory containing that file.
    This is analogous to the directory of a [base URL](https://datatracker.ietf.org/doc/html/rfc1808#section-3.3).
  + For expressions written in command line arguments with [`--expr`](https://nix.dev/manual/nix/2.32/command-ref/opt-common#opt-expr), the base directory is the current working directory.
* [experimental feature](https://nix.dev/manual/nix/2.32/glossary#gloss-experimental-feature)

  Not yet stabilized functionality guarded by named experimental feature flags.
  These flags are enabled or disabled with the [`experimental-features`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-experimental-features) setting.

  See the contribution guide on the [purpose and lifecycle of experimental feaures](https://nix.dev/manual/nix/2.32/development/experimental-features).