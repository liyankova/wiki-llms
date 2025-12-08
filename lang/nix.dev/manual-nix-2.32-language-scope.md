---
url: https://nix.dev/manual/nix/2.32/language/scope
title: Scoping rules - Nix 2.32.2 Reference Manual
source_domain: nix.dev
---

# Scoping rules - Nix 2.32.2 Reference Manual

# [Scoping rules](https://nix.dev/manual/nix/2.32/language/scope#scoping-rules)

A *scope* in the Nix language is a dictionary keyed by [name](https://nix.dev/manual/nix/2.32/language/identifiers#names), mapping each name to an expression and a *definition type*.
The definition type is either *explicit* or *implicit*.
Each entry in this dictionary is a *definition*.

Explicit definitions are created by the following expressions:

* [let-expressions](https://nix.dev/manual/nix/2.32/language/syntax#let-expressions)
* [recursive attribute set literals](https://nix.dev/manual/nix/2.32/language/syntax#recursive-sets) (`rec`)
* [function literals](https://nix.dev/manual/nix/2.32/language/syntax#functions)

Implicit definitions are only created by [with-expressions](https://nix.dev/manual/nix/2.32/language/syntax#with-expressions).

Every expression is *enclosed* by a scope.
The outermost expression is enclosed by the [built-in, global scope](https://nix.dev/manual/nix/2.32/language/builtins), which contains only explicit definitions.
The expressions listed above *extend* their enclosing scope by adding new definitions, or replacing existing ones with the same name.
An explicit definition can replace a definition of any type; an implicit definition can only replace another implicit definition.

Each of the above expressions defines which of its subexpressions are enclosed by the extended scope.
In all other cases, the same scope that encloses an expression is the enclosing scope for its subexpressions.

The Nix language is [statically scoped](https://en.wikipedia.org/wiki/Scope_(computer_science)#Lexical_scope);
the value of a variable is determined only by the variable's enclosing scope, and not by the dynamic context in which the variable is evaluated.

> **Note**
>
> Expressions entered into the [Nix REPL](https://nix.dev/manual/nix/2.32/command-ref/new-cli/nix3-repl) are enclosed by a scope that can be extended by command line arguments or previous REPL commands.
> These ways of extending scope are not, strictly speaking, part of the Nix language.