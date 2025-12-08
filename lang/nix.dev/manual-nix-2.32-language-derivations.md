---
url: https://nix.dev/manual/nix/2.32/language/derivations
title: Derivations - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Derivations - Nix 2.32.2 Reference Manual

# [Derivations](https://nix.dev/manual/nix/2.32/language/derivations#derivations)

The most important built-in function is `derivation`, which is used to describe a single store-layer [store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation).
Consult the [store chapter](https://nix.dev/manual/nix/2.32/store/derivation/) for what a store derivation is;
this section just concerns how to create one from the Nix language.

This builtin function takes as input an attribute set, the attributes of which specify the inputs to the process.
It outputs an attribute set, and produces a [store derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-store-derivation) as a side effect of evaluation.

## [Input attributes](https://nix.dev/manual/nix/2.32/language/derivations#input-attributes)

### [Required](https://nix.dev/manual/nix/2.32/language/derivations#required)

* [`name`](https://nix.dev/manual/nix/2.32/language/derivations#attr-name) ([String](https://nix.dev/manual/nix/2.32/language/types#type-string))

  A symbolic name for the derivation.
  See [derivation outputs](https://nix.dev/manual/nix/2.32/store/derivation/#outputs) for what this is affects.

  > **Example**
  >
  > ```
  > derivation {
  >   name = "hello";
  >   # ...
  > }
  > ```
  >
  > The derivation's path will be `/nix/store/<hash>-hello.drv`.
  > The [output](https://nix.dev/manual/nix/2.32/language/derivations#attr-outputs) paths will be of the form `/nix/store/<hash>-hello[-<output>]`
* [`system`](https://nix.dev/manual/nix/2.32/language/derivations#attr-system) ([String](https://nix.dev/manual/nix/2.32/language/types#type-string))

  See [system](https://nix.dev/manual/nix/2.32/store/derivation/#system).

  > **Example**
  >
  > Declare a derivation to be built on a specific system type:
  >
  > ```
  > derivation {
  >   # ...
  >   system = "x86_64-linux";
  >   # ...
  > }
  > ```

  > **Example**
  >
  > Declare a derivation to be built on the system type that evaluates the expression:
  >
  > ```
  > derivation {
  >   # ...
  >   system = builtins.currentSystem;
  >   # ...
  > }
  > ```
  >
  > [`builtins.currentSystem`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-currentSystem) has the value of the [`system` configuration option], and defaults to the system type of the current Nix installation.
* [`builder`](https://nix.dev/manual/nix/2.32/language/derivations#attr-builder) ([Path](https://nix.dev/manual/nix/2.32/language/types#type-path) | [String](https://nix.dev/manual/nix/2.32/language/types#type-string))

  See [builder](https://nix.dev/manual/nix/2.32/store/derivation/#builder).

  > **Example**
  >
  > Use the file located at `/bin/bash` as the builder executable:
  >
  > ```
  > derivation {
  >   # ...
  >   builder = "/bin/bash";
  >   # ...
  > };
  > ```

  > **Example**
  >
  > Copy a local file to the Nix store for use as the builder executable:
  >
  > ```
  > derivation {
  >   # ...
  >   builder = ./builder.sh;
  >   # ...
  > };
  > ```

  > **Example**
  >
  > Use a file from another derivation as the builder executable:
  >
  > ```
  > let pkgs = import <nixpkgs> {}; in
  > derivation {
  >   # ...
  >   builder = "${pkgs.python}/bin/python";
  >   # ...
  > };
  > ```

### [Optional](https://nix.dev/manual/nix/2.32/language/derivations#optional)

* [`args`](https://nix.dev/manual/nix/2.32/language/derivations#attr-args) ([List](https://nix.dev/manual/nix/2.32/language/types#type-list) of [String](https://nix.dev/manual/nix/2.32/language/types#type-string))

  Default: `[ ]`

  See [args](https://nix.dev/manual/nix/2.32/store/derivation/#args).

  > **Example**
  >
  > Pass arguments to Bash to interpret a shell command:
  >
  > ```
  > derivation {
  >   # ...
  >   builder = "/bin/bash";
  >   args = [ "-c" "echo hello world > $out" ];
  >   # ...
  > };
  > ```
* [`outputs`](https://nix.dev/manual/nix/2.32/language/derivations#attr-outputs) ([List](https://nix.dev/manual/nix/2.32/language/types#type-list) of [String](https://nix.dev/manual/nix/2.32/language/types#type-string))

  Default: `[ "out" ]`

  Symbolic outputs of the derivation.
  Each output name is passed to the [`builder`](https://nix.dev/manual/nix/2.32/language/derivations#attr-builder) executable as an environment variable with its value set to the corresponding [store path](https://nix.dev/manual/nix/2.32/store/store-path).

  By default, a derivation produces a single output called `out`.
  However, derivations can produce multiple outputs.
  This allows the associated [store objects](https://nix.dev/manual/nix/2.32/store/store-object) and their [closures](https://nix.dev/manual/nix/2.32/glossary#gloss-closure) to be copied or garbage-collected separately.

  > **Example**
  >
  > Imagine a library package that provides a dynamic library, header files, and documentation.
  > A program that links against such a library doesn’t need the header files and documentation at runtime, and it doesn’t need the documentation at build time.
  > Thus, the library package could specify:
  >
  > ```
  > derivation {
  >   # ...
  >   outputs = [ "lib" "dev" "doc" ];
  >   # ...
  > }
  > ```
  >
  > This will cause Nix to pass environment variables `lib`, `dev`, and `doc` to the builder containing the intended store paths of each output.
  > The builder would typically do something like
  >
  > ```
  > ./configure \
  >   --libdir=$lib/lib \
  >   --includedir=$dev/include \
  >   --docdir=$doc/share/doc
  > ```
  >
  > for an Autoconf-style package.

  The name of an output is combined with the name of the derivation to create the name part of the output's store path, unless it is `out`, in which case just the name of the derivation is used.

  > **Example**
  >
  > ```
  > derivation {
  >   name = "example";
  >   outputs = [ "lib" "dev" "doc" "out" ];
  >   # ...
  > }
  > ```
  >
  > The store derivation path will be `/nix/store/<hash>-example.drv`.
  > The output paths will be
  >
  > + `/nix/store/<hash>-example-lib`
  > + `/nix/store/<hash>-example-dev`
  > + `/nix/store/<hash>-example-doc`
  > + `/nix/store/<hash>-example`

  You can refer to each output of a derivation by selecting it as an attribute.
  The first element of `outputs` determines the *default output* and ends up at the top-level.

  > **Example**
  >
  > Select an output by attribute name:
  >
  > ```
  > let
  >   myPackage = derivation {
  >     name = "example";
  >     outputs = [ "lib" "dev" "doc" "out" ];
  >     # ...
  >   };
  > in myPackage.dev
  > ```
  >
  > Since `lib` is the first output, `myPackage` is equivalent to `myPackage.lib`.
* See [Advanced Attributes](https://nix.dev/manual/nix/2.32/language/advanced-attributes) for more, infrequently used, optional attributes.
* Every other attribute is passed as an environment variable to the builder.
  Attribute values are translated to environment variables as follows:

  + Strings are passed unchanged.
  + Integral numbers are converted to decimal notation.
  + Floating point numbers are converted to simple decimal or scientific notation with a preset precision.
  + A *path* (e.g., `../foo/sources.tar`) causes the referenced file
    to be copied to the store; its location in the store is put in
    the environment variable. The idea is that all sources should
    reside in the Nix store, since all inputs to a derivation should
    reside in the Nix store.
  + A *derivation* causes that derivation to be built prior to the
    present derivation. The environment variable is set to the [store path](https://nix.dev/manual/nix/2.32/store/store-path) of the derivation's default [output](https://nix.dev/manual/nix/2.32/language/derivations#attr-outputs).
  + Lists of the previous types are also allowed. They are simply
    concatenated, separated by spaces.
  + `true` is passed as the string `1`, `false` and `null` are
    passed as an empty string.