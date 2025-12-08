---
url: https://nix.dev/manual/nix/2.32/language/string-context
title: String context - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# String context - Nix 2.32.2 Reference Manual

# [String context](https://nix.dev/manual/nix/2.32/language/string-context#string-context)

> **Note**
>
> This is an advanced topic.
> The Nix language is designed to be used without the programmer consciously dealing with string contexts or even knowing what they are.

A string in the Nix language is not just a sequence of characters like strings in other languages.
It is actually a pair of a sequence of characters and a *string context*.
The string context is an (unordered) set of *string context elements*.

The purpose of string contexts is to collect non-string values attached to strings via
[string concatenation](https://nix.dev/manual/nix/2.32/language/operators#string-concatenation),
[string interpolation](https://nix.dev/manual/nix/2.32/language/string-interpolation),
and similar operations.
The idea is that a user can reference other files when creating text files through Nix expressions, without manually keeping track of the exact paths.
Nix will ensure that the all referenced files are accessible – that all [store paths](https://nix.dev/manual/nix/2.32/glossary#gloss-store-path) are [valid](https://nix.dev/manual/nix/2.32/glossary#gloss-validity).

> **Note**
>
> String contexts are *not* explicitly manipulated in idiomatic Nix language code.

String context elements come in different forms:

* [deriving path](https://nix.dev/manual/nix/2.32/language/string-context#string-context-element-derived-path)

  A string context element of this type is a [deriving path](https://nix.dev/manual/nix/2.32/glossary#gloss-deriving-path).
  They can be either of type [constant](https://nix.dev/manual/nix/2.32/language/string-context#string-context-constant) or [output](https://nix.dev/manual/nix/2.32/language/string-context#string-context-output), which correspond to the types of deriving paths.

  + [Constant string context elements](https://nix.dev/manual/nix/2.32/language/string-context#string-context-constant)

    > **Example**
    >
    > [`builtins.storePath`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-storePath) creates a string with a single constant string context element:
    >
    > ```
    > builtins.getContext (builtins.storePath "/nix/store/wkhdf9jinag5750mqlax6z2zbwhqb76n-hello-2.10")
    > ```
    >
    > evaluates to
    >
    > ```
    > {
    >   "/nix/store/wkhdf9jinag5750mqlax6z2zbwhqb76n-hello-2.10" = {
    >     path = true;
    >   };
    > }
    > ```
  + [Output string context elements](https://nix.dev/manual/nix/2.32/language/string-context#string-context-output)

    > **Example**
    >
    > The behavior of string contexts are best demonstrated with a built-in function that is still experimental: [`builtins.outputOf`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-outputOf).
    > This example will *not* work with stable Nix!
    >
    > ```
    > builtins.getContext
    >   (builtins.outputOf
    >     (builtins.storePath "/nix/store/fvchh9cvcr7kdla6n860hshchsba305w-hello-2.12.drv")
    >     "out")
    > ```
    >
    > evaluates to
    >
    > ```
    > {
    >   "/nix/store/fvchh9cvcr7kdla6n860hshchsba305w-hello-2.12.drv" = {
    >     outputs = [ "out" ];
    >   };
    > }
    > ```
* [*derivation deep*](https://nix.dev/manual/nix/2.32/language/string-context#string-context-element-derivation-deep)

  *derivation deep* is an advanced feature intended to be used with the
  [`exportReferencesGraph` derivation attribute](https://nix.dev/manual/nix/2.32/language/advanced-attributes#adv-attr-exportReferencesGraph).
  A *derivation deep* string context element is a derivation path, and refers to both its outputs and the entire build closure of that derivation:
  all its outputs, all the other derivations the given derivation depends on, and all the outputs of those.

  > **Example**
  >
  > The best way to illustrate *derivation deep* string contexts is with [`builtins.addDrvOutputDependencies`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-addDrvOutputDependencies).
  > Take a regular constant string context element pointing to a derivation, and transform it into a "Derivation deep" string context element.
  >
  > ```
  > builtins.getContext
  >   (builtins.addDrvOutputDependencies
  >     (builtins.storePath "/nix/store/fvchh9cvcr7kdla6n860hshchsba305w-hello-2.12.drv"))
  > ```
  >
  > evaluates to
  >
  > ```
  > {
  >   "/nix/store/fvchh9cvcr7kdla6n860hshchsba305w-hello-2.12.drv" = {
  >     allOutputs = true;
  >   };
  > }
  > ```

## [Inspecting string contexts](https://nix.dev/manual/nix/2.32/language/string-context#inspecting-string-contexts)

Most basically, [`builtins.hasContext`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-hasContext) will tell whether a string has a non-empty context.

When more granular information is needed, [`builtins.getContext`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-getContext) can be used.
It creates an [attribute set](https://nix.dev/manual/nix/2.32/language/types#attribute-set) representing the string context, which can be inspected as usual.

## [Clearing string contexts](https://nix.dev/manual/nix/2.32/language/string-context#clearing-string-contexts)

[`builtins.unsafeDiscardStringContext`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-unsafeDiscardStringContext) will make a copy of a string, but with an empty string context.
The returned string can be used in more ways, e.g. by operators that require the string context to be empty.
The requirement to explicitly discard the string context in such use cases helps ensure that string context elements are not lost by mistake.
The "unsafe" marker is only there to remind that Nix normally guarantees that dependencies are tracked, whereas the returned string has lost them.

## [Constructing string contexts](https://nix.dev/manual/nix/2.32/language/string-context#constructing-string-contexts)

[`builtins.appendContext`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-appendContext) will create a copy of a string, but with additional string context elements.
The context is specified explicitly by an [attribute set](https://nix.dev/manual/nix/2.32/language/types#attribute-set) in the format that [`builtins.hasContext`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-hasContext) produces.
A string with arbitrary contexts can be made like this:

1. Create a string with the desired string context elements.
   (The contents of the string do not matter.)
2. Dump its context with [`builtins.getContext`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-getContext).
3. Combine it with a base string and repeated [`builtins.appendContext`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-appendContext) calls.