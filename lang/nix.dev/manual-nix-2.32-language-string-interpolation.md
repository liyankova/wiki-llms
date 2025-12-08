---
url: https://nix.dev/manual/nix/2.32/language/string-interpolation
title: String interpolation - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# String interpolation - Nix 2.32.2 Reference Manual

# [String interpolation](https://nix.dev/manual/nix/2.32/language/string-interpolation#string-interpolation)

String interpolation is a language feature where a [string](https://nix.dev/manual/nix/2.32/language/types#type-string), [path](https://nix.dev/manual/nix/2.32/language/types#type-path), or [attribute name](https://nix.dev/manual/nix/2.32/language/types#attribute-set) can contain expressions enclosed in `${ }` (dollar-sign with curly brackets).

Such a construct is called *interpolated string*, and the expression inside is an [interpolated expression](https://nix.dev/manual/nix/2.32/language/string-interpolation#interpolated-expression).

> **Syntax**
>
> *interpolation\_element* → `${` *expression* `}`

## [Examples](https://nix.dev/manual/nix/2.32/language/string-interpolation#examples)

### [String](https://nix.dev/manual/nix/2.32/language/string-interpolation#string)

Rather than writing

```
"--with-freetype2-library=" + freetype + "/lib"
```

(where `freetype` is a [derivation expression](https://nix.dev/manual/nix/2.32/glossary#gloss-derivation-expression)), you can instead write

```
"--with-freetype2-library=${freetype}/lib"
```

The latter is automatically translated to the former.

A more complicated example (from the Nix expression for [Qt](http://www.trolltech.com/products/qt)):

```
configureFlags = "
  -system-zlib -system-libpng -system-libjpeg
  ${if openglSupport then "-dlopen-opengl
    -L${mesa}/lib -I${mesa}/include
    -L${libXmu}/lib -I${libXmu}/include" else ""}
  ${if threadSupport then "-thread" else "-no-thread"}
";
```

Note that Nix expressions and strings can be arbitrarily nested;
in this case the outer string contains various interpolated expressions that themselves contain strings (e.g., `"-thread"`), some of which in turn contain interpolated expressions (e.g., `${mesa}`).

To write a literal `${` in an regular string, escape it with a backslash (`\`).

> **Example**
>
> ```
> "echo \${PATH}"
> ```
>
> ```
> "echo ${PATH}"
> ```

To write a literal `${` in an indented string, escape it with two single quotes (`''`).

> **Example**
>
> ```
> ''
>   echo ''${PATH}
> ''
> ```
>
> ```
> "echo ${PATH}\n"
> ```

`$${` can be written literally in any string.

> **Example**
>
> In Make, `$` in file names or recipes is represented as `$$`, see [GNU `make`: Basics of Variable Reference](https://www.gnu.org/software/make/manual/html_node/Reference.html#Basics-of-Variable-References).
> This can be expressed directly in the Nix language strings:
>
> ```
> ''
>   MAKEVAR = Hello
>   all:
>   	@export BASHVAR=world; echo $(MAKEVAR) $${BASHVAR}
> ''
> ```
>
> ```
> "MAKEVAR = Hello\nall:\n\t@export BASHVAR=world; echo $(MAKEVAR) $\${BASHVAR}\n"
> ```

See the [documentation on strings](https://nix.dev/manual/nix/2.32/language/types#type-string) for details.

### [Path](https://nix.dev/manual/nix/2.32/language/string-interpolation#path)

Rather than writing

```
./. + "/" + foo + "-" + bar + ".nix"
```

or

```
./. + "/${foo}-${bar}.nix"
```

you can instead write

```
./${foo}-${bar}.nix
```

### [Attribute name](https://nix.dev/manual/nix/2.32/language/string-interpolation#attribute-name)

Attribute names can be interpolated strings.

> **Example**
>
> ```
> let name = "foo"; in
> { ${name} = 123; }
> ```
>
> ```
> { foo = 123; }
> ```

Attributes can be selected with interpolated strings.

> **Example**
>
> ```
> let name = "foo"; in
> { foo = 123; }.${name}
> ```
>
> ```
> 123
> ```

# [Interpolated expression](https://nix.dev/manual/nix/2.32/language/string-interpolation#interpolated-expression)

An expression that is interpolated must evaluate to one of the following:

* a [string](https://nix.dev/manual/nix/2.32/language/types#type-string)
* a [path](https://nix.dev/manual/nix/2.32/language/types#type-path)
* an [attribute set](https://nix.dev/manual/nix/2.32/language/types#attribute-set) that has a `__toString` attribute or an `outPath` attribute

  + `__toString` must be a function that takes the attribute set itself and returns a string
  + `outPath` must be a string

  This includes [derivation expressions](https://nix.dev/manual/nix/2.32/language/derivations) or [flake inputs](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-flake#flake-inputs) (experimental).

A string interpolates to itself.

A path in an interpolated expression is first copied into the Nix store, and the resulting string is the [store path](https://nix.dev/manual/nix/2.32/store/store-path) of the newly created [store object](https://nix.dev/manual/nix/2.32/store/store-object).

> **Example**
>
> ```
> $ mkdir foo
> ```
>
> Reference the empty directory in an interpolated expression:
>
> ```
> "${./foo}"
> ```
>
> ```
> "/nix/store/2hhl2nz5v0khbn06ys82nrk99aa1xxdw-foo"
> ```

A derivation interpolates to the [store path](https://nix.dev/manual/nix/2.32/store/store-path) of its first [output](https://nix.dev/manual/nix/2.32/language/derivations#attr-outputs).

> **Example**
>
> ```
> let
>   pkgs = import <nixpkgs> {};
> in
> "${pkgs.hello}"
> ```
>
> ```
> "/nix/store/4xpfqf29z4m8vbhrqcz064wfmb46w5r7-hello-2.12.1"
> ```

An attribute set interpolates to the return value of the function in the `__toString` applied to the attribute set itself.

> **Example**
>
> ```
> let
>   a = {
>     value = 1;
>     __toString = self: toString (self.value + 1);
>   };
> in
> "${a}"
> ```
>
> ```
> "2"
> ```

An attribute set also interpolates to the value of its `outPath` attribute.

> **Example**
>
> ```
> let
>   a = { outPath = "foo"; };
> in
> "${a}"
> ```
>
> ```
> "foo"
> ```

If both `__toString` and `outPath` are present in an attribute set, `__toString` takes precedence.

> **Example**
>
> ```
> let
>   a = { __toString = _: "yes"; outPath = throw "no"; };
> in
> "${a}"
> ```
>
> ```
> "yes"
> ```

If neither is present, an error is thrown.

> **Example**
>
> ```
> let
>   a = {};
> in
> "${a}"
> ```
>
> ```
> error: cannot coerce a set to a string: { }
>
>        at «string»:4:2:
>
>             3| in
>             4| "${a}"
>              |  ^
> ```