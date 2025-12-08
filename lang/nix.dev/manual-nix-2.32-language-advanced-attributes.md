---
url: https://nix.dev/manual/nix/2.32/language/advanced-attributes
title: Advanced Attributes - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Advanced Attributes - Nix 2.32.2 Reference Manual

# [Advanced Attributes](https://nix.dev/manual/nix/2.32/language/advanced-attributes#advanced-attributes)

Derivations can declare some infrequently used optional attributes.

## [Inputs](https://nix.dev/manual/nix/2.32/language/advanced-attributes#inputs)

* [`exportReferencesGraph`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-exportReferencesGraph)  
  This attribute allows builders access to the references graph of
  their inputs. The attribute is a list of inputs in the Nix store
  whose references graph the builder needs to know. The value of
  this attribute should be a list of pairs `[ name1 path1 name2 path2 ... ]`. The references graph of each *pathN* will be stored
  in a text file *nameN* in the temporary build directory. The text
  files have the format used by `nix-store --register-validity`
  (with the deriver fields left empty). For example, when the
  following derivation is built:

  ```
  derivation {
    ...
    exportReferencesGraph = [ "libfoo-graph" libfoo ];
  };
  ```

  the references graph of `libfoo` is placed in the file
  `libfoo-graph` in the temporary build directory.

  `exportReferencesGraph` is useful for builders that want to do
  something with the closure of a store path. Examples include the
  builders in NixOS that generate the initial ramdisk for booting
  Linux (a `cpio` archive containing the closure of the boot script)
  and the ISO-9660 image for the installation CD (which is populated
  with a Nix store containing the closure of a bootable NixOS
  configuration).
* [`passAsFile`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-passAsFile)  
  A list of names of attributes that should be passed via files rather
  than environment variables. For example, if you have

  ```
  passAsFile = ["big"];
  big = "a very long string";
  ```

  then when the builder runs, the environment variable `bigPath`
  will contain the absolute path to a temporary file containing `a very long string`. That is, for any attribute *x* listed in
  `passAsFile`, Nix will pass an environment variable `xPath`
  holding the path of the file containing the value of attribute
  *x*. This is useful when you need to pass large strings to a
  builder, since most operating systems impose a limit on the size
  of the environment (typically, a few hundred kilobyte).
