---
url: https://nix.dev/manual/nix/2.32/language/
title: Nix Language - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Nix Language - Nix 2.32.2 Reference Manual

# [Nix Language](https://nix.dev/manual/nix/2.32/language/#nix-language)

The Nix language is designed for conveniently creating and composing [derivations](https://nix.dev/manual/nix/2.32/glossary#gloss-derivation) – precise descriptions of how contents of existing files are used to derive new files.

> **Tip**
>
> These pages are written as a reference.
> If you are learning Nix, nix.dev has a good [introduction to the Nix language](https://nix.dev/tutorials/nix-language).

The language is:

* *domain-specific*

  The Nix language is purpose-built for working with text files.
  Its most characteristic features are:

  + [File system path primitives](https://nix.dev/manual/nix/2.32/language/types#type-path), for accessing source files
  + [Indented strings](https://nix.dev/manual/nix/2.32/language/string-literals) and [string interpolation](https://nix.dev/manual/nix/2.32/language/string-interpolation), for creating file contents
  + [Strings with contexts](https://nix.dev/manual/nix/2.32/language/string-context), for transparently linking files

  It comes with [built-in functions](https://nix.dev/manual/nix/2.32/language/builtins) to integrate with the [Nix store](https://nix.dev/manual/nix/2.32/store/), which manages files and enables [realising](https://nix.dev/manual/nix/2.32/glossary#gloss-realise) derivations declared in the Nix language.
* *declarative*

  There is no notion of executing sequential steps.
  Dependencies between operations are established only through data.
* *pure*

  Values cannot change during computation.
  Functions always produce the same output if their input does not change.
* *functional*

  Functions are like any other value.
  Functions can be assigned to names, taken as arguments, or returned by functions.
* *lazy*

  Values are only computed when they are needed.
* *dynamically typed*

  Type errors are only detected when expressions are evaluated.

# [Overview](https://nix.dev/manual/nix/2.32/language/#overview)

This is an incomplete overview of language features, by example.

| Example | Description |
| --- | --- |
| *Basic values ([primitives](https://nix.dev/manual/nix/2.32/language/types#primitives))* |  |
| `"hello world"` | A [string](https://nix.dev/manual/nix/2.32/language/types#type-string) |
| ``` ''   multi    line     string '' ``` | A multi-line string. Strips common prefixed whitespace. Evaluates to `"multi\n line\n  string"`. |
| `# Explanation` | A [comment](https://nix.dev/manual/nix/2.32/language/syntax#comments). |
| `"hello ${ { a = "world"; }.a }"`  `"1 2 ${toString 3}"`  `"${pkgs.bash}/bin/sh"` | [String interpolation](https://nix.dev/manual/nix/2.32/language/string-interpolation) (expands to `"hello world"`, `"1 2 3"`, `"/nix/store/<hash>-bash-<version>/bin/sh"`) |
| `true`, `false` | [Booleans](https://nix.dev/manual/nix/2.32/language/types#type-boolean) |
| `null` | [Null](https://nix.dev/manual/nix/2.32/language/types#type-null) value |
| `123` | An [integer](https://nix.dev/manual/nix/2.32/language/types#type-int) |
| `3.141` | A [floating point number](https://nix.dev/manual/nix/2.32/language/types#type-float) |
| `/etc` | An absolute [path](https://nix.dev/manual/nix/2.32/language/types#type-path) |
| `./foo.png` | A [path](https://nix.dev/manual/nix/2.32/language/types#type-path) relative to the file containing this Nix expression |
| `~/.config` | A home [path](https://nix.dev/manual/nix/2.32/language/types#type-path). Evaluates to the `"<user's home directory>/.config"`. |
| `<nixpkgs>` | A [lookup path](https://nix.dev/manual/nix/2.32/language/constructs/lookup-path) for Nix files. Value determined by [`$NIX_PATH` environment variable](https://nix.dev/manual/nix/2.32/command-ref/env-common#env-NIX_PATH). |
| *Compound values* |  |
| `{ x = 1; y = 2; }` | An [attribute set](https://nix.dev/manual/nix/2.32/language/types#attribute-set) with attributes named `x` and `y` |
| `{ foo.bar = 1; }` | A nested set, equivalent to `{ foo = { bar = 1; }; }` |
| `rec { x = "foo"; y = x + "bar"; }` | A [recursive set](https://nix.dev/manual/nix/2.32/language/syntax#recursive-sets), equivalent to `{ x = "foo"; y = "foobar"; }`. |
| `[ "foo" "bar" "baz" ]`  `[ 1 2 3 ]`  `[ (f 1) { a = 1; b = 2; } [ "c" ] ]` | [Lists](https://nix.dev/manual/nix/2.32/language/types#list) with three elements. |
| *Operators* |  |
| `"foo" + "bar"` | String concatenation |
| `1 + 2` | Integer addition |
| `"foo" == "f" + "oo"` | Equality test (evaluates to `true`) |
| `"foo" != "bar"` | Inequality test (evaluates to `true`) |
| `!true` | Boolean negation |
| `{ x = 1; y = 2; }.x` | [Attribute selection](https://nix.dev/manual/nix/2.32/language/types#attribute-set) (evaluates to `1`) |
| `{ x = 1; y = 2; }.z or 3` | [Attribute selection](https://nix.dev/manual/nix/2.32/language/types#attribute-set) with default (evaluates to `3`) |
| `{ x = 1; y = 2; } // { z = 3; }` | Merge two sets (attributes in the right-hand set taking precedence) |
| *Control structures* |  |
| `if 1 + 1 == 2 then "yes!" else "no!"` | [Conditional expression](https://nix.dev/manual/nix/2.32/language/syntax#conditionals). |
| `assert 1 + 1 == 2; "yes!"` | [Assertion](https://nix.dev/manual/nix/2.32/language/syntax#assertions) check (evaluates to `"yes!"`). |
| `let x = "foo"; y = "bar"; in x + y` | Variable definition. See [`let`-expressions](https://nix.dev/manual/nix/2.32/language/syntax#let-expressions). |
| `with builtins; head [ 1 2 3 ]` | Add all attributes from the given set to the scope (evaluates to `1`).  See [`with`-expressions](https://nix.dev/manual/nix/2.32/language/syntax#with-expressions) for details and shadowing caveats. |
| `inherit pkgs src;` | Adds the variables to the current scope (attribute set or `let` binding). Desugars to `pkgs = pkgs; src = src;`. See [Inheriting attributes](https://nix.dev/manual/nix/2.32/language/syntax#inheriting-attributes). |
| `inherit (pkgs) lib stdenv;` | Adds the attributes, from the attribute set in parentheses, to the current scope (attribute set or `let` binding). Desugars to `lib = pkgs.lib; stdenv = pkgs.stdenv;`. See [Inheriting attributes](https://nix.dev/manual/nix/2.32/language/syntax#inheriting-attributes). |
| *[Functions](https://nix.dev/manual/nix/2.32/language/syntax#functions) (lambdas)* |  |
| `x: x + 1` | A [function](https://nix.dev/manual/nix/2.32/language/syntax#functions) that expects an integer and returns it increased by 1. |
| `x: y: x + y` | Curried [function](https://nix.dev/manual/nix/2.32/language/syntax#functions), equivalent to `x: (y: x + y)`. Can be used like a function that takes two arguments and returns their sum. |
| `(x: x + 1) 100` | A [function](https://nix.dev/manual/nix/2.32/language/syntax#functions) call (evaluates to 101) |
| `let inc = x: x + 1; in inc (inc (inc 100))` | A [function](https://nix.dev/manual/nix/2.32/language/syntax#functions) bound to a variable and subsequently called by name (evaluates to 103) |
| `{ x, y }: x + y` | A [function](https://nix.dev/manual/nix/2.32/language/syntax#functions) that expects a set with required attributes `x` and `y` and concatenates them |
| `{ x, y ? "bar" }: x + y` | A [function](https://nix.dev/manual/nix/2.32/language/syntax#functions) that expects a set with required attribute `x` and optional `y`, using `"bar"` as default value for `y` |
| `{ x, y, ... }: x + y` | A [function](https://nix.dev/manual/nix/2.32/language/syntax#functions) that expects a set with required attributes `x` and `y` and ignores any other attributes |
| `{ x, y } @ args: x + y`  `args @ { x, y }: x + y` | A [function](https://nix.dev/manual/nix/2.32/language/syntax#functions) that expects a set with required attributes `x` and `y`, and binds the whole set to `args` |
| *Built-in functions* |  |
| `import ./foo.nix` | Load and return Nix expression in given file. See [import](https://nix.dev/manual/nix/2.32/language/builtins#builtins-import). |
| `map (x: x + x) [ 1 2 3 ]` | Apply a function to every element of a list (evaluates to `[ 2 4 6 ]`). See [`map`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-map). |