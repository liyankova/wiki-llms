---
url: https://doc.rust-lang.org/reference/const_eval.html
title: Constant Evaluation - The Rust Reference
source_domain: doc.rust-lang.org
---

# Constant Evaluation - The Rust Reference

[[const-eval]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval "const-eval")

# [Constant evaluation](https://doc.rust-lang.org/reference/const_eval.html#constant-evaluation)

[[const-eval.general]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.general "const-eval.general")

Constant evaluation is the process of computing the result of
[expressions](https://doc.rust-lang.org/reference/expressions.html) during compilation. Only a subset of all expressions
can be evaluated at compile-time.

[[const-eval.const-expr]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr "const-eval.const-expr")

## [Constant expressions](https://doc.rust-lang.org/reference/const_eval.html#constant-expressions)

[[const-eval.const-expr.general]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.general "const-eval.const-expr.general")

Certain forms of expressions, called constant expressions, can be evaluated at
compile time.

[[const-eval.const-expr.const-context]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.const-context "const-eval.const-expr.const-context")

In [const contexts](https://doc.rust-lang.org/reference/const_eval.html#const-context), these are the only allowed
expressions, and are always evaluated at compile time.

[[const-eval.const-expr.runtime-context]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.runtime-context "const-eval.const-expr.runtime-context")

In other places, such as [let statements](https://doc.rust-lang.org/reference/statements.html#let-statements), constant expressions *may* be, but are not guaranteed to be, evaluated at compile time.

[[const-eval.const-expr.error]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.error "const-eval.const-expr.error")

Behaviors such as out of bounds [array indexing](https://doc.rust-lang.org/reference/expressions/array-expr.html#array-and-slice-indexing-expressions) or [overflow](https://doc.rust-lang.org/reference/expressions/operator-expr.html#overflow) are compiler errors if the value
must be evaluated at compile time (i.e. in const contexts). Otherwise, these
behaviors are warnings, but will likely panic at run-time.

[[const-eval.const-expr.list]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.list "const-eval.const-expr.list")

The following expressions are constant expressions, so long as any operands are
also constant expressions and do not cause any [`Drop::drop`](https://doc.rust-lang.org/reference/destructors.html) calls
to be run.

[[const-eval.const-expr.literal]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.literal "const-eval.const-expr.literal")

* [Literals](https://doc.rust-lang.org/reference/expressions/literal-expr.html).

[[const-eval.const-expr.parameter]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.parameter "const-eval.const-expr.parameter")

* [Const parameters](https://doc.rust-lang.org/reference/items/generics.html).

[[const-eval.const-expr.path-item]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.path-item "const-eval.const-expr.path-item")

* [Paths](https://doc.rust-lang.org/reference/expressions/path-expr.html) to [functions](https://doc.rust-lang.org/reference/items/functions.html) and [constants](https://doc.rust-lang.org/reference/items/constant-items.html).
  Recursively defining constants is not allowed.

[[const-eval.const-expr.path-static]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.path-static "const-eval.const-expr.path-static")

* Paths to [statics](https://doc.rust-lang.org/reference/items/static-items.html) with these restrictions:

  + Writes to `static` items are not allowed in any constant evaluation context.
  + Reads from `extern` statics are not allowed in any constant evaluation context.
  + If the evaluation is *not* carried out in an initializer of a `static` item, then reads from any mutable `static` are not allowed. A mutable `static` is a `static mut` item, or a `static` item with an interior-mutable type.

  These requirements are checked only when the constant is evaluated. In other words, having such accesses syntactically occur in const contexts is allowed as long as they never get executed.

[[const-eval.const-expr.tuple]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.tuple "const-eval.const-expr.tuple")

* [Tuple expressions](https://doc.rust-lang.org/reference/expressions/tuple-expr.html).

[[const-eval.const-expr.array]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.array "const-eval.const-expr.array")

* [Array expressions](https://doc.rust-lang.org/reference/expressions/array-expr.html).

[[const-eval.const-expr.constructor]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.constructor "const-eval.const-expr.constructor")

* [Struct](https://doc.rust-lang.org/reference/expressions/struct-expr.html) expressions.

[[const-eval.const-expr.block]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.block "const-eval.const-expr.block")

* [Block expressions](https://doc.rust-lang.org/reference/expressions/block-expr.html), including `unsafe` and `const` blocks.
  + [let statements](https://doc.rust-lang.org/reference/statements.html#let-statements) and thus irrefutable [patterns](https://doc.rust-lang.org/reference/patterns.html), including mutable bindings
  + [assignment expressions](https://doc.rust-lang.org/reference/expressions/operator-expr.html#assignment-expressions)
  + [compound assignment expressions](https://doc.rust-lang.org/reference/expressions/operator-expr.html#compound-assignment-expressions)
  + [expression statements](https://doc.rust-lang.org/reference/statements.html#expression-statements)

[[const-eval.const-expr.field]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.field "const-eval.const-expr.field")

* [Field](https://doc.rust-lang.org/reference/expressions/field-expr.html) expressions.

[[const-eval.const-expr.index]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.index "const-eval.const-expr.index")

* Index expressions, [array indexing](https://doc.rust-lang.org/reference/expressions/array-expr.html#array-and-slice-indexing-expressions) or [slice](https://doc.rust-lang.org/reference/types/slice.html) with a `usize`.

[[const-eval.const-expr.range]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.range "const-eval.const-expr.range")

* [Range expressions](https://doc.rust-lang.org/reference/expressions/range-expr.html).

[[const-eval.const-expr.closure]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.closure "const-eval.const-expr.closure")

* [Closure expressions](https://doc.rust-lang.org/reference/expressions/closure-expr.html) which don’t capture variables from the environment.

[[const-eval.const-expr.builtin-arith-logic]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.builtin-arith-logic "const-eval.const-expr.builtin-arith-logic")

* Built-in [negation](https://doc.rust-lang.org/reference/expressions/operator-expr.html#negation-operators), [arithmetic](https://doc.rust-lang.org/reference/expressions/operator-expr.html#arithmetic-and-logical-binary-operators), [logical](https://doc.rust-lang.org/reference/expressions/operator-expr.html#arithmetic-and-logical-binary-operators), [comparison](https://doc.rust-lang.org/reference/expressions/operator-expr.html#comparison-operators) or [lazy boolean](https://doc.rust-lang.org/reference/expressions/operator-expr.html#lazy-boolean-operators)
  operators used on integer and floating point types, `bool`, and `char`.

[[const-eval.const-expr.borrows]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.borrows "const-eval.const-expr.borrows")

* All forms of [borrow](https://doc.rust-lang.org/reference/expressions/operator-expr.html#borrow-operators)s, including raw borrows, except borrows of expressions whose temporary scopes would be extended (see [temporary lifetime extension](https://doc.rust-lang.org/reference/destructors.html#r-destructors.scope.lifetime-extension)) to the end of the program and which are either:

  + Mutable borrows.
  + Shared borrows of expressions that result in values with [interior mutability](https://doc.rust-lang.org/reference/interior-mutability.html).

  ```
  ```
  #![allow(unused)]
  fn main() {
  // Due to being in tail position, this borrow extends the scope of the
  // temporary to the end of the program. Since the borrow is mutable,
  // this is not allowed in a const expression.
  const C: &u8 = &mut 0; // ERROR not allowed
  }
  ```
  ```

  ```
  ```
  #![allow(unused)]
  fn main() {
  // Const blocks are similar to initializers of `const` items.
  let _: &u8 = const { &mut 0 }; // ERROR not allowed
  }
  ```
  ```

  ```
  ```
  #![allow(unused)]
  fn main() {
  use core::sync::atomic::AtomicU8;
  // This is not allowed as 1) the temporary scope is extended to the
  // end of the program and 2) the temporary has interior mutability.
  const C: &AtomicU8 = &AtomicU8::new(0); // ERROR not allowed
  }
  ```
  ```

  ```
  ```
  #![allow(unused)]
  fn main() {
  use core::sync::atomic::AtomicU8;
  // As above.
  let _: &_ = const { &AtomicU8::new(0) }; // ERROR not allowed
  }
  ```
  ```

  ```
  ```
  #![allow(unused)]
  fn main() {
  #![allow(static_mut_refs)]
  // Even though this borrow is mutable, it's not of a temporary, so
  // this is allowed.
  const C: &u8 = unsafe { static mut S: u8 = 0; &mut S }; // OK
  }
  ```
  ```

  ```
  ```
  #![allow(unused)]
  fn main() {
  use core::sync::atomic::AtomicU8;
  // Even though this borrow is of a value with interior mutability,
  // it's not of a temporary, so this is allowed.
  const C: &AtomicU8 = {
      static S: AtomicU8 = AtomicU8::new(0); &S // OK
  };
  }
  ```
  ```

  ```
  ```
  #![allow(unused)]
  fn main() {
  use core::sync::atomic::AtomicU8;
  // This shared borrow of an interior mutable temporary is allowed
  // because its scope is not extended.
  const C: () = { _ = &AtomicU8::new(0); }; // OK
  }
  ```
  ```

  ```
  ```
  #![allow(unused)]
  fn main() {
  // Even though the borrow is mutable and the temporary lives to the
  // end of the program due to promotion, this is allowed because the
  // borrow is not in tail position and so the scope of the temporary
  // is not extended via temporary lifetime extension.
  const C: () = { let _: &'static mut [u8] = &mut []; }; // OK
  //                                              ~~
  //                                     Promoted temporary.
  }
  ```
  ```

  > Note
  >
  > In other words — to focus on what’s allowed rather than what’s not allowed — shared borrows of interior mutable data and mutable borrows are only allowed in a [const context](https://doc.rust-lang.org/reference/const_eval.html#const-context) when the borrowed [place expression](https://doc.rust-lang.org/reference/expressions.html#r-expr.place-value.place-memory-location) is *transient*, *indirect*, or *static*.
  >
  > A place expression is *transient* if it is a variable local to the current const context or an expression whose temporary scope is contained inside the current const context.
  >
  > ```
  > ```
  > #![allow(unused)]
  > fn main() {
  > // The borrow is of a variable local to the initializer, therefore
  > // this place expresssion is transient.
  > const C: () = { let mut x = 0; _ = &mut x; };
  > }
  > ```
  > ```
  >
  > ```
  > ```
  > #![allow(unused)]
  > fn main() {
  > // The borrow is of a temporary whose scope has not been extended,
  > // therefore this place expression is transient.
  > const C: () = { _ = &mut 0u8; };
  > }
  > ```
  > ```
  >
  > ```
  > ```
  > #![allow(unused)]
  > fn main() {
  > // When a temporary is promoted but not lifetime extended, its
  > // place expression is still treated as transient.
  > const C: () = { let _: &'static mut [u8] = &mut []; };
  > }
  > ```
  > ```
  >
  > A place expression is *indirect* if it is a [dereference expression](https://doc.rust-lang.org/reference/expressions/operator-expr.html#the-dereference-operator).
  >
  > ```
  > ```
  > #![allow(unused)]
  > fn main() {
  > const C: () = { _ = &mut *(&mut 0); };
  > }
  > ```
  > ```
  >
  > A place expression is *static* if it is a `static` item.
  >
  > ```
  > ```
  > #![allow(unused)]
  > fn main() {
  > #![allow(static_mut_refs)]
  > const C: &u8 = unsafe { static mut S: u8 = 0; &mut S };
  > }
  > ```
  > ```

  > Note
  >
  > One surprising consequence of these rules is that we allow this,
  >
  > ```
  > ```
  > #![allow(unused)]
  > fn main() {
  > const C: &[u8] = { let x: &mut [u8] = &mut []; x }; // OK
  > //                                    ~~~~~~~
  > // Empty arrays are promoted even behind mutable borrows.
  > }
  > ```
  > ```
  >
  > but we disallow this similar code:
  >
  > ```
  > ```
  > #![allow(unused)]
  > fn main() {
  > const C: &[u8] = &mut []; // ERROR
  > //               ~~~~~~~
  > //           Tail expression.
  > }
  > ```
  > ```
  >
  > The difference between these is that, in the first, the empty array is [promoted](https://doc.rust-lang.org/reference/destructors.html#constant-promotion) but its scope does not undergo [temporary lifetime extension](https://doc.rust-lang.org/reference/destructors.html#r-destructors.scope.lifetime-extension), so we consider the [place expression](https://doc.rust-lang.org/reference/expressions.html#r-expr.place-value.place-memory-location) to be transient (even though after promotion the place indeed lives to the end of the program). In the second, the scope of the empty array temporary does undergo lifetime extension, and so it is rejected due to being a mutable borrow of a lifetime-extended temporary (and therefore borrowing a non-transient place expression).
  >
  > The effect is surprising because temporary lifetime extension, in this case, causes less code to compile than would without it.
  >
  > See [issue #143129](https://github.com/rust-lang/rust/issues/143129) for more details.

[[const-eval.const-expr.deref]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.deref "const-eval.const-expr.deref")

* The [dereference operator](https://doc.rust-lang.org/reference/expressions/operator-expr.html#the-dereference-operator) except for raw pointers.

[[const-eval.const-expr.group]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.group "const-eval.const-expr.group")

* [Grouped](https://doc.rust-lang.org/reference/expressions/grouped-expr.html) expressions.

[[const-eval.const-expr.cast]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.cast "const-eval.const-expr.cast")

* [Cast](https://doc.rust-lang.org/reference/expressions/operator-expr.html#type-cast-expressions) expressions, except
  + pointer to address casts and
  + function pointer to address casts.

[[const-eval.const-expr.const-fn]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.const-fn "const-eval.const-expr.const-fn")

* Calls of [const functions](https://doc.rust-lang.org/reference/items/functions.html#const-functions) and const methods.

[[const-eval.const-expr.loop]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.loop "const-eval.const-expr.loop")

* [loop](https://doc.rust-lang.org/reference/expressions/loop-expr.html#infinite-loops) and [while](https://doc.rust-lang.org/reference/expressions/loop-expr.html#predicate-loops) expressions.

[[const-eval.const-expr.if-match]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-expr.if-match "const-eval.const-expr.if-match")

* [if](https://doc.rust-lang.org/reference/expressions/if-expr.html#if-expressions) and [match](https://doc.rust-lang.org/reference/expressions/match-expr.html) expressions.

[[const-eval.const-context]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-context "const-eval.const-context")

## [Const context](https://doc.rust-lang.org/reference/const_eval.html#const-context)

[[const-eval.const-context.general]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-context.general "const-eval.const-context.general")

A *const context* is one of the following:

[[const-eval.const-context.array-length]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-context.array-length "const-eval.const-context.array-length")

* [Array type length expressions](https://doc.rust-lang.org/reference/types/array.html)

[[const-eval.const-context.repeat-length]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-context.repeat-length "const-eval.const-context.repeat-length")

* [Array repeat length expressions](https://doc.rust-lang.org/reference/expressions/array-expr.html)

[[const-eval.const-context.init]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-context.init "const-eval.const-context.init")

* The initializer of
  + [constants](https://doc.rust-lang.org/reference/items/constant-items.html)
  + [statics](https://doc.rust-lang.org/reference/items/static-items.html)
  + [enum discriminants](https://doc.rust-lang.org/reference/items/enumerations.html#discriminants)

[[const-eval.const-context.generic]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-context.generic "const-eval.const-context.generic")

* A [const generic argument](https://doc.rust-lang.org/reference/items/generics.html#const-generics)

[[const-eval.const-context.block]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-context.block "const-eval.const-context.block")

* A [const block](https://doc.rust-lang.org/reference/expressions/block-expr.html#const-blocks)

[[const-eval.const-context.outer-generics]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-context.outer-generics "const-eval.const-context.outer-generics")

Const contexts that are used as parts of types (array type and repeat length
expressions as well as const generic arguments) can only make restricted use of
surrounding generic parameters: such an expression must either be a single bare
const generic parameter, or an arbitrary expression not making use of any
generics.

[[const-eval.const-fn]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-fn "const-eval.const-fn")

## [Const Functions](https://doc.rust-lang.org/reference/const_eval.html#const-functions)

[[const-eval.const-fn.general]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-fn.general "const-eval.const-fn.general")

A *const fn* is a function that one is permitted to call from a const context.

[[const-eval.const-fn.usage]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-fn.usage "const-eval.const-fn.usage")

Declaring a function
`const` has no effect on any existing uses, it only restricts the types that arguments and the
return type may use, and restricts the function body to constant expressions.

[[const-eval.const-fn.const-context]](https://doc.rust-lang.org/reference/const_eval.html#r-const-eval.const-fn.const-context "const-eval.const-fn.const-context")

When called from a const context, the function is interpreted by the
compiler at compile time. The interpretation happens in the
environment of the compilation target and not the host. So `usize` is
`32` bits if you are compiling against a `32` bit system, irrelevant
of whether you are building on a `64` bit or a `32` bit system.