* [`__structuredAttrs`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-structuredAttrs)  
  If the special attribute `__structuredAttrs` is set to `true`, the other derivation
  attributes are serialised into a file in JSON format.

  This obviates the need for [`passAsFile`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-passAsFile) since JSON files have no size restrictions, unlike process environments.
  It also makes it possible to tweak derivation settings in a structured way;
  see [`outputChecks`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-outputChecks) for example.

  See the [corresponding section in the derivation page](https://nix.dev/manual/nix/2.32/store/derivation/#structured-attrs) for further details.

  > **Warning**
  >
  > If set to `true`, other advanced attributes such as [`allowedReferences`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-allowedReferences), [`allowedRequisites`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-allowedRequisites),
  > [`disallowedReferences`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-disallowedReferences) and [`disallowedRequisites`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-disallowedRequisites), maxSize, and maxClosureSize.
  > will have no effect.

## [Output checks](https://nix.dev/manual/nix/2.32/language/advanced-attributes#output-checks)

See the [corresponding section in the derivation output page](https://nix.dev/manual/nix/2.32/store/derivation/outputs/).

* [`allowedReferences`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-allowedReferences)  
  The optional attribute `allowedReferences` specifies a list of legal
  references (dependencies) of the output of the builder. For example,

  ```
  allowedReferences = [];
  ```

  enforces that the output of a derivation cannot have any runtime
  dependencies on its inputs. To allow an output to have a runtime
  dependency on itself, use `"out"` as a list item. This is used in
  NixOS to check that generated files such as initial ramdisks for
  booting Linux don’t have accidental dependencies on other paths in
  the Nix store.
* [`allowedRequisites`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-allowedRequisites)  
  This attribute is similar to `allowedReferences`, but it specifies
  the legal requisites of the whole closure, so all the dependencies
  recursively. For example,

  ```
  allowedRequisites = [ foobar ];
  ```

  enforces that the output of a derivation cannot have any other
  runtime dependency than `foobar`, and in addition it enforces that
  `foobar` itself doesn't introduce any other dependency itself.
* [`disallowedReferences`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-disallowedReferences)  
  The optional attribute `disallowedReferences` specifies a list of
  illegal references (dependencies) of the output of the builder. For
  example,

  ```
  disallowedReferences = [ foo ];
  ```

  enforces that the output of a derivation cannot have a direct
  runtime dependencies on the derivation `foo`.
* [`disallowedRequisites`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-disallowedRequisites)  
  This attribute is similar to `disallowedReferences`, but it
  specifies illegal requisites for the whole closure, so all the
  dependencies recursively. For example,

  ```
  disallowedRequisites = [ foobar ];
  ```

  enforces that the output of a derivation cannot have any runtime
  dependency on `foobar` or any other derivation depending recursively
  on `foobar`.
* [`outputChecks`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-outputChecks)  
  When using [structured attributes](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-structuredAttrs), the `outputChecks`
  attribute allows defining checks per-output.

  In addition to
  [`allowedReferences`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-allowedReferences), [`allowedRequisites`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-allowedRequisites),
  [`disallowedReferences`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-disallowedReferences) and [`disallowedRequisites`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-disallowedRequisites),
  the following attributes are available:

  + `maxSize` defines the maximum size of the resulting [store object](https://nix.dev/manual/nix/2.32/store/store-object).
  + `maxClosureSize` defines the maximum size of the output's closure.
  + `ignoreSelfRefs` controls whether self-references should be considered when
    checking for allowed references/requisites.

  Example:

  ```
  __structuredAttrs = true;

  outputChecks.out = {
    # The closure of 'out' must not be larger than 256 MiB.
    maxClosureSize = 256 * 1024 * 1024;

    # It must not refer to the C compiler or to the 'dev' output.
    disallowedRequisites = [ stdenv.cc "dev" ];
  };

  outputChecks.dev = {
    # The 'dev' output must not be larger than 128 KiB.
    maxSize = 128 * 1024;
  };
  ```

## [Other output modifications](https://nix.dev/manual/nix/2.32/language/advanced-attributes#other-output-modifications)

* [`unsafeDiscardReferences`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-unsafeDiscardReferences)  
  When using [structured attributes](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-structuredAttrs), the
  attribute `unsafeDiscardReferences` is an attribute set with a boolean value for each output name.
  If set to `true`, it disables scanning the output for runtime dependencies.

  Example:

  ```
  __structuredAttrs = true;
  unsafeDiscardReferences.out = true;
  ```

  This is useful, for example, when generating self-contained filesystem images with
  their own embedded Nix store: hashes found inside such an image refer
  to the embedded store and not to the host's Nix store.

## [Build scheduling](https://nix.dev/manual/nix/2.32/language/advanced-attributes#build-scheduling)

* [`preferLocalBuild`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-preferLocalBuild)  
  If this attribute is set to `true` and [distributed building is enabled](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-builders), then, if possible, the derivation will be built locally instead of being forwarded to a remote machine.
  This is useful for derivations that are cheapest to build locally.
* [`allowSubstitutes`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-allowSubstitutes)  
  If this attribute is set to `false`, then Nix will always build this derivation (locally or remotely); it will not try to substitute its outputs.
  This is useful for derivations that are cheaper to build than to substitute.

  This attribute can be ignored by setting [`always-allow-substitutes`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-always-allow-substitutes) to `true`.

  > **Note**
  >
  > If set to `false`, the [`builder`](https://nix.dev/manual/nix/2.32/language/derivations#attr-builder) should be able to run on the system type specified in the [`system` attribute](https://nix.dev/manual/nix/2.32/language/derivations#attr-system), since the derivation cannot be substituted.
* [`requiredSystemFeatures`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-requiredSystemFeatures)  
  If a derivation has the `requiredSystemFeatures` attribute, then Nix will only build it on a machine that has the corresponding features set in its [`system-features` configuration](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-system-features).

  For example, setting

  ```
  requiredSystemFeatures = [ "kvm" ];
  ```

  ensures that the derivation can only be built on a machine with the `kvm` feature.

# [Impure builder configuration](https://nix.dev/manual/nix/2.32/language/advanced-attributes#impure-builder-configuration)

* [`impureEnvVars`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-impureEnvVars)  
  This attribute allows you to specify a list of environment variables
  that should be passed from the environment of the calling user to
  the builder. Usually, the environment is cleared completely when the
  builder is executed, but with this attribute you can allow specific
  environment variables to be passed unmodified. For example,
  `fetchurl` in Nixpkgs has the line

  ```
  impureEnvVars = [ "http_proxy" "https_proxy" ... ];
  ```

  to make it use the proxy server configuration specified by the user
  in the environment variables `http_proxy` and friends.

  This attribute is only allowed in [fixed-output derivations](https://nix.dev/manual/nix/2.32/glossary#gloss-fixed-output-derivation),
  where impurities such as these are okay since (the hash
  of) the output is known in advance. It is ignored for all other
  derivations.

  > **Warning**
  >
  > `impureEnvVars` implementation takes environment variables from
  > the current builder process. When a daemon is building its
  > environmental variables are used. Without the daemon, the
  > environmental variables come from the environment of the
  > `nix-build`.

  If the [`configurable-impure-env` experimental
  feature](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-configurable-impure-env)
  is enabled, these environment variables can also be controlled
  through the
  [`impure-env`](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-impure-env)
  configuration setting.

## [Setting the derivation type](https://nix.dev/manual/nix/2.32/language/advanced-attributes#setting-the-derivation-type)

As discussed in [Derivation Outputs and Types of Derivations](https://nix.dev/manual/nix/2.32/store/derivation/outputs/), there are multiples kinds of derivations / kinds of derivation outputs.
The choice of the following attributes determines which kind of derivation we are making.

* [`__contentAddressed`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-__contentAddressed)
* [`outputHash`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-outputHash)
* [`outputHashAlgo`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-outputHashAlgo)
* [`outputHashMode`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-outputHashMode)

The three types of derivations are chosen based on the following combinations of these attributes.
All other combinations are invalid.

* [Input-addressing derivations](https://nix.dev/manual/nix/2.32/store/derivation/outputs/input-address)

  This is the default for `builtins.derivation`.
  Nix only currently supports one kind of input-addressing, so no other information is needed.

  `__contentAddressed = false;` may also be included, but is not needed, and will trigger the experimental feature check.
* [Fixed-output derivations](https://nix.dev/manual/nix/2.32/glossary#gloss-fixed-output-derivation)

  All of [`outputHash`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-outputHash), [`outputHashAlgo`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-outputHashAlgo), and [`outputHashMode`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-outputHashMode).
* [(Floating) content-addressing derivations](https://nix.dev/manual/nix/2.32/store/derivation/outputs/content-address)

  Both [`outputHashAlgo`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-outputHashAlgo) and [`outputHashMode`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-outputHashMode), `__contentAddressed = true;`, and *not* `outputHash`.

  If an output hash was given, then the derivation output would be "fixed" not "floating".

Here is more information on the `output*` attributes, and what values they may be set to:

* [`outputHashMode`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-outputHashMode)

  This specifies how the files of a content-addressing derivation output are digested to produce a content address.

  This works in conjunction with [`outputHashAlgo`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-outputHashAlgo).
  Specifying one without the other is an error (unless [`outputHash` is also specified and includes its own hash algorithm as described below).

  The `outputHashMode` attribute determines how the hash is computed.
  It must be one of the following values:

  + [`"flat"`](https://nix.dev/manual/nix/2.32/store/store-object/content-address#method-flat)

    This is the default.
  + [`"recursive"` or `"nar"`](https://nix.dev/manual/nix/2.32/store/store-object/content-address#method-nix-archive)

    > **Compatibility**
    >
    > `"recursive"` is the traditional way of indicating this,
    > and is supported since 2005 (virtually the entire history of Nix).
    > `"nar"` is more clear, and consistent with other parts of Nix (such as the CLI),
    > however support for it is only added in Nix version 2.21.
  + [`"text"`](https://nix.dev/manual/nix/2.32/store/store-object/content-address#method-text)

    > **Warning**
    >
    > The use of this method for derivation outputs is part of the [`dynamic-derivations`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-dynamic-derivations) experimental feature.
  + [`"git"`](https://nix.dev/manual/nix/2.32/store/store-object/content-address#method-git)

    > **Warning**
    >
    > This method is part of the [`git-hashing`](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-git-hashing) experimental feature.

  See [content-addressing store objects](https://nix.dev/manual/nix/2.32/store/store-object/content-address) for more information about the process this flag controls.
* [`outputHashAlgo`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-outputHashAlgo)

  This specifies the hash algorithm used to digest the [file system object](https://nix.dev/manual/nix/2.32/store/file-system-object) data of a content-addressing derivation output.

  This works in conjunction with [`outputHashMode`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-outputHashAlgo).
  Specifying one without the other is an error (unless `outputHash` is also specified and includes its own hash algorithm as described below).

  The `outputHashAlgo` attribute specifies the hash algorithm used to compute the hash.
  It can currently be `"blake3"`, `"sha1"`, `"sha256"`, `"sha512"`, or `null`.

  `outputHashAlgo` can only be `null` when `outputHash` follows the SRI format, because in that case the choice of hash algorithm is determined by `outputHash`.
* [`outputHash`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-outputHashAlgo); [`outputHash`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-outputHashMode)

  This will specify the output hash of the single output of a [fixed-output derivation](https://nix.dev/manual/nix/2.32/glossary#gloss-fixed-output-derivation).

  The `outputHash` attribute must be a string containing the hash in either hexadecimal or "nix32" encoding, or following the format for integrity metadata as defined by [SRI](https://www.w3.org/TR/SRI/).
  The "nix32" encoding is an adaptation of base-32 encoding.

  > **Note**
  >
  > The [`convertHash`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-convertHash) function shows how to convert between different encodings.
  > The [`nix-hash` command](https://nix.dev/manual/nix/2.32/command-ref/nix-hash) has information about obtaining the hash for some contents, as well as converting to and from encodings.
* [`__contentAddressed`](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-__contentAddressed)

  > **Warning**
  >
  > This attribute is part of an [experimental feature](https://nix.dev/manual/nix/2.32/development/experimental-features).
  >
  > To use this attribute, you must enable the
  > [`ca-derivations`][xp-feature-ca-derivations] experimental feature.
  > For example, in [nix.conf](https://nix.dev/manual/nix/2.32/command-ref/conf-file) you could add:
  >
  > ```
  > extra-experimental-features = ca-derivations
  > ```

  This is a boolean with a default of `false`.
  It determines whether the derivation is floating content-addressing.