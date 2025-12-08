---
url: https://nix.dev/manual/nix/2.32/language/identifiers
title: Identifiers - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Identifiers - Nix 2.32.2 Reference Manual

# [Identifiers](https://nix.dev/manual/nix/2.32/language/identifiers#identifiers)

An *identifier* is an [ASCII](https://en.wikipedia.org/wiki/ASCII) character sequence that:

* Starts with a letter (`a-z`, `A-Z`) or underscore (`_`)
* Can contain any number of:
  + Letters (`a-z`, `A-Z`)
  + Digits (`0-9`)
  + Underscores (`_`)
  + Apostrophes (`'`)
  + Hyphens (`-`)
* Is not one of the [keywords](https://nix.dev/manual/nix/2.32/language/identifiers#keywords)

> **Syntax**
>
> *identifier* ~ `[A-Za-z_][A-Za-z0-9_'-]*`

# [Names](https://nix.dev/manual/nix/2.32/language/identifiers#names)

A *name* can be written as an [identifier](https://nix.dev/manual/nix/2.32/language/identifiers#identifier) or a [string literal](https://nix.dev/manual/nix/2.32/language/string-literals).

> **Syntax**
>
> *name* → *identifier* | *string*

Names are used in [attribute sets](https://nix.dev/manual/nix/2.32/language/syntax#attrs-literal), [`let` bindings](https://nix.dev/manual/nix/2.32/language/syntax#let-expressions), and [`inherit`](https://nix.dev/manual/nix/2.32/language/syntax#inheriting-attributes).
Two names are the same if they represent the same sequence of characters, regardless of whether they are written as identifiers or strings.

# [Keywords](https://nix.dev/manual/nix/2.32/language/identifiers#keywords)

These keywords are reserved and cannot be used as [identifiers](https://nix.dev/manual/nix/2.32/language/identifiers#identifiers):

* [`assert`](https://nix.dev/manual/nix/2.32/language/syntax#assertions)
* [`else`](https://nix.dev/manual/nix/2.32/language/syntax#conditionals)
* [`if`](https://nix.dev/manual/nix/2.32/language/syntax#conditionals)
* [`in`](https://nix.dev/manual/nix/2.32/language/syntax#let-expressions)
* [`inherit`](https://nix.dev/manual/nix/2.32/language/syntax#inheriting-attributes)
* [`let`](https://nix.dev/manual/nix/2.32/language/syntax#let-expressions)
* [`or`](https://nix.dev/manual/nix/2.32/language/operators#attribute-selection) (see note)
* [`rec`](https://nix.dev/manual/nix/2.32/language/syntax#recursive-sets)
* [`then`](https://nix.dev/manual/nix/2.32/language/syntax#conditionals)
* [`with`](https://nix.dev/manual/nix/2.32/language/syntax#with-expressions)

> **Note**
>
> The Nix language evaluator currently allows `or` to be used as a name in some contexts, for backwards compatibility reasons.
> Users are advised not to rely on this.
>
> There are long-standing issues with how `or` is parsed as a name, which can't be resolved without making a breaking change to the language.