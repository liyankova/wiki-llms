---
url: https://nix.dev/manual/nix/2.32/language/operators
title: Operators - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Operators - Nix 2.32.2 Reference Manual

# [Operators](https://nix.dev/manual/nix/2.32/language/operators#operators)

| Name | Syntax | Associativity | Precedence |
| --- | --- | --- | --- |
| [Attribute selection](https://nix.dev/manual/nix/2.32/language/operators#attribute-selection) | *attrset* `.` *attrpath* [ `or` *expr* ] | none | 1 |
| [Function application](https://nix.dev/manual/nix/2.32/language/operators#function-application) | *func* *expr* | left | 2 |
| [Arithmetic negation](https://nix.dev/manual/nix/2.32/language/operators#arithmetic) | `-` *number* | none | 3 |
| [Has attribute](https://nix.dev/manual/nix/2.32/language/operators#has-attribute) | *attrset* `?` *attrpath* | none | 4 |
| List concatenation | *list* `++` *list* | right | 5 |
| [Multiplication](https://nix.dev/manual/nix/2.32/language/operators#arithmetic) | *number* `*` *number* | left | 6 |
| [Division](https://nix.dev/manual/nix/2.32/language/operators#arithmetic) | *number* `/` *number* | left | 6 |
| [Subtraction](https://nix.dev/manual/nix/2.32/language/operators#arithmetic) | *number* `-` *number* | left | 7 |
| [Addition](https://nix.dev/manual/nix/2.32/language/operators#arithmetic) | *number* `+` *number* | left | 7 |
| [String concatenation](https://nix.dev/manual/nix/2.32/language/operators#string-concatenation) | *string* `+` *string* | left | 7 |
| [Path concatenation](https://nix.dev/manual/nix/2.32/language/operators#path-concatenation) | *path* `+` *path* | left | 7 |
| [Path and string concatenation](https://nix.dev/manual/nix/2.32/language/operators#path-and-string-concatenation) | *path* `+` *string* | left | 7 |
| [String and path concatenation](https://nix.dev/manual/nix/2.32/language/operators#string-and-path-concatenation) | *string* `+` *path* | left | 7 |
| Logical negation (`NOT`) | `!` *bool* | none | 8 |
| [Update](https://nix.dev/manual/nix/2.32/language/operators#update) | *attrset* `//` *attrset* | right | 9 |
| [Less than](https://nix.dev/manual/nix/2.32/language/operators#comparison) | *expr* `<` *expr* | none | 10 |
| [Less than or equal to](https://nix.dev/manual/nix/2.32/language/operators#comparison) | *expr* `<=` *expr* | none | 10 |
| [Greater than](https://nix.dev/manual/nix/2.32/language/operators#comparison) | *expr* `>` *expr* | none | 10 |
| [Greater than or equal to](https://nix.dev/manual/nix/2.32/language/operators#comparison) | *expr* `>=` *expr* | none | 10 |
| [Equality](https://nix.dev/manual/nix/2.32/language/operators#equality) | *expr* `==` *expr* | none | 11 |
| Inequality | *expr* `!=` *expr* | none | 11 |
| Logical conjunction (`AND`) | *bool* `&&` *bool* | left | 12 |
| Logical disjunction (`OR`) | *bool* `||` *bool* | left | 13 |
| [Logical implication](https://nix.dev/manual/nix/2.32/language/operators#logical-implication) | *bool* `->` *bool* | right | 14 |
| [Pipe operator](https://nix.dev/manual/nix/2.32/language/operators#pipe-operators) (experimental) | *expr* `|>` *func* | left | 15 |
| [Pipe operator](https://nix.dev/manual/nix/2.32/language/operators#pipe-operators) (experimental) | *func* `<|` *expr* | right | 15 |

## [Attribute selection](https://nix.dev/manual/nix/2.32/language/operators#attribute-selection)

> **Syntax**
>
> *attrset* `.` *attrpath* [ `or` *expr* ]

Select the attribute denoted by attribute path *attrpath* from [attribute set](https://nix.dev/manual/nix/2.32/language/types#type-attrs) *attrset*.
If the attribute doesn’t exist, return the *expr* after `or` if provided, otherwise abort evaluation.

## [Function application](https://nix.dev/manual/nix/2.32/language/operators#function-application)

> **Syntax**
>
> *func* *expr*

Apply the callable value *func* to the argument *expr*. Note the absence of any visible operator symbol.
A callable value is either:

* a [user-defined function](https://nix.dev/manual/nix/2.32/language/syntax#functions)
* a [built-in](https://nix.dev/manual/nix/2.32/language/builtins) function
* an attribute set with a [`__functor` attribute](https://nix.dev/manual/nix/2.32/language/syntax#attr-__functor)

> **Warning**
>
> [List](https://nix.dev/manual/nix/2.32/language/types#type-list) items are also separated by whitespace, which means that function calls in list items must be enclosed by parentheses.

## [Has attribute](https://nix.dev/manual/nix/2.32/language/operators#has-attribute)

> **Syntax**
>
> *attrset* `?` *attrpath*

Test whether [attribute set](https://nix.dev/manual/nix/2.32/language/types#type-attrs) *attrset* contains the attribute denoted by *attrpath*.
The result is a [Boolean](https://nix.dev/manual/nix/2.32/language/types#type-bool) value.

See also: [`builtins.hasAttr`](https://nix.dev/manual/nix/2.32/language/builtins#builtins-hasAttr)

After evaluating *attrset* and *attrpath*, the computational complexity is O(log(*n*)) for *n* attributes in the *attrset*

## [Arithmetic](https://nix.dev/manual/nix/2.32/language/operators#arithmetic)

Numbers will retain their type unless mixed with other numeric types:
Pure integer operations will always return integers, whereas any operation involving at least one floating point number returns a floating point number.

Evaluation of the following numeric operations throws an evaluation error:

* Division by zero
* Integer overflow, that is, any operation yielding a result outside of the representable range of [Nix language integers](https://nix.dev/manual/nix/2.32/language/syntax#number-literal)

See also [Comparison](https://nix.dev/manual/nix/2.32/language/operators#comparison) and [Equality](https://nix.dev/manual/nix/2.32/language/operators#equality).

The `+` operator is overloaded to also work on strings and paths.

## [String concatenation](https://nix.dev/manual/nix/2.32/language/operators#string-concatenation)

> **Syntax**
>
> *string* `+` *string*

Concatenate two [strings](https://nix.dev/manual/nix/2.32/language/types#type-string) and merge their [string contexts](https://nix.dev/manual/nix/2.32/language/string-context).

## [Path concatenation](https://nix.dev/manual/nix/2.32/language/operators#path-concatenation)

> **Syntax**
>
> *path* `+` *path*

Concatenate two [paths](https://nix.dev/manual/nix/2.32/language/types#type-path).
The result is a path.

## [Path and string concatenation](https://nix.dev/manual/nix/2.32/language/operators#path-and-string-concatenation)

> **Syntax**
>
> *path* + *string*

Concatenate *[path](https://nix.dev/manual/nix/2.32/language/types#type-path)* with *[string](https://nix.dev/manual/nix/2.32/language/types#type-string)*.
The result is a path.

> **Note**
>
> The string must not have a [string context](https://nix.dev/manual/nix/2.32/language/string-context) that refers to a [store path](https://nix.dev/manual/nix/2.32/store/store-path).

## [String and path concatenation](https://nix.dev/manual/nix/2.32/language/operators#string-and-path-concatenation)

> **Syntax**
>
> *string* + *path*

Concatenate *[string](https://nix.dev/manual/nix/2.32/language/types#type-string)* with *[path](https://nix.dev/manual/nix/2.32/language/types#type-path)*.
The result is a string.

> **Important**
>
> The file or directory at *path* must exist and is copied to the [store](https://nix.dev/manual/nix/2.32/glossary#gloss-store).
> The path appears in the result as the corresponding [store path](https://nix.dev/manual/nix/2.32/store/store-path).

## [Update](https://nix.dev/manual/nix/2.32/language/operators#update)

> **Syntax**
>
> *attrset1* // *attrset2*

Update [attribute set](https://nix.dev/manual/nix/2.32/language/types#type-attrs) *attrset1* with names and values from *attrset2*.

The returned attribute set will have all of the attributes in *attrset1* and *attrset2*.
If an attribute name is present in both, the attribute value from the latter is taken.

## [Comparison](https://nix.dev/manual/nix/2.32/language/operators#comparison)

Comparison is

* [arithmetic](https://nix.dev/manual/nix/2.32/language/operators#arithmetic) for [numbers](https://nix.dev/manual/nix/2.32/language/types#type-float)
* lexicographic for [strings](https://nix.dev/manual/nix/2.32/language/types#type-string) and [paths](https://nix.dev/manual/nix/2.32/language/types#type-path)
* item-wise lexicographic for [lists](https://nix.dev/manual/nix/2.32/language/types#type-list):
  elements at the same index in both lists are compared according to their type and skipped if they are equal.

All comparison operators are implemented in terms of `<`, and the following equivalencies hold:

| comparison | implementation |
| --- | --- |
| *a* `<=` *b* | `! (` *b* `<` *a* `)` |
| *a* `>` *b* | *b* `<` *a* |
| *a* `>=` *b* | `! (` *a* `<` *b* `)` |

## [Equality](https://nix.dev/manual/nix/2.32/language/operators#equality)

* [Attribute sets](https://nix.dev/manual/nix/2.32/language/types#type-attrs) and [lists](https://nix.dev/manual/nix/2.32/language/types#type-list) are compared recursively, and therefore are fully evaluated.
* Comparison of [functions](https://nix.dev/manual/nix/2.32/language/syntax#functions) always returns `false`.
* Numbers are type-compatible, see [arithmetic](https://nix.dev/manual/nix/2.32/language/operators#arithmetic) operators.
* Floating point numbers only differ up to a limited precision.

## [Logical implication](https://nix.dev/manual/nix/2.32/language/operators#logical-implication)

Equivalent to `!`*b1* `||` *b2* (or `if` *b1* `then` *b2* `else true`)

## [Pipe operators](https://nix.dev/manual/nix/2.32/language/operators#pipe-operators)

* *a* `|>` *b* is equivalent to *b* *a*
* *a* `<|` *b* is equivalent to *a* *b*

> **Example**
>
> ```
> nix-repl> 1 |> builtins.add 2 |> builtins.mul 3
> 9
>
> nix-repl> builtins.add 1 <| builtins.mul 2 <| 3
> 7
> ```

> **Warning**
>
> This syntax is part of an
> [experimental feature](https://nix.dev/manual/nix/2.32/development/experimental-features)
> and may change in future releases.
>
> To use this syntax, make sure the
> [`pipe-operators` experimental feature](https://nix.dev/manual/nix/2.32/development/experimental-features#xp-feature-pipe-operators)
> is enabled.
> For example, include the following in [`nix.conf`](https://nix.dev/manual/nix/2.32/command-ref/conf-file):
>
> ```
> extra-experimental-features = pipe-operators
> ```