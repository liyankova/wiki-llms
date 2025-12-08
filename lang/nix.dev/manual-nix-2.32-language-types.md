---
url: https://nix.dev/manual/nix/2.32/language/types
title: Data Types - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Data Types - Nix 2.32.2 Reference Manual

# [Data Types](https://nix.dev/manual/nix/2.32/language/types#data-types)

Every value in the Nix language has one of the following types:

* [Integer](https://nix.dev/manual/nix/2.32/language/types#type-int)
* [Float](https://nix.dev/manual/nix/2.32/language/types#type-float)
* [Boolean](https://nix.dev/manual/nix/2.32/language/types#type-bool)
* [String](https://nix.dev/manual/nix/2.32/language/types#type-string)
* [Path](https://nix.dev/manual/nix/2.32/language/types#type-path)
* [Null](https://nix.dev/manual/nix/2.32/language/types#type-null)
* [Attribute set](https://nix.dev/manual/nix/2.32/language/types#type-attrs)
* [List](https://nix.dev/manual/nix/2.32/language/types#type-list)
* [Function](https://nix.dev/manual/nix/2.32/language/types#type-function)
* [External](https://nix.dev/manual/nix/2.32/language/types#type-external)

## [Primitives](https://nix.dev/manual/nix/2.32/language/types#primitives)

### [Integer](https://nix.dev/manual/nix/2.32/language/types#type-int)

An *integer* in the Nix language is a signed 64-bit integer.

Non-negative integers can be expressed as [integer literals](https://nix.dev/manual/nix/2.32/language/syntax#number-literal).
Negative integers are created with the [arithmetic negation operator](https://nix.dev/manual/nix/2.32/language/operators#arithmetic).
The function [`builtins.isInt`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-isInt) can be used to determine if a value is an integer.

### [Float](https://nix.dev/manual/nix/2.32/language/types#type-float)

A *float* in the Nix language is a 64-bit [IEEE 754](https://en.wikipedia.org/wiki/IEEE_754) floating-point number.

Most non-negative floats can be expressed as [float literals](https://nix.dev/manual/nix/2.32/language/syntax#number-literal).
Negative floats are created with the [arithmetic negation operator](https://nix.dev/manual/nix/2.32/language/operators#arithmetic).
The function [`builtins.isFloat`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-isFloat) can be used to determine if a value is a float.

### [Boolean](https://nix.dev/manual/nix/2.32/language/types#type-bool)

A *boolean* in the Nix language is one of *true* or *false*.

These values are available as attributes of [`builtins`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-builtins) as [`builtins.true`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-true) and [`builtins.false`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-false).
The function [`builtins.isBool`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-isBool) can be used to determine if a value is a boolean.

### [String](https://nix.dev/manual/nix/2.32/language/types#type-string)

A *string* in the Nix language is an immutable, finite-length sequence of bytes, along with a [string context](https://nix.dev/manual/nix/2.32/language/string-context).
Nix does not assume or support working natively with character encodings.

String values without string context can be expressed as [string literals](https://nix.dev/manual/nix/2.32/language/string-literals).
The function [`builtins.isString`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-isString) can be used to determine if a value is a string.

### [Path](https://nix.dev/manual/nix/2.32/language/types#type-path)

A *path* in the Nix language is an immutable, finite-length sequence of bytes starting with `/`, representing a POSIX-style, canonical file system path.
Path values are distinct from string values, even if they contain the same sequence of bytes.
Operations that produce paths will simplify the result as the standard C function [`realpath`](https://pubs.opengroup.org/onlinepubs/9699919799/functions/realpath.html) would, except that there is no symbolic link resolution.

Paths are suitable for referring to local files, and are often preferable over strings.

* Path values do not contain trailing or duplicate slashes, `.`, or `..`.
* Relative path literals are automatically resolved relative to their [base directory](https://nix.dev/manual/nix/2.32/glossary#gloss-base-directory).
* Tooling can recognize path literals and provide additional features, such as autocompletion, refactoring automation and jump-to-file.

A file is not required to exist at a given path in order for that path value to be valid, but a path that is converted to a string with [string interpolation](https://nix.dev/manual/nix/2.32/language/string-interpolation#interpolated-expression) or [string-and-path concatenation](https://nix.dev/manual/nix/2.32/language/operators#string-and-path-concatenation) must resolve to a readable file or directory which will be copied into the Nix store.
For instance, evaluating `"${./foo.txt}"` will cause `foo.txt` from the same directory to be copied into the Nix store and result in the string `"/nix/store/<hash>-foo.txt"`.
Operations such as [`import`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-import) can also expect a path to resolve to a readable file or directory.

> **Note**
>
> The Nix language assumes that all input files will remain *unchanged* while evaluating a Nix expression.
> For example, assume you used a file path in an interpolated string during a `nix repl` session.
> Later in the same session, after having changed the file contents, evaluating the interpolated string with the file path again might not return a new [store path](https://nix.dev/manual/nix/2.32/store/store-path), since Nix might not re-read the file contents.
> Use `:r` to reset the repl as needed.

Path values can be expressed as [path literals](https://nix.dev/manual/nix/2.32/language/syntax#path-literal).
The function [`builtins.isPath`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-isPath) can be used to determine if a value is a path.

### [Null](https://nix.dev/manual/nix/2.32/language/types#type-null)

There is a single value of type *null* in the Nix language.

This value is available as an attribute on the [`builtins`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-builtins) attribute set as [`builtins.null`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-null).

## [Compound values](https://nix.dev/manual/nix/2.32/language/types#compound-values)

### [Attribute set](https://nix.dev/manual/nix/2.32/language/types#type-attrs)

An attribute set can be constructed with an [attribute set literal](https://nix.dev/manual/nix/2.32/language/syntax#attrs-literal).
The function [`builtins.isAttrs`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-isAttrs) can be used to determine if a value is an attribute set.

### [List](https://nix.dev/manual/nix/2.32/language/types#type-list)

A list can be constructed with a [list literal](https://nix.dev/manual/nix/2.32/language/syntax#list-literal).
The function [`builtins.isList`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-isList) can be used to determine if a value is a list.

## [Function](https://nix.dev/manual/nix/2.32/language/types#type-function)

A function can be constructed with a [function expression](https://nix.dev/manual/nix/2.32/language/syntax#functions).
The function [`builtins.isFunction`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-isFunction) can be used to determine if a value is a function.

## [External](https://nix.dev/manual/nix/2.32/language/types#type-external)

An *external* value is an opaque value created by a Nix [plugin](https://nix.dev/manual/nix/2.32/command-ref/conf-file#conf-plugin-files).
Such a value can be substituted in Nix expressions but only created and used by plugin code.