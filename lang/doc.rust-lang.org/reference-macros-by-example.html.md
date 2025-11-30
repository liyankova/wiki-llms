---
url: https://doc.rust-lang.org/reference/macros-by-example.html
title: Macros By Example - The Rust Reference
source_domain: doc.rust-lang.org
---

# Macros By Example - The Rust Reference

[[macro.decl]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl "macro.decl")

# [Macros By Example](https://doc.rust-lang.org/reference/macros-by-example.html#macros-by-example)

[[macro.decl.syntax]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.syntax "macro.decl.syntax")

**Syntax**
  
[MacroRulesDefinition](https://doc.rust-lang.org/reference/macros-by-example.html#railroad-MacroRulesDefinition) →   
    macro\_rules ! [IDENTIFIER](https://doc.rust-lang.org/reference/identifiers.html#grammar-IDENTIFIER) [MacroRulesDef](https://doc.rust-lang.org/reference/macros-by-example.html#grammar-MacroRulesDef)

[MacroRulesDef](https://doc.rust-lang.org/reference/macros-by-example.html#railroad-MacroRulesDef) →   
      ( [MacroRules](https://doc.rust-lang.org/reference/macros-by-example.html#grammar-MacroRules) ) ;   
    | [ [MacroRules](https://doc.rust-lang.org/reference/macros-by-example.html#grammar-MacroRules) ] ;   
    | { [MacroRules](https://doc.rust-lang.org/reference/macros-by-example.html#grammar-MacroRules) }

[MacroRules](https://doc.rust-lang.org/reference/macros-by-example.html#railroad-MacroRules) →   
    [MacroRule](https://doc.rust-lang.org/reference/macros-by-example.html#grammar-MacroRule) ( ; [MacroRule](https://doc.rust-lang.org/reference/macros-by-example.html#grammar-MacroRule) )\* ;?

[MacroRule](https://doc.rust-lang.org/reference/macros-by-example.html#railroad-MacroRule) →   
    [MacroMatcher](https://doc.rust-lang.org/reference/macros-by-example.html#grammar-MacroMatcher) => [MacroTranscriber](https://doc.rust-lang.org/reference/macros-by-example.html#grammar-MacroTranscriber)

[MacroMatcher](https://doc.rust-lang.org/reference/macros-by-example.html#railroad-MacroMatcher) →   
      ( [MacroMatch](https://doc.rust-lang.org/reference/macros-by-example.html#grammar-MacroMatch)\* )   
    | [ [MacroMatch](https://doc.rust-lang.org/reference/macros-by-example.html#grammar-MacroMatch)\* ]   
    | { [MacroMatch](https://doc.rust-lang.org/reference/macros-by-example.html#grammar-MacroMatch)\* }

[MacroMatch](https://doc.rust-lang.org/reference/macros-by-example.html#railroad-MacroMatch) →   
      [Token](https://doc.rust-lang.org/reference/tokens.html#grammar-Token)except `$` and [delimiters](https://doc.rust-lang.org/reference/tokens.html#r-lex.token.delim)   
    | [MacroMatcher](https://doc.rust-lang.org/reference/macros-by-example.html#grammar-MacroMatcher)   
    | $ ( [IDENTIFIER\_OR\_KEYWORD](https://doc.rust-lang.org/reference/identifiers.html#grammar-IDENTIFIER_OR_KEYWORD)except `crate` | [RAW\_IDENTIFIER](https://doc.rust-lang.org/reference/identifiers.html#grammar-RAW_IDENTIFIER) | \_ ) : [MacroFragSpec](https://doc.rust-lang.org/reference/macros-by-example.html#grammar-MacroFragSpec)   
    | $ ( [MacroMatch](https://doc.rust-lang.org/reference/macros-by-example.html#grammar-MacroMatch)+ ) [MacroRepSep](https://doc.rust-lang.org/reference/macros-by-example.html#grammar-MacroRepSep)? [MacroRepOp](https://doc.rust-lang.org/reference/macros-by-example.html#grammar-MacroRepOp)

[MacroFragSpec](https://doc.rust-lang.org/reference/macros-by-example.html#railroad-MacroFragSpec) →   
      block | expr | expr\_2021 | ident | item | lifetime | literal   
    | meta | pat | pat\_param | path | stmt | tt | ty | vis

[MacroRepSep](https://doc.rust-lang.org/reference/macros-by-example.html#railroad-MacroRepSep) → [Token](https://doc.rust-lang.org/reference/tokens.html#grammar-Token)except [delimiters](https://doc.rust-lang.org/reference/tokens.html#r-lex.token.delim) and [MacroRepOp](https://doc.rust-lang.org/reference/macros-by-example.html#grammar-MacroRepOp)

[MacroRepOp](https://doc.rust-lang.org/reference/macros-by-example.html#railroad-MacroRepOp) → \* | + | ?

[MacroTranscriber](https://doc.rust-lang.org/reference/macros-by-example.html#railroad-MacroTranscriber) → [DelimTokenTree](https://doc.rust-lang.org/reference/macros.html#grammar-DelimTokenTree)

[[macro.decl.intro]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.intro "macro.decl.intro")

`macro_rules` allows users to define syntax extension in a declarative way. We
call such extensions “macros by example” or simply “macros”.

Each macro by example has a name, and one or more *rules*. Each rule has two
parts: a *matcher*, describing the syntax that it matches, and a *transcriber*,
describing the syntax that will replace a successfully matched invocation. Both
the matcher and the transcriber must be surrounded by delimiters. Macros can
expand to expressions, statements, items (including traits, impls, and foreign
items), types, or patterns.

[[macro.decl.transcription]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.transcription "macro.decl.transcription")

## [Transcribing](https://doc.rust-lang.org/reference/macros-by-example.html#transcribing)

[[macro.decl.transcription.intro]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.transcription.intro "macro.decl.transcription.intro")

When a macro is invoked, the macro expander looks up macro invocations by name,
and tries each macro rule in turn. It transcribes the first successful match; if
this results in an error, then future matches are not tried.

[[macro.decl.transcription.lookahead]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.transcription.lookahead "macro.decl.transcription.lookahead")

When matching, no lookahead is performed; if the compiler cannot unambiguously determine how to
parse the macro invocation one token at a time, then it is an error. In the
following example, the compiler does not look ahead past the identifier to see
if the following token is a `)`, even though that would allow it to parse the
invocation unambiguously:

```
```
#![allow(unused)]
fn main() {
macro_rules! ambiguity {
    ($($i:ident)* $j:ident) => { };
}

ambiguity!(error); // Error: local ambiguity
}
```
```

[[macro.decl.transcription.syntax]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.transcription.syntax "macro.decl.transcription.syntax")

In both the matcher and the transcriber, the `$` token is used to invoke special
behaviours from the macro engine (described below in [Metavariables](https://doc.rust-lang.org/reference/macros-by-example.html#metavariables) and
[Repetitions](https://doc.rust-lang.org/reference/macros-by-example.html#repetitions)). Tokens that aren’t part of such an invocation are matched and
transcribed literally, with one exception. The exception is that the outer
delimiters for the matcher will match any pair of delimiters. Thus, for
instance, the matcher `(())` will match `{()}` but not `{{}}`. The character
`$` cannot be matched or transcribed literally.

[[macro.decl.transcription.fragment]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.transcription.fragment "macro.decl.transcription.fragment")

### [Forwarding a matched fragment](https://doc.rust-lang.org/reference/macros-by-example.html#forwarding-a-matched-fragment)

When forwarding a matched fragment to another macro-by-example, matchers in
the second macro will see an opaque AST of the fragment type. The second macro
can’t use literal tokens to match the fragments in the matcher, only a
fragment specifier of the same type. The `ident`, `lifetime`, and `tt`
fragment types are an exception, and *can* be matched by literal tokens. The
following illustrates this restriction:

```
```
#![allow(unused)]
fn main() {
macro_rules! foo {
    ($l:expr) => { bar!($l); }
// ERROR:               ^^ no rules expected this token in macro call
}

macro_rules! bar {
    (3) => {}
}

foo!(3);
}
```
```

The following illustrates how tokens can be directly matched after matching a
`tt` fragment:

```
```
#![allow(unused)]
fn main() {
// compiles OK
macro_rules! foo {
    ($l:tt) => { bar!($l); }
}

macro_rules! bar {
    (3) => {}
}

foo!(3);
}
```
```

[[macro.decl.meta]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.meta "macro.decl.meta")

## [Metavariables](https://doc.rust-lang.org/reference/macros-by-example.html#metavariables)

[[macro.decl.meta.intro]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.meta.intro "macro.decl.meta.intro")

In the matcher, `$` *name* `:` *fragment-specifier* matches a Rust syntax
fragment of the kind specified and binds it to the metavariable `$`*name*.

[[macro.decl.meta.specifier]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.meta.specifier "macro.decl.meta.specifier")

Valid fragment specifiers are:

* `block`: a [BlockExpression](https://doc.rust-lang.org/reference/expressions/block-expr.html#grammar-BlockExpression)
* `expr`: an [Expression](https://doc.rust-lang.org/reference/expressions.html#grammar-Expression)
* `expr_2021`: an [Expression](https://doc.rust-lang.org/reference/expressions.html#grammar-Expression) except [UnderscoreExpression](https://doc.rust-lang.org/reference/expressions/underscore-expr.html#grammar-UnderscoreExpression) and [ConstBlockExpression](https://doc.rust-lang.org/reference/expressions/block-expr.html#grammar-ConstBlockExpression) (see [macro.decl.meta.edition2024](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.meta.edition2024))
* `ident`: an [IDENTIFIER\_OR\_KEYWORD](https://doc.rust-lang.org/reference/identifiers.html#grammar-IDENTIFIER_OR_KEYWORD), [RAW\_IDENTIFIER](https://doc.rust-lang.org/reference/identifiers.html#grammar-RAW_IDENTIFIER), or [`$crate`](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.hygiene.crate)
* `item`: an [Item](https://doc.rust-lang.org/reference/items.html#grammar-Item)
* `lifetime`: a [LIFETIME\_TOKEN](https://doc.rust-lang.org/reference/tokens.html#grammar-LIFETIME_TOKEN)
* `literal`: matches `-`?[LiteralExpression](https://doc.rust-lang.org/reference/expressions/literal-expr.html#grammar-LiteralExpression)
* `meta`: an [Attr](https://doc.rust-lang.org/reference/attributes.html#grammar-Attr), the contents of an attribute
* `pat`: a [Pattern](https://doc.rust-lang.org/reference/patterns.html#grammar-Pattern) (see [macro.decl.meta.edition2021](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.meta.edition2021))
* `pat_param`: a [PatternNoTopAlt](https://doc.rust-lang.org/reference/patterns.html#grammar-PatternNoTopAlt)
* `path`: a [TypePath](https://doc.rust-lang.org/reference/paths.html#grammar-TypePath) style path
* `stmt`: a [Statement](https://doc.rust-lang.org/reference/statements.html#grammar-Statement) without the trailing semicolon (except for item statements that require semicolons)
* `tt`: a [TokenTree](https://doc.rust-lang.org/reference/macros.html#grammar-TokenTree) (a single [token](https://doc.rust-lang.org/reference/tokens.html) or tokens in matching delimiters `()`, `[]`, or `{}`)
* `ty`: a [Type](https://doc.rust-lang.org/reference/types.html#grammar-Type)
* `vis`: a possibly empty [Visibility](https://doc.rust-lang.org/reference/visibility-and-privacy.html#grammar-Visibility) qualifier

[[macro.decl.meta.transcription]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.meta.transcription "macro.decl.meta.transcription")

In the transcriber, metavariables are referred to simply by `$`*name*, since
the fragment kind is specified in the matcher. Metavariables are replaced with
the syntax element that matched them.
Metavariables can be transcribed more than once or not at all.

[[macro.decl.meta.dollar-crate]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.meta.dollar-crate "macro.decl.meta.dollar-crate")

The keyword metavariable [`$crate`](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.hygiene.crate) can be used to refer to the current crate.

[[macro.decl.meta.edition2021]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.meta.edition2021 "macro.decl.meta.edition2021")

> 2021 Edition differences
>
> Starting with the 2021 edition, `pat` fragment-specifiers match top-level or-patterns (that is, they accept [Pattern](https://doc.rust-lang.org/reference/patterns.html#grammar-Pattern)).
>
> Before the 2021 edition, they match exactly the same fragments as `pat_param` (that is, they accept [PatternNoTopAlt](https://doc.rust-lang.org/reference/patterns.html#grammar-PatternNoTopAlt)).
>
> The relevant edition is the one in effect for the `macro_rules!` definition.

[[macro.decl.meta.edition2024]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.meta.edition2024 "macro.decl.meta.edition2024")

> 2024 Edition differences
>
> Before the 2024 edition, `expr` fragment specifiers do not match [UnderscoreExpression](https://doc.rust-lang.org/reference/expressions/underscore-expr.html#grammar-UnderscoreExpression) or [ConstBlockExpression](https://doc.rust-lang.org/reference/expressions/block-expr.html#grammar-ConstBlockExpression) at the top level. They are allowed within subexpressions.
>
> The `expr_2021` fragment specifier exists to maintain backwards compatibility with editions before 2024.

[[macro.decl.repetition]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.repetition "macro.decl.repetition")

## [Repetitions](https://doc.rust-lang.org/reference/macros-by-example.html#repetitions)

[[macro.decl.repetition.intro]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.repetition.intro "macro.decl.repetition.intro")

In both the matcher and transcriber, repetitions are indicated by placing the
tokens to be repeated inside `$(`…`)`, followed by a repetition operator,
optionally with a separator token between.

[[macro.decl.repetition.separator]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.repetition.separator "macro.decl.repetition.separator")

The separator token can be any token
other than a delimiter or one of the repetition operators, but `;` and `,` are
the most common. For instance, `$( $i:ident ),*` represents any number of
identifiers separated by commas. Nested repetitions are permitted.

[[macro.decl.repetition.operators]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.repetition.operators "macro.decl.repetition.operators")

The repetition operators are:

* `*` — indicates any number of repetitions.
* `+` — indicates any number but at least one.
* `?` — indicates an optional fragment with zero or one occurrence.

[[macro.decl.repetition.optional-restriction]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.repetition.optional-restriction "macro.decl.repetition.optional-restriction")

Since `?` represents at most one occurrence, it cannot be used with a
separator.

[[macro.decl.repetition.fragment]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.repetition.fragment "macro.decl.repetition.fragment")

The repeated fragment both matches and transcribes to the specified number of
the fragment, separated by the separator token. Metavariables are matched to
every repetition of their corresponding fragment. For instance, the `$( $i:ident ),*` example above matches `$i` to all of the identifiers in the list.

During transcription, additional restrictions apply to repetitions so that the
compiler knows how to expand them properly:

1. A metavariable must appear in exactly the same number, kind, and nesting
   order of repetitions in the transcriber as it did in the matcher. So for the
   matcher `$( $i:ident ),*`, the transcribers `=> { $i }`,
   `=> { $( $( $i)* )* }`, and `=> { $( $i )+ }` are all illegal, but
   `=> { $( $i );* }` is correct and replaces a comma-separated list of
   identifiers with a semicolon-separated list.
2. Each repetition in the transcriber must contain at least one metavariable to
   decide how many times to expand it. If multiple metavariables appear in the
   same repetition, they must be bound to the same number of fragments. For
   instance, `( $( $i:ident ),* ; $( $j:ident ),* ) => (( $( ($i,$j) ),* ))` must
   bind the same number of `$i` fragments as `$j` fragments. This means that
   invoking the macro with `(a, b, c; d, e, f)` is legal and expands to
   `((a,d), (b,e), (c,f))`, but `(a, b, c; d, e)` is illegal because it does
   not have the same number. This requirement applies to every layer of nested
   repetitions.

[[macro.decl.scope]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.scope "macro.decl.scope")

## [Scoping, Exporting, and Importing](https://doc.rust-lang.org/reference/macros-by-example.html#scoping-exporting-and-importing)

[[macro.decl.scope.intro]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.scope.intro "macro.decl.scope.intro")

For historical reasons, the scoping of macros by example does not work entirely
like items. Macros have two forms of scope: textual scope, and path-based scope.
Textual scope is based on the order that things appear in source files, or even
across multiple files, and is the default scoping. It is explained further below.
Path-based scope works exactly the same way that item scoping does. The scoping,
exporting, and importing of macros is controlled largely by attributes.

[[macro.decl.scope.unqualified]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.scope.unqualified "macro.decl.scope.unqualified")

When a macro is invoked by an unqualified identifier (not part of a multi-part
path), it is first looked up in textual scoping. If this does not yield any
results, then it is looked up in path-based scoping. If the macro’s name is
qualified with a path, then it is only looked up in path-based scoping.

```
use lazy_static::lazy_static; // Path-based import.

macro_rules! lazy_static { // Textual definition.
    (lazy) => {};
}

lazy_static!{lazy} // Textual lookup finds our macro first.
self::lazy_static!{} // Path-based lookup ignores our macro, finds imported one.
```

[[macro.decl.scope.textual]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.scope.textual "macro.decl.scope.textual")

### [Textual Scope](https://doc.rust-lang.org/reference/macros-by-example.html#textual-scope)

[[macro.decl.scope.textual.intro]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.scope.textual.intro "macro.decl.scope.textual.intro")

Textual scope is based largely on the order that things appear in source files,
and works similarly to the scope of local variables declared with `let` except
it also applies at the module level. When `macro_rules!` is used to define a
macro, the macro enters the scope after the definition (note that it can still
be used recursively, since names are looked up from the invocation site), up
until its surrounding scope, typically a module, is closed. This can enter child
modules and even span across multiple files:

```
//// src/lib.rs
mod has_macro {
    // m!{} // Error: m is not in scope.

    macro_rules! m {
        () => {};
    }
    m!{} // OK: appears after declaration of m.

    mod uses_macro;
}

// m!{} // Error: m is not in scope.

//// src/has_macro/uses_macro.rs

m!{} // OK: appears after declaration of m in src/lib.rs
```

[[macro.decl.scope.textual.shadow]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.scope.textual.shadow "macro.decl.scope.textual.shadow")

It is not an error to define a macro multiple times; the most recent declaration
will shadow the previous one unless it has gone out of scope.

```
```
#![allow(unused)]
fn main() {
macro_rules! m {
    (1) => {};
}

m!(1);

mod inner {
    m!(1);

    macro_rules! m {
        (2) => {};
    }
    // m!(1); // Error: no rule matches '1'
    m!(2);

    macro_rules! m {
        (3) => {};
    }
    m!(3);
}

m!(1);
}
```
```

Macros can be declared and used locally inside functions as well, and work
similarly:

```
```
#![allow(unused)]
fn main() {
fn foo() {
    // m!(); // Error: m is not in scope.
    macro_rules! m {
        () => {};
    }
    m!();
}

// m!(); // Error: m is not in scope.
}
```
```

[[macro.decl.scope.macro\_use]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.scope.macro_use "macro.decl.scope.macro_use")

### [The `macro_use` attribute](https://doc.rust-lang.org/reference/macros-by-example.html#the-macro_use-attribute)

[[macro.decl.scope.macro\_use.mod-decl]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.scope.macro_use.mod-decl "macro.decl.scope.macro_use.mod-decl")

The *`macro_use` attribute* has two purposes. First, it can be used to make a
module’s macro scope not end when the module is closed, by applying it to a
module:

```
```
#![allow(unused)]
fn main() {
#[macro_use]
mod inner {
    macro_rules! m {
        () => {};
    }
}

m!();
}
```
```

[[macro.decl.scope.macro\_use.prelude]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.scope.macro_use.prelude "macro.decl.scope.macro_use.prelude")

Second, it can be used to import macros from another crate, by attaching it to
an `extern crate` declaration appearing in the crate’s root module. Macros
imported this way are imported into the [`macro_use` prelude](https://doc.rust-lang.org/reference/names/preludes.html#macro_use-prelude), not textually,
which means that they can be shadowed by any other name. While macros imported
by `#[macro_use]` can be used before the import statement, in case of a
conflict, the last macro imported wins. Optionally, a list of macros to import
can be specified using the [MetaListIdents](https://doc.rust-lang.org/reference/attributes.html#grammar-MetaListIdents) syntax; this is not supported
when `#[macro_use]` is applied to a module.

```
#[macro_use(lazy_static)] // Or #[macro_use] to import all macros.
extern crate lazy_static;

lazy_static!{}
// self::lazy_static!{} // Error: lazy_static is not defined in `self`
```

[[macro.decl.scope.macro\_use.export]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.scope.macro_use.export "macro.decl.scope.macro_use.export")

Macros to be imported with `#[macro_use]` must be exported with
`#[macro_export]`, which is described below.

[[macro.decl.scope.path]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.scope.path "macro.decl.scope.path")

### [Path-Based Scope](https://doc.rust-lang.org/reference/macros-by-example.html#path-based-scope)

[[macro.decl.scope.path.intro]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.scope.path.intro "macro.decl.scope.path.intro")

By default, a macro has no path-based scope. However, if it has the
`#[macro_export]` attribute, then it is declared in the crate root scope and can
be referred to normally as such:

```
```
#![allow(unused)]
fn main() {
self::m!();
m!(); // OK: Path-based lookup finds m in the current module.

mod inner {
    super::m!();
    crate::m!();
}

mod mac {
    #[macro_export]
    macro_rules! m {
        () => {};
    }
}
}
```
```

[[macro.decl.scope.path.export]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.scope.path.export "macro.decl.scope.path.export")

Macros labeled with `#[macro_export]` are always `pub` and can be referred to
by other crates, either by path or by `#[macro_use]` as described above.

[[macro.decl.hygiene]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.hygiene "macro.decl.hygiene")

## [Hygiene](https://doc.rust-lang.org/reference/macros-by-example.html#hygiene)

[[macro.decl.hygiene.intro]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.hygiene.intro "macro.decl.hygiene.intro")

Macros by example have *mixed-site hygiene*. This means that [loop labels](https://doc.rust-lang.org/reference/expressions/loop-expr.html#loop-labels), [block labels](https://doc.rust-lang.org/reference/expressions/loop-expr.html#labelled-block-expressions), and local variables are looked up at the macro definition site while other symbols are looked up at the macro invocation site. For example:

```
```
#![allow(unused)]
fn main() {
let x = 1;
fn func() {
    unreachable!("this is never called")
}

macro_rules! check {
    () => {
        assert_eq!(x, 1); // Uses `x` from the definition site.
        func();           // Uses `func` from the invocation site.
    };
}

{
    let x = 2;
    fn func() { /* does not panic */ }
    check!();
}
}
```
```

Labels and local variables defined in macro expansion are not shared between invocations, so this code doesn’t compile:

```
```
#![allow(unused)]
fn main() {
macro_rules! m {
    (define) => {
        let x = 1;
    };
    (refer) => {
        dbg!(x);
    };
}

m!(define);
m!(refer);
}
```
```

[[macro.decl.hygiene.crate]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.hygiene.crate "macro.decl.hygiene.crate")

A special case is the `$crate` metavariable. It refers to the crate defining the macro, and can be used at the start of the path to look up items or macros which are not in scope at the invocation site.

```
//// Definitions in the `helper_macro` crate.
#[macro_export]
macro_rules! helped {
    // () => { helper!() } // This might lead to an error due to 'helper' not being in scope.
    () => { $crate::helper!() }
}

#[macro_export]
macro_rules! helper {
    () => { () }
}

//// Usage in another crate.
// Note that `helper_macro::helper` is not imported!
use helper_macro::helped;

fn unit() {
    helped!();
}
```

Note that, because `$crate` refers to the current crate, it must be used with a
fully qualified module path when referring to non-macro items:

```
```
#![allow(unused)]
fn main() {
pub mod inner {
    #[macro_export]
    macro_rules! call_foo {
        () => { $crate::inner::foo() };
    }

    pub fn foo() {}
}
}
```
```

[[macro.decl.hygiene.vis]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.hygiene.vis "macro.decl.hygiene.vis")

Additionally, even though `$crate` allows a macro to refer to items within its
own crate when expanding, its use has no effect on visibility. An item or macro
referred to must still be visible from the invocation site. In the following
example, any attempt to invoke `call_foo!()` from outside its crate will fail
because `foo()` is not public.

```
```
#![allow(unused)]
fn main() {
#[macro_export]
macro_rules! call_foo {
    () => { $crate::foo() };
}

fn foo() {}
}
```
```

> **Version differences**: Prior to Rust 1.30, `$crate` and
> `local_inner_macros` (below) were unsupported. They were added alongside
> path-based imports of macros (described above), to ensure that helper macros
> did not need to be manually imported by users of a macro-exporting crate.
> Crates written for earlier versions of Rust that use helper macros need to be
> modified to use `$crate` or `local_inner_macros` to work well with path-based
> imports.

[[macro.decl.hygiene.local\_inner\_macros]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.hygiene.local_inner_macros "macro.decl.hygiene.local_inner_macros")

When a macro is exported, the `#[macro_export]` attribute can have the
`local_inner_macros` keyword added to automatically prefix all contained macro
invocations with `$crate::`. This is intended primarily as a tool to migrate
code written before `$crate` was added to the language to work with Rust 2018’s
path-based imports of macros. Its use is discouraged in new code.

```
```
#![allow(unused)]
fn main() {
#[macro_export(local_inner_macros)]
macro_rules! helped {
    () => { helper!() } // Automatically converted to $crate::helper!().
}

#[macro_export]
macro_rules! helper {
    () => { () }
}
}
```
```

[[macro.decl.follow-set]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.follow-set "macro.decl.follow-set")

## [Follow-set Ambiguity Restrictions](https://doc.rust-lang.org/reference/macros-by-example.html#follow-set-ambiguity-restrictions)

[[macro.decl.follow-set.intro]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.follow-set.intro "macro.decl.follow-set.intro")

The parser used by the macro system is reasonably powerful, but it is limited in
order to prevent ambiguity in current or future versions of the language.

[[macro.decl.follow-set.token-restriction]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.follow-set.token-restriction "macro.decl.follow-set.token-restriction")

In particular, in addition to the rule about ambiguous expansions, a nonterminal
matched by a metavariable must be followed by a token which has been decided can
be safely used after that kind of match.

As an example, a macro matcher like `$i:expr [ , ]` could in theory be accepted
in Rust today, since `[,]` cannot be part of a legal expression and therefore
the parse would always be unambiguous. However, because `[` can start trailing
expressions, `[` is not a character which can safely be ruled out as coming
after an expression. If `[,]` were accepted in a later version of Rust, this
matcher would become ambiguous or would misparse, breaking working code.
Matchers like `$i:expr,` or `$i:expr;` would be legal, however, because `,` and
`;` are legal expression separators. The specific rules are:

[[macro.decl.follow-set.token-expr-stmt]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.follow-set.token-expr-stmt "macro.decl.follow-set.token-expr-stmt")

* `expr` and `stmt` may only be followed by one of: `=>`, `,`, or `;`.

[[macro.decl.follow-set.token-pat\_param]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.follow-set.token-pat_param "macro.decl.follow-set.token-pat_param")

* `pat_param` may only be followed by one of: `=>`, `,`, `=`, `|`, `if`, or `in`.

[[macro.decl.follow-set.token-pat]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.follow-set.token-pat "macro.decl.follow-set.token-pat")

* `pat` may only be followed by one of: `=>`, `,`, `=`, `if`, or `in`.

[[macro.decl.follow-set.token-path-ty]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.follow-set.token-path-ty "macro.decl.follow-set.token-path-ty")

* `path` and `ty` may only be followed by one of: `=>`, `,`, `=`, `|`, `;`,
  `:`, `>`, `>>`, `[`, `{`, `as`, `where`, or a macro variable of `block`
  fragment specifier.

[[macro.decl.follow-set.token-vis]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.follow-set.token-vis "macro.decl.follow-set.token-vis")

* `vis` may only be followed by one of: `,`, an identifier other than a
  non-raw `priv`, any token that can begin a type, or a metavariable with a
  `ident`, `ty`, or `path` fragment specifier.

[[macro.decl.follow-set.token-other]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.follow-set.token-other "macro.decl.follow-set.token-other")

* All other fragment specifiers have no restrictions.

[[macro.decl.follow-set.edition2021]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.follow-set.edition2021 "macro.decl.follow-set.edition2021")

> 2021 Edition differences
>
> Before the 2021 edition, `pat` may also be followed by `|`.

[[macro.decl.follow-set.repetition]](https://doc.rust-lang.org/reference/macros-by-example.html#r-macro.decl.follow-set.repetition "macro.decl.follow-set.repetition")

When repetitions are involved, then the rules apply to every possible number of
expansions, taking separators into account. This means:

* If the repetition includes a separator, that separator must be able to
  follow the contents of the repetition.
* If the repetition can repeat multiple times (`*` or `+`), then the contents
  must be able to follow themselves.
* The contents of the repetition must be able to follow whatever comes
  before, and whatever comes after must be able to follow the contents of the
  repetition.
* If the repetition can match zero times (`*` or `?`), then whatever comes
  after must be able to follow whatever comes before.

For more detail, see the [formal specification](https://doc.rust-lang.org/reference/macro-ambiguity.html).